---
title: '1 단계: pyodbc Python 개발 환경 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a1a43540d866faaf79b1c020eb255689862e6d97
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992524"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>1단계: pyodbc Python 개발을 위한 개발 환경 구성

## <a name="windows"></a>Windows  
Windows에서 Python-pyodbc를 사용 하 여 SQL Database에 연결 합니다.
  
1. **Python 설치 관리자를 다운로드**합니다.  
  컴퓨터에 Python이 없는 경우 설치 합니다. [Python 다운로드 페이지로](https://www.python.org/downloads/windows/) 이동 하 여 적절 한 설치 관리자를 다운로드 합니다. 예를 들어, 64 비트 컴퓨터의 경우 Python 2.7 또는 3.7 (x64) 설치 관리자를 다운로드 합니다.  
  
2. **Python을 설치합니다**.  설치 관리자를 다운로드 한 후에는 다음 단계를 수행 합니다. a. 파일을 두 번 클릭 하 여 설치 관리자를 시작 합니다. 2\. 언어를 선택 하 고 약관에 동의 합니다. c. 화면의 지시에 따라 컴퓨터에 Python을 설치 해야 합니다. d. 또는 `C:\Python27` (3`C:\Python37` . x의 경우)로 이동 하 여 Python이 설치 되었는지 확인할 수 있습니다. `python -V` `py -V` 
      
3. [**Windows에 Microsoft ODBC Driver for SQL Server 설치**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **관리자 권한으로 cmd.exe를 엽니다.**     

5. **Pip를 사용 하 여 Pyodbc 설치-Python 패키지 관리자** (를 `C:\Python27\Scripts` 설치 된 Python 경로로 바꿉니다.)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Python-pyodbc를 사용 하 여 SQL Database에 연결 합니다.
  
1. **터미널 열기**  

2. [**Linux에 Microsoft ODBC Driver for SQL Server 설치**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **Pyodbc 설치**  
```  
> sudo -H pip install pyodbc
```
