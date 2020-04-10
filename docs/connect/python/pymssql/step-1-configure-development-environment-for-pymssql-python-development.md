---
title: '1단계: pymssql Python 개발 환경 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3310f268bf04b015c5f80cd08b2ae3909fd3a5c2
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926810"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>1단계: pymssql Python 개발을 위한 개발 환경 구성
SQL Server용 Python 드라이버로 애플리케이션을 개발하려면 개발 환경을 필수 구성 요소로 구성해야 합니다.    
  
Python SQL 드라이버는 SQL Server와 Azure SQL Database에서 기본적으로 사용 설정되는 TDS 프로토콜을 사용합니다.  추가적인 서버 구성은 필요하지 않습니다.  
  
## <a name="windows"></a>Windows  
  
1. **Python 런타임 및 pip 패키지 관리자 설치**  
a. [python.org](https://www.python.org/downloads/)로 이동합니다.  
b. 적절한 Windows Installer msi 링크를 클릭합니다.   
다. 다운로드되면 msi를 실행하여 Python 런타임을 설치합니다.  
  
2. [여기](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)에서 **pymssql 모듈을 다운로드**합니다.  
  
    올바른 whl 파일을 선택했는지 확인합니다.  예: 64비트 컴퓨터에서 Python 2.7을 사용하는 경우 pymssql‑2.1.1‑cp27‑none‑win_amd64.whl을 선택합니다. .whl 파일을 다운로드한 후 C:/Python27 폴더에 넣습니다.  
      
3. **cmd.exe 열기**  
  
4. **Pymssql 모듈 설치**     
    예를 들어 64비트 컴퓨터에서 Python 2.7을 사용하는 경우:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Python 런타임 및 pip 패키지 관리자 설치** Python은 대부분의 Ubuntu 배포판에 사전 설치되어 있습니다.  컴퓨터에 Python이 설치되어 있지 않은 경우 [python.org](https://www.python.org/downloads/)에서 소스 tarball을 다운로드하여 로컬로 빌드하거나 패키지 관리자를 사용할 수 있습니다.  
```  
> sudo apt-get install python   
```  
  
2.  **터미널 열기**  
  
3.  **Pymssql 모듈 및 종속성 설치**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **Python 런타임 및 pip 패키지 관리자 설치**  
a. [python.org](https://www.python.org/downloads/)로 이동합니다.  
b. 적절한 Mac 설치 프로그램 pkg 링크를 클릭합니다.   
다. 다운로드되면 pkg를 실행하여 Python 런타임을 설치합니다.  
  
2.  **터미널 열기**  
  
3. **Homebrew 패키지 관리자 설치**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **FreeTDS 모듈 설치**  
```  
> brew install FreeTDS  
```  
  
5.  **pymssql 모듈 설치**  
```  
> sudo -H pip install pymssql  
```
