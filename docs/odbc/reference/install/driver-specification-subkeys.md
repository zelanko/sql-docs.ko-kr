---
title: 드라이버 사양 하위 키 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], driver specification subkeys
- driver specification subkeys [ODBC]
- registry entries for components [ODBC], driver specification subkeys
- drivers subkey [ODBC]
ms.assetid: b4d802ef-b199-4e64-b7a5-6f2b3e5e2c80
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a10a3036e049a85e44c59ad8c8fa5a09bff538be
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="driver-specification-subkeys"></a>드라이버 사양 하위 키
ODBC 드라이버 하위 키에 나열 된 각 드라이버에는 자체의 하위 키를 있습니다. 이 하위 키는 ODBC 드라이버 하위 키 아래에서 해당 값으로 동일한 이름을 있습니다. 드라이버 및 드라이버 설치 Dll 반환한 드라이버 키워드 값의 전체 경로 나열 하는 값이 하위이 키 아래 **SQLDrivers**, 사용 횟수입니다. 다음 표에 표시 된은 값의 형식입니다.  
  
|이름|데이터 형식|Data|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&AMP;#124;**N**} {**Y**&AMP;#124;**N**} {**Y**&AMP;#124;**N**}|  
|CreateDSN|REG_SZ|*드라이버 설명*|  
|드라이버|REG_SZ|*드라이버 DLL 경로*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|FileExtns|REG_SZ|**\*.** *파일 extension1*[**,\*합니다.** *파일 extension2*]...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|설치 프로그램|REG_SZ|*설치 프로그램 DLL 경로*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*count*|  
  
 각 키워드의 사용은 다음 표에 표시 됩니다.  
  
