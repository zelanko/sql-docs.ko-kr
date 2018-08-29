---
title: '1 단계: pyodbc Python 개발 환경 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f588174ea80677066628cb3e756d7c38bd42fba
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2018
ms.locfileid: "42784496"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>1단계: pyodbc Python 개발을 위한 개발 환경 구성

## <a name="windows"></a>Windows  
Python – Windows에서 pyodbc를 사용 하 여 SQL Database에 연결 합니다.
  
1. **Python 설치 관리자 다운로드**합니다.  
  컴퓨터에 Python이 없는 경우 설치 합니다. 로 이동 합니다 [Python 다운로드 페이지](https://www.python.org/downloads/windows/) 하 고 적절 한 설치 관리자를 다운로드 합니다. 예를 들어, 64 비트 컴퓨터를 사용 하는 경우 Python 2.7 또는 3.7 (x64) 설치 관리자를 다운로드 합니다.  
  
2. **Python을 설치합니다**.  설치 관리자 다운로드 되 면 다음 단계를 수행 합니다:는 합니다. 설치 관리자를 시작 하려면 파일을 두 번 클릭 합니다. 2. 언어를 선택 하 고 약관에 동의 합니다. c. 화면의 지침을 따르고 컴퓨터에 Python을 설치 해야 합니다. d. Python으로 이동 하 여 설치 되어 있는지 확인할 수 있습니다 `C:\Python27` 나 `C:\Python37` 실행 하 고 `python -V` 또는 `py -V` (3.x)에 대 한 
      
3. [**Windows에 Microsoft ODBC Driver for SQL Server 설치**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **관리자 권한으로 cmd.exe를 엽니다.**     

5. **Pip-Python 패키지 관리자를 사용 하 여 pyodbc를 설치** (대체 `C:\Python27\Scripts` 설치 된 Python 경로 사용 하 여)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Python-pyodbc를 사용 하 여 SQL Database에 연결 합니다.
  
1. **터미널 열기**  

2. [**Linux에 Microsoft ODBC Driver for SQL Server 설치**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **Pyodbc를 설치 합니다.**  
```  
> sudo -H pip install pyodbc
```
