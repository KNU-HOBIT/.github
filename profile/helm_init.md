## Helm 설치

1. 헬름 설치
    ```
    curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 > get_helm.sh

    chmod 700 get_helm.sh

    ./get_helm.sh
    ```
    다음과 같이 출력.
    ```
    [WARNING] Could not find git. It is required for plugin installation.
    Downloading https://get.helm.sh/helm-v3.11.3-linux-amd64.tar.gz
    Verifying checksum... Done.
    Preparing to install helm into /usr/local/bin
    ```
4. 헬름 설치 확인.
    ```
    helm version
    ```