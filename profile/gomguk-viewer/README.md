# 곰국 뷰어
대학생들을 위한 논문 전용 PDF Viewer 입니다. 논문을 읽을 때 사용하는 여러 가지 툴들을 종합하여 제공하여 논문 읽기 경험을 개선하는 것을 목표로 두고 있습니다.

본 서비스는 제 6회 개방형 클라우드 플랫폼 기반 서비스 개발 아이디어 공모전 출품작입니다.

데모: https://gomguk.paas-ta.org/  

소개 PPT: [공모전 본선 발표](https://github.com/ssu-memorier/.github/blob/main/profile/gomguk-viewer/%EA%B3%B5%EB%AA%A8%EC%A0%84%20%EB%B3%B8%EC%84%A0%20%EB%B0%9C%ED%91%9C%20PPT.pdf)

소개 영상: [![소개 영상 유튜브](./thumbnail.png)](https://youtu.be/XwXoHRqTsb0)


## 왜 이것을 만드는가?
### 문제 인식
대학생활을 하다보면 논문을 읽어야할 때가 종종있습니다. 그리고 논문을 읽으며 다양한 문제와 마주하게되죠. 

우선 논문은 영어로 씌여있는 경우가 대부분입니다. 영어를 잘하는 사람들은 괜찮지만, 영어를 못하는 사람들에게 영어 해석은 지루하고 힘든 일일 것입니다. 또 논문을 단순히 읽기만 하진 않죠. 보통 중요한 내용을 요약하거나 다른 참고 자료들을 같이 보곤 합니다. 이를 위해 우리는 한 논문을 읽을 때도 메모장, 번역기, 논문 파일을 켜놓고 왔다갔다 하며 논문을 읽게됩니다. 내 컴퓨터에서 논문을 읽으며 정리한 내용을 다른 컴퓨터에서는 볼 수 없는 것도 불편사항입니다. 이를 위해선 파일을 옮길 별도의 방법을 사용해야만 합니다.

결국, 논문을 읽는 일은 복잡하고 피곤한 일이 됩니다.

### 유저 사전 인터뷰
저희가 발견한 논문 읽기의 문제점에 대해 실제 주변의 논문을 읽는 지인들은 어떻게 생각하는지 인터뷰를 해 보았습니다. 

인터뷰를 진행한 대학생 이모씨와 회사원 소모씨 모두 논문 읽기에 대해 피로감을 느끼고 있다고 했습니다. 

특히 한 화면에 여러 앱을 띄우고 사용해야 하는 상황에 대한 불편함과 환경이 바뀌었을 때 논문을 이어 읽기 위해 여러 파일들을 함께 클라우드 스토리지에 올려 관리해줘야 하는 점이 불편하다는 공감을 얻을 수 있었습니다.

### 솔루션
저희는 이렇게, 논문 읽기에 불편함을 겪고 있는 사람들이 있음을 발견했고, 이러한 불편함을 어떻게 개선할 수 있을지 고민하게 되었습니다.

먼저 "필요한 툴들을 이것 저것 띄우다 보니 화면이 너무 복잡하다" 라는 문제에 대해서 번역기, PDF 뷰어, 메모장 등을 동시에 사용 가능한 올인원 형태의 서비스를 제공함으로써 해결할 수 있을 것이라 생각했고,

또, "데스크탑에서 읽던 논문을 노트북에서 읽고 싶다" 라는 문제에 대해서는 클라우드 스토리지를 통해 어디서든 동일한 환경의 서비스를 제공함으로써 해결할 수 있을 것이라 생각했습니다.

이러한 솔루션들을 통해 전체적인 논문 읽기 경험을 개선할 수 있을 것이라 생각해 곰국 뷰어를 기획 & 개발하게 되었습니다.

## 무엇을 했는가?
![image](https://user-images.githubusercontent.com/40891497/210160025-bec1d986-5660-4776-ba26-1c79a2ffb937.png)

저희 곰국 뷰어는 다음과 같은 서비스들을 제공합니다.

첫째로, PDF 뷰어입니다.
웹사이트 내에서 뷰어를 제공해 논문을 읽을 수 있게 해줍니다.

둘째로, 메모장입니다.
논문을 읽다가 중요한 내용을 기록하고 싶다면 그때그때 메모장에 기록을 남길 수 있습니다. 

셋째로, 번역기입니다.
이해가 어려운 원문을 번역하고 뜻을 확인할 수 있습니다.

마지막으로 클라우드 스토리지입니다.
클라우드 스토리지를 제공하여 논문과 메모를 함께 저장하고 관리할 수 있습니다.

## 어떻게 했는가?

### 아키텍처
![image](https://user-images.githubusercontent.com/40891497/210160097-08d2b3cf-d03b-410e-a958-4d96f71bc752.png)
저희는 다양한 종류의 기능을 제공하기 때문에 유연한 확장이 가능하고 서비스 단위로 배포할 수 있는 마이크로 서비스 아키텍처를 채택했습니다. 

저희 서비스는 웹사이트를 호스팅하고 로그인 기능을 제공하기 위한 **웹 & 인증 서버**, 논문 파일에 대한 CRUD를 수행할 수 있는 **스토리지 서버**, 번역 서비스를 제공하는 **번역 서버**. 세 가지의 서버로 구성되고, 각 서버는 컨테이너 방식으로 파스타 클라우드 환경에 배포되어 운영됩니다.

스토리지의 경우 파스타에서 제공하지 않기 때문에 AWS S3를 이용했습니다.

유저 인증은 OAuth를 통해 유저 편의성과 보안성을 높였습니다.

또한 각 서비스는 토큰을 통해서 인가된 유저만 접근할 수 있도록 하였습니다. 

### 기술 스택
![image](https://user-images.githubusercontent.com/40891497/210160125-50094ed7-4e3a-4643-bbee-66d315b4bb5e.png)
클라이언트는 타입스크립트와 Vue.js 프레임워크를 사용했고, 메모장은 Editor.js, PDF 뷰어는 pdf.js 라이브러리를 활용했습니다.

번역 서비스와 스토리지 서비스는 Django 프레임워크를 사용했고, 웹 & 인증 서비스는 node.js, express 프레임워크를 사용했습니다. 데이터베이스는 MariaDB를 사용합니다.

번역은 Google Trans API를 사용하며, 스토리지는 AWS S3를 사용합니다. OAuth는 카카오와 구글 두 종류의 Provider를 제공합니다. 

코드 저장소는 Github, 컨테이너 배포 & 관리에는 클라우드 파운더리를 사용합니다. 

## 기대 효과

### 피로감 해소
여러가지 툴을 켜놓고 논문을 읽어야 했던 기존의 논문 읽기 경험을 개선해 유저들이 겪고 있던 어려움을 해결할 수 있을 것이라 생각합니다.

### 통합 환경 제공
클라우드를 통해서 이곳 저곳에 흩어져 있던 논문 파일들을 한 곳에 모으고 손쉽게 관리할 수 있는 통합 환경을 제공할 수 있을 것이라 생각합니다.

## FE 링크
### gomguk-viewer-fe  
곰국 뷰어의 클라이언트 영역에 대한 레포입니다.   
https://github.com/ssu-memorier/gomguk-viewer-fe  

## BE 링크
### gomguk_webserver  
곰국 뷰어의 웹 호스팅 서비스 & 인증 서비스를 위한 레포입니다.    
https://github.com/ssu-memorier/gomguk_webserver  

### S3-RestAPI  
곰국 뷰어의 스토리지 서비스 레포입니다.  
https://github.com/ssu-memorier/S3-RestAPI  

### translate-api  
곰국 뷰어의 번역 서비스 레포입니다.  
https://github.com/ssu-memorier/translate-api  
