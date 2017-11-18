---
title: "1 단계: Ruby 개발을 위한 개발 환경 구성 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ruby
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d722d1eed21162d5e076f5dfdfc3a2f18787f42e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>1 단계: Ruby 개발을 위한 개발 환경 구성
SQL Server에 대 한 Ruby 드라이버를 사용 하 여 응용 프로그램을 개발 하기 위해 필수 구성 요소 개발 환경을 구성 해야 합니다.    
  
Ruby 드라이버에서는 SQL Server 및 Azure SQL 데이터베이스에 기본적으로 사용 되는 TDS 프로토콜을 참고 합니다.  추가적인 서버 구성은 필요하지 않습니다.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Ruby 설치 관리자 다운로드**  
컴퓨터에 없으면 Ruby 소프트웨어를 설치 하십시오. 새 ruby 사용자에 대 한 Ruby 2.2. X 설치 관리자를 사용 하는 것이 좋습니다. 안정적인 언어와 호환 되며 업데이트 된 패키지 (gems)의 광범위 한 목록을 제공 합니다. 이동 된 [Ruby 다운로드 페이지](http://rubyinstaller.org/downloads/) 적절 한 2.1. x 설치 관리자를 다운로드 하 고 있습니다. 예제는 64 비트 컴퓨터에 있는 다운로드 Ruby 2.1.6 (x64) 설치 관리자에 대 한 합니다.   
  
2.  **Ruby를 설치 합니다.**  
설치 관리자를 다운로드 한 후 다음을 수행 합니다.  
a. 설치 프로그램을 시작 하려면 파일을 두 번 클릭 합니다.  
b. 언어를 선택 하 고 약관에 동의 합니다.  
c.  설치 설정 화면에서이 Ruby 설치 경로 연결.rb 및.rbw 파일에 모두 추가 Ruby 실행 파일 옆의 확인란을 선택 합니다.  
  
3.  **Ruby 하세요 다운로드**  
하세요 RubyInstaller 페이지에서 다운로드  
  
4.  **Ruby 하세요 설치**  
다운로드가 완료 되 면 다음을 수행 합니다.  
a. 파일을 두 번 클릭 합니다. 파일을 추출 하는 위치를 묻는 나타납니다.  
b. "..." 단추를 클릭 하 고 "C:\DevKit"를 선택 합니다. "새 폴더 만들기"를 클릭 하 여이 폴더를 먼저 만들 해야 합니다.  
c. 파일을 추출 하려면 "확인" 및 "추출를 선택 후"를 클릭 합니다.  
  
5. **Cmd.exe를 엽니다.**  
  
6. **Ruby 하세요를 초기화 합니다.**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **TinyTDS 보석 설치**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **열기 터미널**  
  
2. **Ruby 버전 관리자 (rvm) 및 필수 구성 요소 설치**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **Rvm를 사용 하 여 Ruby를 설치 합니다.**  
예를 들어 Ruby의 2.3.0 버전을 설치 합니다.  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;마지막 명령의 출력에 2.3.0 버전을 실행 하는 표시 되는지 확인 합니다.  
  
4.  **FreeTDS 설치**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **TinyTDS 설치**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
Mac OS X에 이미 있다고 Ruby 미리 설치 된 운영 체제에 종속성을 참고 합니다.    
  
1.  **열기 터미널**  
  
2. **Homebrew 패키지 관리자를 설치 합니다.**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **FreeTDS 설치**  
```  
> brew install FreeTDS  
```  
  
4.  **TinyTDS 보석 설치**  
```  
> gem install tiny_tds  
```

