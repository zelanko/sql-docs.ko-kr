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
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67992465"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>1단계: Ruby 개발을 위한 개발 환경 구성
SQL Server용 Ruby 드라이버로 애플리케이션을 개발하려면 개발 환경을 필수 구성 요소로 구성해야 합니다.    
  
Ruby 드라이버는 SQL Server와 Azure SQL Database에서 기본적으로 사용 설정되는 TDS 프로토콜을 사용합니다.  추가적인 서버 구성은 필요하지 않습니다.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Ruby 설치 프로그램을 다운로드합니다.**  
컴퓨터에 Ruby가 없는 경우 설치합니다. 새 Ruby 사용자의 경우 Ruby 2.2.X 설치 프로그램을 사용하는 것이 좋습니다. 이러한 설치 프로그램은 안정적인 언어와 호환 및 업데이트되는 다양한 패키지(gem) 목록을 제공합니다. [Ruby 다운로드 페이지](https://rubyinstaller.org/downloads/)로 이동하여 해당하는 2.1.x 설치 프로그램을 다운로드합니다. 예를 들어 64비트 컴퓨터에서는 Ruby 2.1.6(x64) 설치 프로그램을 다운로드합니다.   
  
2.  **Ruby를 설치합니다.**  
설치 프로그램을 다운로드한 후 다음을 수행합니다.  
a. 파일을 두 번 클릭하여 설치 프로그램을 시작합니다.  
b. 언어를 선택하고 약관에 동의합니다.  
다.  설치 설정 화면에서 '경로에 Ruby 실행 파일 추가' 옆의 확인란과 '.rb 및 .rbw 파일을 이 Ruby 설치에 연결' 옆의 확인란을 모두 선택합니다.  
  
3.  **Ruby DevKit을 다운로드합니다.**  
RubyInstaller 페이지에서 DevKit를 다운로드합니다.  
  
4.  **Ruby DevKit을 설치합니다.**  
다운로드가 완료되면 다음을 수행합니다.  
a. 파일을 두 번 클릭합니다. 파일을 압축 해제할 위치를 묻는 메시지가 표시됩니다.  
b. "..." 단추를 클릭하고 "C:\DevKit"를 선택합니다. "새 폴더 만들기"를 클릭하여 이 폴더를 먼저 만들어야 할 수 있습니다.  
다. "확인"을 클릭한 다음 "압축 풀기"를 클릭하여 파일을 압축 해제합니다.  
  
5. **cmd.exe를 엽니다.**  
  
6. **Ruby DevKit를 초기화합니다.**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **TinyTDS gem을 설치합니다.**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **터미널을 엽니다.**  
  
2. **rvm(Ruby 버전 관리자) 및 필수 구성 요소를 설치합니다.**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **rvm을 사용하여 Ruby를 설치합니다.**  
예를 들어 Ruby의 2.3.0 버전을 설치합니다.  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;마지막 명령의 출력에서 버전 2.3.0이 실행되고 있는지 확인합니다.  
  
4.  **FreeTDS를 설치합니다.**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **TinyTDS를 설치합니다.**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
OS에 종속성이 있으므로 Mac OS X에 Ruby가 미리 설치되어 있습니다.    
  
1.  **터미널을 엽니다.**  
  
2. **Homebrew 패키지 관리자 설치**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **FreeTDS를 설치합니다.**  
```  
> brew install FreeTDS  
```  
  
4.  **TinyTDS gem을 설치합니다.**  
```  
> gem install tiny_tds  
```
