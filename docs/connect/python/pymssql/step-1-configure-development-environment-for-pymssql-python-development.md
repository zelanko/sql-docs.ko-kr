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
manager: jroth
ms.openlocfilehash: 9d74e3ce2f7db91aca295dcb7507431a82e49c8c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803870"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>1단계: pymssql Python 개발을 위한 개발 환경 구성
SQL Server 용 Python Driver를 사용 하 여 응용 프로그램을 개발 하기 위해 개발 환경 필수 구성 요소를 사용 하 여 구성 해야 합니다.    
  
Python SQL 드라이버 SQL Server 및 Azure SQL Database에서 기본적으로 사용 되는 TDS 프로토콜을 사용 하는 참고 합니다.  추가적인 서버 구성은 필요하지 않습니다.  
  
## <a name="windows"></a>Windows  
  
1. **Python 런타임을 설치 하 고 pip 패키지 관리자**  
1\. 로 [python.org](https://www.python.org/downloads/)  
2\. 적절 한 Windows installer msi 링크를 클릭 합니다.   
c. Python 런타임을 설치 msi 다운로드 한 번 실행  
  
2. **Pymssql 모듈을 다운로드** 에서 [여기](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    올바른 whl 파일을 선택 했는지 확인 하십시오.  예를 들어: 64 비트 컴퓨터에서 Python 2.7을 사용 하는 경우 선택: pymssql‑2.1.1‑cp27‑none‑win_amd64.whl 합니다. 다운로드 한 후 c:/python27 폴더에 넣습니다.whl 파일을 표시 합니다.  
      
3. **Cmd.exe를 열으십시오**  
  
4. **Pymssql 모듈 설치**     
    예를 들어, 64 비트 컴퓨터에서 Python 2.7을 사용 하는 경우:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Python 런타임을 설치 하 고 pip 패키지 관리자** Python는 Ubuntu의 대부분의 배포에 미리 설치 되어 제공 됩니다.  컴퓨터에 설치 된 python 없으면 가져올 수 있습니다 하거나 다운로드에서 원본 tarball [python.org](https://www.python.org/downloads/) 및 로컬에서 빌드 또는 패키지 관리자를 사용할 수 있습니다.  
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
  
1. **Python 런타임을 설치 하 고 pip 패키지 관리자**  
1\. 로 [python.org](https://www.python.org/downloads/)  
2\. 적절 한 Mac 설치 관리자 패키지 링크를 클릭 합니다.   
c. 한 번 다운로드 한 실행 Python 런타임을 설치 패키지  
  
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
