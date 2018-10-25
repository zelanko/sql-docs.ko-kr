---
title: '1단계: Ruby 개발을 위한 개발 환경 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1de9ce8b14dd164ac24ac1bb7098494dbc134bfa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47778261"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>1단계: Ruby 개발을 위한 개발 환경 구성
SQL Server 용 Ruby 드라이버를 사용 하 여 응용 프로그램을 개발 하기 위해 개발 환경 필수 구성 요소를 사용 하 여 구성 해야 합니다.    
  
Ruby 드라이버는 SQL Server 및 Azure SQL Database에 기본적으로 사용 되는 TDS 프로토콜을 참고 합니다.  추가적인 서버 구성은 필요하지 않습니다.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Ruby 설치 관리자 다운로드**  
컴퓨터에 없으면 Ruby를 설치 하십시오. 새 ruby 사용자에 대 한 Ruby 2.2.X 설치 관리자를 사용 하는 것이 좋습니다. 안정적인 언어와 호환 되 고 업데이트 된 패키지 (보석)의 광범위 한 목록을 제공 합니다. 이동 합니다 [Ruby 다운로드 페이지](http://rubyinstaller.org/downloads/) 하 고 적절 한 2.1.x 설치 관리자를 다운로드 합니다. 예제를 64 비트 컴퓨터의 경우 다운로드 Ruby 2.1.6 (x64) 설치 관리자에 대 한 합니다.   
  
2.  **Ruby 설치**  
설치 관리자 다운로드 되 면 다음을 수행 합니다.  
1. 설치 관리자를 시작 하려면 파일을 두 번 클릭 합니다.  
2. 언어를 선택 하 고 약관에 동의 합니다.  
c.  설치 설정 화면에서이 Ruby 설치를 사용 하 여 경로 연결.rb 및.rbw 파일 모두 추가 Ruby 실행 파일 옆의 확인란을 선택 합니다.  
  
3.  **Ruby DevKit를 다운로드 합니다.**  
DevKit RubyInstaller 페이지에서 다운로드  
  
4.  **Ruby DevKit를 설치 합니다.**  
다운로드가 완료 되 면 다음을 수행 합니다.  
1. 파일을 두 번 클릭 합니다. 파일을 추출 하는 where를 라는 메시지가 나타납니다.  
2. "..." 단추를 클릭 하 고 "C:\DevKit"를 선택 합니다. "새 폴더 만들기"를 클릭 하 여이 폴더를 먼저 만들어야 아마도 해야 합니다.  
c. 파일을 추출 하려면 [확인]을 및 다음 추출""를 클릭 합니다.  
  
5. **Cmd.exe를 열으십시오**  
  
6. **Ruby DevKit를 초기화 합니다.**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **TinyTDS gem 설치**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **터미널 열기**  
  
2. **Ruby 버전 관리자 (rvm) 및 필수 구성 요소를 설치 합니다.**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **Rvm를 사용 하 여 Ruby 설치**  
예를 들어 버전 2.3.0 Ruby의 설치:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;버전 2.3.0를 실행 하는 마지막 명령의 출력에 표시 되는지 확인 합니다.  
  
4.  **FreeTDS를 설치 합니다.**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **TinyTDS 설치**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
Mac OS X에 이미 있다고 미리 설치 된 Ruby OS에 대 한 종속성을 참고 합니다.    
  
1.  **터미널 열기**  
  
2. **Homebrew 패키지 관리자 설치**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **FreeTDS를 설치 합니다.**  
```  
> brew install FreeTDS  
```  
  
4.  **TinyTDS gem 설치**  
```  
> gem install tiny_tds  
```
