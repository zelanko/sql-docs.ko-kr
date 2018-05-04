---
title: '1 단계: pymssql Python 개발 환경 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: python
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8524f873adfb7a787285486f3a5fc04f1356a8fd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>1 단계: pymssql Python 개발에 대 한 개발 환경 구성
SQL Server에 대 한 Python 드라이버를 사용 하 여 응용 프로그램을 개발 하기 위해 필수 구성 요소 개발 환경을 구성 해야 합니다.    
  
Python SQL 드라이버는 SQL Server 및 Azure SQL 데이터베이스에서 기본적으로 사용 하도록 설정 하는 TDS 프로토콜을 사용 하는 참고 합니다.  추가적인 서버 구성은 필요하지 않습니다.  
  
## <a name="windows"></a>Windows  
  
1. **Python 런타임을 설치 하 고 pip 패키지 관리자**  
a. 로 이동 [python.org](https://www.python.org/downloads/)  
b. 적절 한 Windows installer msi 링크를 클릭 합니다.   
c. 한 번 다운로드 한 실행은 msi Python 런타임을 설치 하려면  
  
2. **Pymssql 모듈을 다운로드** 에서 [여기](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    올바른 whl 파일을 선택 하 고 있는지 확인 합니다.  예를 들어: Python 2.7을 사용 하는 64 비트 컴퓨터의 경우 선택: pymssql‑2.1.1‑cp27‑none‑win_amd64.whl 합니다. 다운로드 한 후.whl 파일에 배치할는 c: / Python27 폴더입니다.  
      
3. **Cmd.exe를 엽니다.**  
  
4. **Pymssql 모듈 설치**     
    예를 들어, 64 비트 컴퓨터에서 Python 2.7을 사용 하는 경우:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Python 런타임을 설치 하 고 패키지 관리자 pip** Ubuntu의 대부분의 배포판에 Python 미리 설치 되어 나오는 합니다.  컴퓨터에 설치 하는 python 얻을 수 있습니다 다운로드에서 소스 tarball [python.org](https://www.python.org/downloads/) 및 로컬에 작성 되거나 패키지 관리자를 사용할 수 있습니다.  
```  
> sudo apt-get install python   
```  
  
2.  **열기 터미널**  
  
3.  **Pymssql 모듈 및 종속성 설치**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **Python 런타임을 설치 하 고 pip 패키지 관리자**  
a. 로 이동 [python.org](https://www.python.org/downloads/)  
b. 적절 한 Mac installer pkg 링크를 클릭 합니다.   
c. 한 번 다운로드 한 실행 pkg Python 런타임을 설치 하려면  
  
2.  **열기 터미널**  
  
3. **Homebrew 패키지 관리자를 설치 합니다.**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **FreeTDS 모듈 설치**  
```  
> brew install FreeTDS  
```  
  
5.  **Pymssql 모듈 설치**  
```  
> sudo -H pip install pymssql  
```
