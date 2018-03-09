---
title: "1 단계: pyodbc Python 개발 환경 구성 | Microsoft Docs"
ms.custom: 
ms.date: 08/08/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: python
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
caps.latest.revision: "2"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 886cf420228b622fb9c269423ce9a71c2c25ecaa
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>1 단계: pyodbc Python 개발에 대 한 개발 환경 구성

## <a name="windows"></a>Windows  
Python-pyodbc Windows에서 사용 하 여 SQL 데이터베이스에 연결 합니다.
  
1. **Python 설치 관리자 다운로드**  
  컴퓨터에 없으면 Python 소프트웨어를 설치 하십시오. 이동 된 [Python 다운로드 페이지](https://www.python.org/downloads/windows/) 적절 한 설치 관리자를 다운로드 합니다. 예제는 64 비트 컴퓨터에 있는 다운로드 Python 2.7 또는 3.5 (x64) 설치 관리자에 대 한 합니다.  
  
2. **Python 설치** 설치 관리자를 다운로드 한 다음 실행:는 합니다. 설치 프로그램을 시작 하려면 파일을 두 번 클릭 합니다. b. 언어를 선택 하 고 약관에 동의 합니다. c. 화면의 지침에 따라 Python 컴퓨터에 설치 해야 합니다. d. Python C:\Python27 또는 C:\Python35로 이동 하 여 설치 되 고 python v 또는 py-v (3.x)를 실행 합니다. 즉 확인할 수 있습니다. 
      
3. [**Microsoft ODBC 드라이버 설치**](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)
  
4. **관리자 권한으로 cmd.exe를 엽니다.**     

5. **Pip-를 사용 하 여 pyodbc Python 패키지 관리자 설치**
```  
> cd C:\Python27\Scripts>  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Ubuntu 및 RedHat pyodbc-Python을 사용 하 여 SQL 데이터베이스에 연결:
  
1. **열기 터미널**  

2. **Microsoft ODBC Driver 13 for Linux 설치** Ubuntu 15.04 + 
``` 
> sudo su  
> wget https://gallery.technet.microsoft.com/ODBC-Driver-13-for-Ubuntu-b87369f0/file/154097/2/installodbc.sh  
> sh installodbc.sh  
```   

  RedHat 6,7에 대 한 
``` 
> sudo su 
> wget https://gallery.technet.microsoft.com/ODBC-Driver-13-for-SQL-8d067754/file/153653/4/install.sh 
> sh install.sh 
```  
  
3.  **Pyodbc 설치**  
```  
> sudo -H pip install pyodbc
```
