---
title: '1 단계: pymssql Python 개발 환경 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5bf2942b79cf7e72efbb36a53019de8208cd3b8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935822"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>1단계: pymssql Python 개발을 위한 개발 환경 구성
SQL Server 용 Python 드라이버를 사용 하 여 응용 프로그램을 개발 하려면 필수 구성 요소를 사용 하 여 개발 환경을 구성 해야 합니다.    
  
Python SQL 드라이버는 SQL Server 및 Azure SQL Database에서 기본적으로 사용 되는 TDS 프로토콜을 사용 합니다.  추가적인 서버 구성은 필요하지 않습니다.  
  
## <a name="windows"></a>Windows  
  
1. **Python 런타임 및 pip 패키지 관리자 설치**  
1\. [Python.org](https://www.python.org/downloads/) 으로 이동  
2\. 적절 한 Windows installer msi 링크를 클릭 합니다.   
c. 다운로드 되 면 msi를 실행 하 여 Python 런타임을 설치 합니다.  
  
2. [여기](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql) 에서 **Pymssql 모듈을 다운로드** 합니다.  
  
    올바른 whl 파일을 선택 했는지 확인 합니다.  예: 64 비트 컴퓨터에서 Python 2.7를 사용 하는 경우 pymssql-2.1.1-cp27-none-win_amd64. . Whl 파일을 다운로드 한 후에는 C:/Python27.pdb 폴더에 넣습니다.  
      
3. **Cmd.exe를 엽니다.**  
  
4. **Pymssql 모듈 설치**     
    예를 들어 64 비트 컴퓨터에서 Python 2.7를 사용 하는 경우:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Python 런타임 및 pip 패키지 관리자 설치**  Python은 대부분의 Ubuntu 배포판에 미리 설치 되어 제공 됩니다.  컴퓨터에 python이 설치 되어 있지 않은 경우 [python.org](https://www.python.org/downloads/) 에서 원본 tarball를 다운로드 하 여 로컬로 빌드를 수행 하거나 패키지 관리자를 사용할 수 있습니다.  
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
1\. [Python.org](https://www.python.org/downloads/) 으로 이동  
2\. 적절 한 Mac 설치 관리자 pkg 링크를 클릭 합니다.   
c. 다운로드 되 면 pkg를 실행 하 여 Python 런타임을 설치 합니다.  
  
2.  **터미널 열기**  
  
3. **Homebrew 패키지 관리자 설치**  
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