|키워드|사용법|  
|-------------|-----------|  
|**APILevel**|ODBC를 나타내는 숫자 인터페이스는 드라이버에서 지 원하는 규칙 수준:<br /><br /> 0 = 없음<br /><br /> 1 = 수준 1 지원<br /><br /> 2 = 지원 수준 2<br /><br /> SQL_ODBC_INTERFACE_CONFORMANCE 옵션에 대 한 반환 값과 동일 하 게이 해야 **SQLGetInfo**합니다.|  
|**CreateDSN**|드라이버를 설치할 때 만들 하나 이상의 데이터 원본의 이름입니다. 시스템 정보와 함께 나열 된 각 데이터 원본에 대 한 데이터 원본 사양 섹션에 포함 해야 합니다는 **CreateDSN** 키워드입니다. 이 섹션에서는 포함 되지 않습니다는 **드라이버** 키워드에이 드라이버 사양 섹션에 지정 되어 있지만 충분 한 정보를 포함 해야 하기 때문에 **ConfigDSN** 드라이버에서 함수 데이터 원본 지정 대화 상자를 표시 하지 않고 만들려고 DLL을 설치 합니다. 데이터 원본 사양 섹션의 형식에 대 한 참조 [데이터 원본에 대 한 사양 하위 키](../../../odbc/reference/install/data-source-specification-subkeys.md)합니다.|  
|**ConnectFunctions**|드라이버를 지원 하는지를 나타내는 3 자 문자열 **SQLConnect**, **SQLDriverConnect**, 및 **SQLBrowseConnect**합니다. 드라이버에서 지 원하는 경우 **SQLConnect**, 첫 번째 문자는 "Y" 이며, 그렇지 않으면 "N"입니다. 드라이버에서 지 원하는 경우 **SQLDriverConnect**, 두 번째 문자는 "Y" 이며, 그렇지 않으면 "N"입니다. 드라이버에서 지 원하는 경우 **SQLBrowseConnect**, 세 번째 문자는 "Y" 이며, 그렇지 않으면 "N"입니다. 예를 들어, 드라이버를 지 원하는 경우 **SQLConnect** 및 **SQLDriverConnect** 아닌 **SQLBrowseConnect**, 3 자리 문자열은 "YYN"입니다.|  
|**DriverODBCVer**|ODBC 드라이버에서 지 원하는 버전으로 문자 문자열입니다. 폼의 버전은 *nn.nn*, 여기서 첫 두 자리는 주 버전 및 다음 두 자리는 부 버전. 이 설명서에 설명 된 ODBC 버전에서는 드라이버 "03.00" 반환 해야 합니다.<br /><br /> SQL_DRIVER_ODBC_VER 옵션에 대 한 반환 값과 동일 하 게이 해야 **SQLGetInfo**합니다.|  
|**FileExtns**|파일 기반 드라이버 쉼표로 구분 된 목록이 있는 파일의 확장명 드라이버 사용할 수 있습니다. 예를 들어 dBASE 드라이버 지정 \*.dbf 및 서식 있는 텍스트 파일 드라이버 지정할 수 있습니다 \*.txt,\*.csv입니다. 응용 프로그램 수이 정보를 사용 하는 방법의 예제를 보려면는 **FileUsage** 키워드입니다.|  
|**FileUsage**|파일 기반 드라이버 파일을 데이터 원본에서 직접 처리 하는 방법을 나타내는 수입니다.<br /><br /> 0 = 드라이버 파일 기반 드라이버 아닙니다. 예를 들어 ORACLE 드라이버는 DBMS 기반 드라이버.<br /><br /> 1 = 테이블로 데이터 소스에서 파일 기반 드라이버 처리 파일. 예를 들어 Xbase 드라이버 각 Xbase 파일을 테이블로 처리합니다.<br /><br /> 2 = 카탈로그로 데이터 원본에 파일 기반 드라이버 처리 파일. 예를 들어 Microsoft® Access 드라이버는 전체 데이터베이스를 각 Microsoft Access 파일을 처리합니다.<br /><br /> 응용 프로그램 사용자는 데이터를 선택 하는 방법을 확인 하려면이 사용할 수 있습니다. 예를 들어 Xbase 및 Paradox 사용자는 종종 ORACLE 및 Microsoft Access 사용자가 일반적으로 생각 하는 데이터 테이블에 저장 하는 동안 파일에 저장 되어 있는 데이터 인지 있습니다.<br /><br /> 사용자가 선택할 때 **데이터 파일 열기** 에서 **파일** 메뉴에서 응용 프로그램 표시할 수는 **Windows 파일 열기** 일반 대화 상자. 파일 형식 목록으로 지정 된 파일 확장명을 사용 합니다는 **FileExtns** 지정 하는 드라이버에 대 한 키워드는 **FileUsage** 값 1 및 "Y"의 값의 두 번째 문자는  **ConnectFunctions** 키워드입니다. 사용자가 파일을 선택 후 응용 프로그램을 호출 하는 **SQLDriverConnect** 와 **드라이버** 키워드 다음를 실행 한 **선택 \* FROM *테이블 이름***   문.<br /><br /> 사용자가 선택할 때 **데이터 가져오기** 에서 **파일** 메뉴에서 응용 프로그램에 지정 하는 드라이버에 대 한 설명 목록을 표시할 수는 **FileUsage** 0 또는 2, "Y"의 값 값의 두 번째 문자는 **ConnectFunctions** 키워드입니다. 사용자가 드라이버를 선택 후 응용 프로그램을 호출 하는 **SQLDriverConnect** 와 **드라이버** 키워드와 다음 디스플레이 사용자 지정 **테이블 선택** 대화 상자.|  
|**SQLLevel**|드라이버에서 지 원하는 SQL 92 문법을 나타내는 숫자:<br /><br /> 0 = SQL 92 항목<br /><br /> 1 = 전환 FIPS127 2<br /><br /> 2 = SQL 92 중간<br /><br /> 3 = sql-92 Full<br /><br /> SQL_SQL_CONFORMANCE 옵션에 대 한 반환 값과 동일 하 게이 해야 **SQLGetInfo**합니다.|  
  
 사용 횟수에 대 한 정보를 참조 하십시오. [사용 계산](../../../odbc/reference/install/usage-counting.md) 이 섹션의에서 앞부분입니다.  
  
 응용 프로그램 사용 횟수를 설정 해야 합니다. ODBC는이 개수를 유지 합니다.  
  
 예를 들어, 서식 있는 텍스트 파일에 대 한 드라이버는 드라이버 Text.dll 이라는 DLL을 가정해 보겠습니다 별도 드라이버 설치 DLL Txtsetup.dll, 명명 된 및 설치가 완료 된 후 3 번입니다. 드라이버에서는 수준 1 API 규칙 수준 지원 최소 SQL 문법을 규칙 수준,에서는 파일을 테이블로 처리 하며.txt 및.csv 확장명을 가진 파일을 사용할 수, 하는 경우 텍스트 하위 키 아래의 값 다음과 같을 수 있습니다.  
  
```  
APILevel : REG_SZ : 1  
ConnectFunctions : REG_SZ : YYN  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\TEXT.DLL  
DriverODBCVer : REG_SZ : 03.00.00  
FileExtns : REG_SZ : *.txt,*.csv  
FileUsage : REG_SZ : 1  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\TXTSETUP.DLL  
SQLLevel : REG_SZ : 0  
UsageCount : REG_DWORD : 0x3  
```
