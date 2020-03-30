---
title: '1단계: pyodbc Python 개발 환경 구성 | Microsoft Docs'
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
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67992524"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>1단계: pyodbc Python 개발을 위한 개발 환경 구성

## <a name="windows"></a>Windows  
Windows에서 Python - pyodbc를 사용하여 SQL Database에 연결:
  
1. **Python 설치 프로그램을 다운로드합니다**.  
  컴퓨터에 Python이 없는 경우 Python을 설치합니다. [Python 다운로드 페이지](https://www.python.org/downloads/windows/)로 이동하여 적절한 설치 프로그램을 다운로드합니다. 예를 들어 64비트 컴퓨터에서는 Python 2.7 또는 3.7(x64) 설치 프로그램을 다운로드합니다.  
  
2. **Python을 설치합니다**.  설치 프로그램을 다운로드한 후 다음을 수행합니다. a. 파일을 두 번 클릭하여 설치 프로그램을 시작합니다. b. 언어를 선택하고 약관에 동의합니다. 다. 화면의 지시에 따라 컴퓨터에 Python을 설치합니다. d. `C:\Python27` 또는 `C:\Python37`로 이동하여 Python이 설치되었는지 확인하고 `python -V` 또는 `py -V`를 실행합니다(3.x의 경우). 
      
3. [**Windows에 Microsoft ODBC Driver for SQL Server 설치**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **관리자 권한으로 cmd.exe를 엽니다.**     

5. **pip - Python 패키지 관리자를 사용하여 pyodbc를 설치합니다**(`C:\Python27\Scripts`를 Python 설치 경로로 바꿈).
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Python - pyodbc를 사용하여 SQL Database에 연결:
  
1. **터미널 열기**  

2. [**Linux에 Microsoft ODBC Driver for SQL Server 설치**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **pyodbc 설치**  
```  
> sudo -H pip install pyodbc
```
