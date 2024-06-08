


<!-- Improved compatibility of back to top link: See: https://github.com/othneildrew/Best-README-Template/pull/73 -->
<a name="readme-top"></a>
<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Don't forget to give the project a star!
*** Thanks again! Now go create something AMAZING! :D
-->



<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
<!-- [![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url] -->



<!-- PROJECT LOGO -->
<br />
<div align="center">
    <p align="center">
    <img src="https://github.com/blueberry0814/hobitfront_jiye/assets/155938701/512f8d1d-408f-4cdb-b9ff-1b319caa0b65" width="70%">
    <p/>

  <h3 align="center">HOBIT</h3>

  <p align="center">
    산업용 사물 인터넷 빅데이터 처리를 위한 온-프리미스 기반 분산 처리 프레임워크
    <br />
    <a href="#getting-started"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/othneildrew/Best-README-Template">🎥 View Demo</a>
    ·
    <a href="https://github.com/othneildrew/Best-README-Template/issues/new?labels=bug&template=bug-report---.md">🐞 Report Bug</a>
    ·
    <a href="https://github.com/othneildrew/Best-README-Template/issues/new?labels=enhancement&template=feature-request---.md">💬 Request Feature</a>
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <!-- <li><a href="#installation">Installation</a></li> -->
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <!-- <li><a href="#roadmap">Roadmap</a></li> -->
    <!-- <li><a href="#contributing">Contributing</a></li> -->
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

<p>
<img src="profile/images/output.png" width="49%">
<img src="profile/images/temp.png" width="49%">
</p>

산업계에서 작업 효율과 안전을 높이기 위해 산업 사물 인터넷(IIoT) 데이터의 활용이 점점 중요해지고 있습니다. 많은 제조 기업들이 센서 데이터 파이프라인을 통해 IIoT 빅데이터를 수집하고 저장하고 있지만, 대용량 데이터를 효과적으로 전송하고 처리할 수 있는 소프트웨어 인프라는 부족한 상태입니다.이를 해결하기 위해, **Apach Kafka**와 **Apache Spark**를 기반으로 한 온-프리미스 IIoT 빅데이터 처리 플랫폼인 **HOBIT** 시스템을 제안합니다. HOBIT 시스템은 데이터 수집과 저장, 고속 분석을 강화하여 기존 REST API 방식보다 데이터 전송 처리 속도를 **10배** 이상 향상시킬 수 있었으며, AI 모델 학습에 있어서도 병렬 분산 컴퓨팅을 통해 속도를 단일 컴퓨팅 환경 대비 **4배** 빠르게 향상시켰습니다. 이를 통해 제조 기업들이 클라우드 비용을 절약하며 실시간으로 경제적이고 효율적인 빅데이터 처리 및 분석을 할 수 있을 것으로 기대됩니다.

### Architecture
<p align="center">
<img src="profile/images/arch.png" width="90%">
</p>

### Module configuration and roles:
* **IoT Platform** : IoT 데이터 수집 및 전달
    * **CSV to Protobuf** : 시계열 IoT 데이터셋(.csv)을 활용하여 센서를 시뮬레이션 (MQTT Producer)
    * **Influx MQTT Connector** : 실시간으로 InfluxDB에 센서 데이터를 적재 (MQTT Consumer)
    * **IoT Server** : 적재된 IoT 데이터를 요청에 따라 병렬적으로 Kafka 브로커에 전송 (Kafka Producer)
    * **InfluxDB** : IoT 데이터 저장소
    
* **HOBIT** : IoT 전용 빅데이터 처리 플랫폼
    * **MQTT Broker** : MQTT를 통한 실시간 IoT 데이터 파이프라인
    * **Spark Cluster** : 대규모 데이터 처리용 통합 분석 엔진
    * **Kafka Cluster** : 분산 스트리밍 오픈소스 플랫폼

* **Application** : IoT플랫폼과 HOBIT을 이용하는 어플리케이션 계층
    * **React** : 서버로부터 받은 데이터 시각화, API에 대한 UI/UX 제공
    * **FastAPI Server** : 어플리케이션 API 제공. 주로 사용자 요구에 따라, IoT 서버와 HOBIT의 모듈로 IoT 데이터 전송 및 가공을 요청 (Spark Driver에 해당)
    * **MySQL** : 해당 어플리케이션 운영에 필요한 데이터 저장소

<p align="right">(<a href="#readme-top">back to top</a>)</p>


### Built With

| Category | Technology |
|----------|------------|
| Frontend(예시) | [![React][React.js]][React-url][![npm][npm]][npm-url][![Bootstrap][Bootstrap.com]][Bootstrap-url][![Socket.io][Socket.io]][Socket.io-url][![JavaScript][JavaScript.js]][JavaScript-url][![Figma][Figma]][Figma-url] |
| Face Identify Server(예시) | [![Flask][Flask]][Flask-url][![OpenCV][OpenCV]][OpenCV-url][![Socket.io][Socket.io]][Socket.io-url][![Python][Python.org]][Python-url] |
| Kiosk API Server(예시) | [![Nodejs][Nodejs]][Nodejs-url][![npm][npm]][npm-url][![Prisma][Prisma]][Prisma-url][![JavaScript][JavaScript.js]][JavaScript-url] |
| Database(예시) | [![MySQL][MySQL]][MySQL-url][![Prisma][Prisma]][Prisma-url] |
| Development Environment(예시) | [![macOS][macOS]][macOS-url] |
|------(위에는 예시)----|-------(아래는 우리꺼)-----|
| Sensor Simulation | CSV, Protobuf, MQTT, Python ... |
| IoT Platform | Golang, Go Kafka Client, Go Influx client, InfluxDB, ... ? ,? ,? ( 쓴 언어나,라이브러리,, )  |
| HOBIT |<img src="https://img.shields.io/badge/apachespark-E25A1C?style=flat-square&logo=apachespark&logoColor=white"/><img src="https://img.shields.io/badge/apachekafka-231F20?style=flat-square&logo=apachekafka&logoColor=white"/><img src="https://img.shields.io/badge/eclipsemosquitto-3C5280?style=flat-square&logo=eclipsemosquitto&logoColor=white"/><img src="https://img.shields.io/badge/k3s-FFC61C?style=flat-square&logo=k3s&logoColor=white"/>, k9s, ... |
| Application | [![React][React.js]][React-url][![npm][npm]][npm-url][![Bootstrap][Bootstrap.com]][Bootstrap-url][![JavaScript][JavaScript.js]][JavaScript-url]![js](https://img.shields.io/badge/CSS-239120?&style=for-the-badge&logo=css3&logoColor=white)FastAPI, Pyspark, MySQL, ? ,? ,? ( 쓴 언어나,라이브러리,, )  |
| Development Environment | 리눅스, 맥 ,? ,?  |



<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- GETTING STARTED -->
## Prerequisites


### H/W Requirements
  </summary>

<details>
  <summary><b>k8s Cluster</b> ( >= 3 node)</summary>

| | |
|-|-|
| OS | Ubuntu 20.04.6 LTS (Focal Fossa) |
| CPU | Intel Core i7-10700K 3.80GHz |
| RAM | 64GB DDR4, 3200 MT/s, 16GB x 4 |
</details>
<details>
  <summary><b>Other spare servers</b> ( for Iot Platform / Application layer )</summary>

| | |
|-|-|
| OS | Ubuntu 20.04.6 LTS (Focal Fossa) |
| CPU | Intel Core i7-10700K@3.80GHz |
| RAM | 32GB DDR4, 3200 MT/s, 16GB x 2 |

> Optional, but Recommand

</details>

<details>
  <summary><b>Sensor Simulation</b> (in Our case, <b>x7</b> use)</summary>

| | |
|-|-|
| Model | Raspberry Pi 4 Model B Rev 1.4 |
| OS | Ubuntu 22.04.1 LTS (Jammy JeIlyfish) |

</details>


### S/W Requirements
| | |
|-|-|
| **k8s Cluster** |  v1.28.7+k3s1 |
| **Helm** | v3.11.3 |
| **Rook-Ceph** | v1.13.7 |
| **Spark Cluster** | 3.5.1 ( **Standalond** on K8s) |
| **Strimzi** | 0.40.0 |
| **Kafka Cluster** | 3.7.0 ( **Kraft** Mode ) |
| **InfluxDB** | InfluxDB OSS v2.7.4 |
| **Golang** |  go1.22.2 linux/amd64 (common) |
| **Protobuf Compiler** | libprotoc 27.0 |


_For other Library or Language versions, please refer to the respective repositories._

## Getting Started
_클릭하면 각 모듈에 대한 Repo로 이동._

### K8s Setting Menual
* [**Init k8s**](profile/k8s_init.md)
* [**Install Helm**](profile/helm_init.md)
* [**Init Rook-Cefh**](profile/rook_ceph_init.md)
> Required steps for setting up HOBIT. 

### Each Module Repo or Docs
* **IoT Platform** 
    * **CSV to Protobuf** // 영우형이랑 같이 레포 합치고,
    * [**Influx MQTT Connector**](https://github.com/KNU-HOBIT/mqtt-influxdb-connector)
    * [**IoT Server**](https://github.com/KNU-HOBIT/large-dataset-delivery-kafka)
    * [**InfluxDB**](profile/influx_helm_init.md)
* **HOBIT**
    * [**MQTT Broker**](https://github.com/KNU-HOBIT/mosquitto-kube)
    * [**Spark Cluster**](https://github.com/KNU-HOBIT/spark-standalone-kube)
    * [**Kafka Cluster**](https://github.com/KNU-HOBIT/kafka-kube)
* **Application**
    * **React** // 현재 있음
    * **FastAPI Server** // 현재 있음
    * [**MySQL**](https://github.com/KNU-HOBIT/mysql-kube)

아래는 각 Repo 의 README에 있어야할 것 예시.

_다음은 잠재 고객에게 앱 설치 및 설정에 대해 안내하는 방법의 예시입니다. 이 템플릿은 외부 종속성이나 서비스에 의존하지 않습니다.._

1. Get a free API Key at [https://example.com](https://example.com)
2. Clone the repo
   ```sh
   git clone https://github.com/KNU-HOBIT/knu_hobit_gr.git
   ```
   ```sh
   cd knu_hobit_gr
   ```
    ```sh
   git checkout master
   ```
4. Install NPM packages
   ```sh
   npm install
   ```
5. Run Application
    ```sh
   npm start
   ```



<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage

이 공간을 사용하여 프로젝트 사용 방법에 대한 유용한 예를 보여주세요. 추가 스크린샷, 코드 예제 및 데모도 이 공간에서 잘 작동합니다. 더 많은 리소스로 연결할 수도 있습니다.

_For more examples, please refer to the [Documentation](https://example.com)_

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ROADMAP -->
<!-- ## Roadmap

- [x] Add Changelog
- [x] Add back to top links
- [ ] Add Additional Templates w/ Examples
- [ ] Add "components" document to easily copy & paste sections of the readme
- [ ] Multi-language Support
    - [ ] Chinese
    - [ ] Spanish

See the [open issues](https://github.com/othneildrew/Best-README-Template/issues) for a full list of proposed features (and known issues).

<p align="right">(<a href="#readme-top">back to top</a>)</p> -->



<!-- CONTRIBUTING -->
<!-- ## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#readme-top">back to top</a>)</p> -->



<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTACT -->
## Contact

#### 💡 노유수 ([noFlowWater](https://github.com/noFlowWater)) : [noyusu98@gmail.com](mailto:noyusu98@gmail.com)

#### 💡 박규리 ([parkgyul](https://github.com/parkgyul)) : [haha0888@naver.com](mailto:haha0888@naver.com)

#### 💡 박지현 ([parkjihyeon124594](https://github.com/parkjihyeon124594)) : [blackhole124594@naver.com](mailto:blackhole124594@naver.com)

#### 💡 원지예 ([blueberry0814](https://github.com/blueberry0814)) : [oneone8773@gmail.com](mailto:oneone8773@gmail.com)

#### 💡 장영우 ([jangscon](https://github.com/jangscon)) : [jtu6568@gmail.com](mailto:jtu6568@gmail.com)


<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

이 공간에 도움이 되었거나 공로를 인정하고 싶은 리소스를 나열하세요. 시작을 위해 제가 가장 좋아하는 몇 가지를 포함시켜 보았습니다!

* [Choose an Open Source License](https://choosealicense.com)
* [GitHub Emoji Cheat Sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet)
* [Malven's Flexbox Cheatsheet](https://flexbox.malven.co/)
* [Malven's Grid Cheatsheet](https://grid.malven.co/)
* [Img Shields](https://shields.io)
* [GitHub Pages](https://pages.github.com)
* [Font Awesome](https://fontawesome.com)
* [React Icons](https://react-icons.github.io/react-icons/search)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/othneildrew/Best-README-Template.svg?style=for-the-badge
[contributors-url]: https://github.com/othneildrew/Best-README-Template/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/othneildrew/Best-README-Template.svg?style=for-the-badge
[forks-url]: https://github.com/othneildrew/Best-README-Template/network/members
[stars-shield]: https://img.shields.io/github/stars/othneildrew/Best-README-Template.svg?style=for-the-badge
[stars-url]: https://github.com/othneildrew/Best-README-Template/stargazers
[issues-shield]: https://img.shields.io/github/issues/othneildrew/Best-README-Template.svg?style=for-the-badge
[issues-url]: https://github.com/othneildrew/Best-README-Template/issues
[license-shield]: https://img.shields.io/github/license/othneildrew/Best-README-Template.svg?style=for-the-badge
[license-url]: https://github.com/othneildrew/Best-README-Template/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/othneildrew
[product-screenshot]: images/screenshot.png
[Next.js]: https://img.shields.io/badge/next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white
[Next-url]: https://nextjs.org/
[React.js]: https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB
[React-url]: https://reactjs.org/
[Vue.js]: https://img.shields.io/badge/Vue.js-35495E?style=for-the-badge&logo=vuedotjs&logoColor=4FC08D
[Vue-url]: https://vuejs.org/
[Angular.io]: https://img.shields.io/badge/Angular-DD0031?style=for-the-badge&logo=angular&logoColor=white
[Angular-url]: https://angular.io/
[Svelte.dev]: https://img.shields.io/badge/Svelte-4A4A55?style=for-the-badge&logo=svelte&logoColor=FF3E00
[Svelte-url]: https://svelte.dev/
[Laravel.com]: https://img.shields.io/badge/Laravel-FF2D20?style=for-the-badge&logo=laravel&logoColor=white
[Laravel-url]: https://laravel.com
[Bootstrap.com]: https://img.shields.io/badge/Bootstrap-563D7C?style=for-the-badge&logo=bootstrap&logoColor=white
[Bootstrap-url]: https://getbootstrap.com
[JQuery.com]: https://img.shields.io/badge/jQuery-0769AD?style=for-the-badge&logo=jquery&logoColor=white
[JQuery-url]: https://jquery.com 


[contributors-shield]: https://img.shields.io/github/contributors/noFlowWater/signage_solution.svg?style=for-the-badge
[contributors-url]: https://github.com/noFlowWater/signage_solution/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/noFlowWater/signage_solution.svg?style=for-the-badge
[forks-url]: https://github.com/noFlowWater/signage_solution/network/members
[stars-shield]: https://img.shields.io/github/stars/noFlowWater/signage_solution.svg?style=for-the-badge
[stars-url]: https://github.com/noFlowWater/signage_solution/stargazers
[issues-shield]: https://img.shields.io/github/issues/noFlowWater/signage_solution.svg?style=for-the-badge
[issues-url]: https://github.com/noFlowWater/signage_solution/issues
[license-shield]: https://img.shields.io/github/license/noFlowWater/signage_solution.svg?style=for-the-badge
[license-url]: https://github.com/noFlowWater/signage_solution/blob/master/LICENSE.txt

[React.js]: https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=000
[React-url]: https://reactjs.org/

[Bootstrap.com]: https://img.shields.io/badge/Bootstrap-563D7C?style=for-the-badge&logo=bootstrap&logoColor=white
[Bootstrap-url]: https://getbootstrap.com

[Figma]: https://img.shields.io/badge/Figma-F24E1E?style=for-the-badge&logo=figma&logoColor=fff
[Figma-url]: https://www.figma.com/

[Flask]: https://img.shields.io/badge/Flask-000?style=for-the-badge&logo=flask&logoColor=fff
[Flask-url]: https://flask.palletsprojects.com/en/3.0.x/

[Nodejs]: https://img.shields.io/badge/Node.js-393?style=for-the-badge&logo=nodedotjs&logoColor=fff
[Nodejs-url]: https://nodejs.org/en

[Prisma]: https://img.shields.io/badge/Prisma-2D3748?style=for-the-badge&logo=prisma&logoColor=fff
[Prisma-url]: https://www.prisma.io/

[OpenCV]: https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=fff
[OpenCV-url]: https://opencv.org/

[Socket.io]: https://img.shields.io/badge/Socket.io-010101?style=for-the-badge&logo=socketdotio&logoColor=fff
[Socket.io-url]: https://socket.io/

[npm]: https://img.shields.io/badge/npm-CB3837?style=for-the-badge&logo=npm&logoColor=fff
[npm-url]: https://www.npmjs.com/

[MySQL]: https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=fff
[MySQL-url]: https://www.mysql.com/

[Python.org]: https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white
[Python-url]: https://www.python.org/

[JavaScript.js]: https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black
[JavaScript-url]: https://developer.mozilla.org/ko/docs/Learn/JavaScript

[LG]: https://img.shields.io/badge/webOS-A50034?style=for-the-badge&logo=lg&logoColor=fff
[LG-url]: https://www.webosose.org/

[Raspberry]: https://img.shields.io/badge/Raspberry%20Pi-A22846?style=for-the-badge&logo=raspberrypi&logoColor=fff
[Raspberry-url]: https://www.raspberrypi.com/

[macOS]: https://img.shields.io/badge/macOS-000?style=for-the-badge&logo=macOS&logoColor=fff
[macOS-url]: https://support.apple.com/ko-kr/macOS
