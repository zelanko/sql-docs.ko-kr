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
ms.openlocfilehash: 38af92d3cb0354bc4b75131a349f6a1c26e90490
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992465"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>1단계: Ruby 개발을 위한 개발 환경 구성
SQL Server 용 Ruby 드라이버를 사용 하 여 응용 프로그램을 개발 하려면 필수 구성 요소를 사용 하 여 개발 환경을 구성 해야 합니다.    
  
Ruby 드라이버는 SQL Server 및 Azure SQL Database에서 기본적으로 사용 되는 TDS 프로토콜을 사용 합니다.  추가적인 서버 구성은 필요하지 않습니다.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Ruby 설치 관리자 다운로드**  
컴퓨터에 Ruby가 없는 경우 설치 하세요. 새 ruby 사용자의 경우 Ruby 2.2. X 설치 관리자를 사용 하는 것이 좋습니다. 이러한 기능은 안정적인 언어와 호환 및 업데이트 되는 다양 한 패키지 목록 (보석)을 제공 합니다. [Ruby 다운로드 페이지로](https://rubyinstaller.org/downloads/) 이동 하 여 적절 한 2.1. x 설치 관리자를 다운로드 합니다. 예를 들어 64 비트 컴퓨터에 있는 경우 Ruby 2.1.6 (x64) 설치 관리자를 다운로드 합니다.   
  
2.  **Ruby 설치**  
설치 관리자를 다운로드 한 후 다음을 수행 합니다.  
1\. 파일을 두 번 클릭 하 여 설치 관리자를 시작 합니다.  
2\. 언어를 선택 하 고 약관에 동의 합니다.  
c.  설치 설정 화면에서 경로에 Ruby 실행 파일 추가 옆의 확인란을 선택 하 고이 Ruby 설치를 사용 하 여 rbw 파일을 연결 합니다.  
  
3.  **Ruby DevKit 다운로드**  
RubyInstaller 페이지에서 DevKit 다운로드  
  
4.  **Ruby DevKit 설치**  
다운로드가 완료 되 면 다음을 수행 합니다.  
1\. 파일을 두 번 클릭 합니다. 파일의 압축을 풀 위치를 묻는 메시지가 표시 됩니다.  
2\. "..."를 클릭 합니다. 단추를 선택 하 고 "C:\DevKit"를 선택 합니다. "새 폴더 만들기"를 클릭 하 여이 폴더를 먼저 만들어야 할 수도 있습니다.  
c. "확인"을 클릭 한 다음 "Extract"를 클릭 하 여 파일을 추출 합니다.  
  
5. **Cmd.exe를 엽니다.**  
  
6. **Ruby DevKit 초기화**  
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
  
1. **터미널 열기**  
  
2. **Rvm (Ruby 버전 관리자) 및 필수 구성 요소 설치**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **Rvm을 사용 하 여 Ruby 설치**  
예를 들어 Ruby의 2.3.0 버전을 설치 합니다.  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;마지막 명령의 출력에서 버전 2.3.0를 실행 하 고 있음을 확인 합니다.  
  
4.  **FreeTDS 설치**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **TinyTDS 설치**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
OS에 종속성이 있으므로 Mac OS X에 이미 Ruby가 설치 되어 있습니다.    
  
1.  **터미널 열기**  
  
2. **Homebrew 패키지 관리자 설치**  
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
