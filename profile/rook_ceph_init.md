## Pre-requisites for Ceph Installation

- Ensure each Kubernetes worker node has a raw device for Ceph storage.
  - This should be a clean SSD or HDD that has never been used and is unformatted (i.e., it should not have a filesystem).

- Ceph will be configured as a 3-node cluster, so each of the three worker nodes should have one raw device.

Once you have attached the raw devices to all worker nodes, run the following command to verify that the storage is in a clean state:

```sh
lsblk -f
```


# Getting start

>_Perform the following commands on a kubernetes bastion node or a PC capable of running `kubectl`.</br>
>Please refer to [this guide](k8s_init.md) first._

1. GitHub에서 Rook operator를 내려 받는다.
    ```
    git clone --single-branch --branch v1.10.13 https://github.com/rook/rook.git

    cd rook/deploy/examples
    ```

2. Rook operator 운영에 필요한 custom resource definition을 생성하고 </br>
    Rook operator 리소스를 kubernetes cluster에 배포한다.
    ```
    kubectl create -f crds.yaml -f common.yaml -f operator.yaml
    ```


3. rook-ceph-operator pod가 running 상태인지 확인한다.
    ```
    kubectl -n rook-ceph get pod
    ```

4. Ceph cluster를 생성
    ```
    kubectl create -f cluster.yaml
    ```
    > 다소 오래 걸리는 작업.
    따라서, 아래와 같이 rook-ceph-operator 로그를 보면서 진행 과정을 보는 것이 좋다.</br>
    >```
    >kubectl -n rook-ceph logs -l app=rook-ceph-operator -f
    >```
    >대략 3분 정도 로그가 올라가다가 마지막 부분에 "op-osd: finished .... "
    이런 문구가 출력되면 작업이 끝난 것이다.
    >```
    >... 중간 생략 ...
    > 
    >2023-01-06 07:05:19.680387 I | cephclient: successfully disallowed pre-quincy osds >and enabled all new quincy-only functionality
    >2023-01-06 07:05:19.681868 I | op-osd: finished running OSDs in namespace "rook-ceph"
    >2023-01-06 07:05:19.682577 I | ceph-cluster-controller: done reconciling ceph cluster >in namespace "rook-ceph"
    >```
    >위 문장이 출력되면, 끝난 것이다. Ctrl+C 키를 눌러서 kubectl log 명령을 종료시킨다
5. Ceph 관련 pod가 running 상태인지 확인한다.
    ```
    kubectl -n rook-ceph get pod
    ```
    ```
    NAME                                                 READY   STATUS   
    csi-cephfsplugin-provisioner-d77bb49c6-n5tgs         5/5     Running  
    csi-cephfsplugin-provisioner-d77bb49c6-v9rvn         5/5     Running  
    csi-cephfsplugin-rthrp                               3/3     Running  
    csi-rbdplugin-hbsm7                                  3/3     Running  
    csi-rbdplugin-provisioner-5b5cd64fd-nvk6c            6/6     Running  
    csi-rbdplugin-provisioner-5b5cd64fd-q7bxl            6/6     Running  
    rook-ceph-crashcollector-minikube-5b57b7c5d4-hfldl   1/1     Running  
    rook-ceph-mgr-a-64cd7cdf54-j8b5p                     1/1     Running  
    rook-ceph-mon-a-694bb7987d-fp9w7                     1/1     Running  
    rook-ceph-mon-b-856fdd5cb9-5h2qk                     1/1     Running  
    rook-ceph-mon-c-57545897fc-j576h                     1/1     Running  
    rook-ceph-operator-85f5b946bd-s8grz                  1/1     Running  
    rook-ceph-osd-0-6bb747b6c5-lnvb6                     1/1     Running  
    rook-ceph-osd-1-7f67f9646d-44p7v                     1/1     Running  
    rook-ceph-osd-2-6cd4b776ff-v4d68                     1/1     Running  
    rook-ceph-osd-prepare-node1-vx2rz                    0/2     Completed
    rook-ceph-osd-prepare-node2-ab3fd                    0/2     Completed
    rook-ceph-osd-prepare-node3-w4xyz                    0/2     Completed
    ```
6. Rook toolbox를 설치한다.
    ```
    kubectl create -f deploy/examples/toolbox.yaml
    ```

7. Rook toolbox pod 내부에서 `ceph status` 명령을 수행하여 ceph cluster 상태를 조회한다.
    ```
    kubectl -n rook-ceph exec -it deploy/rook-ceph-tools -- bash
    ```
    ```
    bash-4.4$ ceph status
      cluster:
        id:     661d89a0-d4c5-432b-97d7-6a4d06beaf52
        health: HEALTH_OK
    
      services:
        mon: 3 daemons, quorum a,b,d (age 10m)
        mgr: b(active, since 11m), standbys: a
        osd: 3 osds: 3 up (since 10m), 3 in (since 11m)
    
      data:
        pools:   1 pools, 1 pgs
        objects: 2 objects, 449 KiB
        usage:   62 MiB used, 750 GiB / 750 GiB avail
        pgs:     1 active+clean
    
    bash-4.4$
    bash-4.4$
    bash-4.4$
    bash-4.4$ ceph df
    --- RAW STORAGE ---
    CLASS     SIZE    AVAIL    USED  RAW USED  %RAW USED
    hdd    750 GiB  750 GiB  62 MiB    62 MiB          0
    TOTAL  750 GiB  750 GiB  62 MiB    62 MiB          0
    
    --- POOLS ---
    POOL  ID  PGS   STORED  OBJECTS     USED  %USED  MAX AVAIL
    .mgr   1    1  449 KiB        2  1.3 MiB      0    237 GiB
    
    bash-4.4$ exit
    
    $
    ```
    The Rook cluster has been created.

## Shared Filesystem (create StorageClass)
Create a filesystem to be shared across multiple pods (RWX)

1. Create the filesystem (in `deploy/examples`)
    ```
    kubectl create -f filesystem.yaml
    ```

    To confirm the filesystem is configured

    ```
    kubectl -n rook-ceph get pod -l app=rook-ceph-mds
    ```
    ```
    NAME                                      READY     STATUS 
    rook-ceph-mds-myfs-7d59fdfcf4-h8kw9       1/1       Running
    rook-ceph-mds-myfs-7d59fdfcf4-kgkjp       1/1       Running
    ```
    & A new line will be shown with ceph status for the mds service
    ```
    kubectl -n rook-ceph exec -it deploy/rook-ceph-tools -- bash
    ```
    ```
    bash-4.4$ ceph status
    [...]
      services:
        mds: myfs-1/1/1 up {[myfs:0]=mzw58b=up:active}, 1 up:standby-replay
    ```



2. Create the storage class. (in `deploy/examples/csi/cephfs`)

    Rook이 스토리지 프로비저닝을 시작하기 전에, 파일시스템을 기반으로 `StorageClass`를 생성해야 함.</br>
    이는 쿠버네티스가 CSI 드라이버와 상호 운용하여 `persistent volumes`을 생성하는 데 필요.
    ```
    kubectl create -f storageclass.yaml
    ```
