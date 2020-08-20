---
description: 드라이버 사양 하위 키
title: 드라이버 사양 하위 키 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], driver specification subkeys
- driver specification subkeys [ODBC]
- registry entries for components [ODBC], driver specification subkeys
- drivers subkey [ODBC]
ms.assetid: b4d802ef-b199-4e64-b7a5-6f2b3e5e2c80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a363335931723e33a6461b86395494153491d328
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499786"
---
# <a name="driver-specification-subkeys"></a>드라이버 사양 하위 키
ODBC Drivers 하위 키에 나열 된 각 드라이버에는 자체의 하위 키가 있습니다. 이 하위 키는 ODBC 드라이버 하위 키 아래에 있는 해당 값과 동일한 이름을 갖습니다. 이 하위 키의 값에는 드라이버 및 드라이버 설치 Dll의 전체 경로, **Sqldrivers**에서 반환 된 드라이버 키워드의 값 및 사용 횟수가 나열 됩니다. 값의 형식은 다음 표에 나와 있습니다.  
  
|Name|데이터 형식|데이터|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124;**n**} {**y**&#124;**n**} {**y**&#124;**n**}|  
|CreateDSN|REG_SZ|*드라이버-설명*|  
|드라이버|REG_SZ|*드라이버 DLL-경로*|  
|DriverODBCVer|REG_SZ|*nn. nn*|  
|FileExtns|REG_SZ|**\*.** *파일 extension1*[**, \* .** *파일-extension2*] ...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|설치 프로그램|REG_SZ|*설치 프로그램-DLL-경로*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*count*|  
  
 다음 표에서는 각 키워드를 사용 하는 방법을 보여 줍니다.  
  
|키워드|사용|  
|-------------|-----------|  
|**APILevel**|드라이버에서 지 원하는 ODBC 인터페이스 규칙 수준을 나타내는 숫자입니다.<br /><br /> 0 = 없음<br /><br /> 1 = 지원 되는 수준 1<br /><br /> 2 = 수준 2 지원 됨<br /><br /> 이 값은 **SQLGetInfo**의 SQL_ODBC_INTERFACE_CONFORMANCE 옵션에 대해 반환 되는 값과 동일 해야 합니다.|  
|**CreateDSN**|드라이버가 설치 될 때 생성 될 하나 이상의 데이터 원본 이름입니다. 시스템 정보는 **CreateDSN** 키워드를 사용 하 여 나열 된 각 데이터 원본에 대해 하나의 데이터 원본 사양 섹션을 포함 해야 합니다. 이러한 섹션은 드라이버 사양 섹션에 지정 되어 있지만, 모든 대화 상자를 표시 하지 않고 데이터 원본 사양을 만들기 위해 드라이버 설치 DLL의 **ConfigDSN** 함수에 대 한 충분 한 정보를 포함 해야 하기 때문에 **driver** 키워드를 포함 해서는 안 됩니다. 데이터 원본 사양 섹션의 형식은 [데이터 원본 사양 하위 키](../../../odbc/reference/install/data-source-specification-subkeys.md)를 참조 하세요.|  
|**ConnectFunctions**|드라이버에서 **SQLConnect**, **SQLDriverConnect**및 **SQLBrowseConnect**을 지원 하는지 여부를 나타내는 세 문자로 된 문자열입니다. 드라이버가 **SQLConnect**을 지 원하는 경우 첫 번째 문자는 "Y"입니다. 그렇지 않으면 "N"입니다. 드라이버가 **SQLDriverConnect**을 지 원하는 경우 두 번째 문자는 "Y"입니다. 그렇지 않으면 "N"입니다. 드라이버가 **SQLBrowseConnect**을 지 원하는 경우 세 번째 문자는 "Y"입니다. 그렇지 않으면 "N"입니다. 예를 들어 드라이버가 **SQLConnect** 및 **SQLDriverConnect** 를 지원 하지만 **SQLBrowseConnect**는 지원 하지 않는 경우 3 자 문자열은 "YYN"입니다.|  
|**DriverODBCVer**|드라이버가 지 원하는 ODBC 버전을 포함 하는 문자열입니다. 버전은 *nn. nn*형식입니다. 여기서 처음 두 자리는 주 버전이 고 다음 두 자리는 부 버전입니다. 이 설명서에 설명 된 ODBC 버전의 경우 드라이버에서 "03.00"을 반환 해야 합니다.<br /><br /> 이 값은 **SQLGetInfo**의 SQL_DRIVER_ODBC_VER 옵션에 대해 반환 되는 값과 동일 해야 합니다.|  
|**FileExtns**|파일 기반 드라이버의 경우 드라이버에서 사용할 수 있는 파일 확장명의 쉼표로 구분 된 목록입니다. 예를 들어 dBASE 드라이버는 .dbf를 지정 \* 하 고 형식이 지정 된 텍스트 파일 드라이버는 \* .txt, .csv를 지정할 \* 수 있습니다. 응용 프로그램에서이 정보를 사용 하는 방법에 대 한 예제는 **Fileusage** 키워드를 참조 하세요.|  
|**FileUsage**|파일 기반 드라이버에서 데이터 원본의 파일을 직접 처리 하는 방법을 나타내는 숫자입니다.<br /><br /> 0 = 드라이버가 파일 기반 드라이버가 아닙니다. 예를 들어 ORACLE 드라이버는 DBMS 기반 드라이버입니다.<br /><br /> 1 = 파일 기반 드라이버는 데이터 원본의 파일을 테이블로 처리 합니다. 예를 들어 Xbase 드라이버는 각 Xbase 파일을 테이블로 처리 합니다.<br /><br /> 2 = 파일 기반 드라이버는 데이터 원본의 파일을 카탈로그로 처리 합니다. 예를 들어 Microsoft® Access 드라이버는 각 Microsoft Access 파일을 전체 데이터베이스로 처리 합니다.<br /><br /> 응용 프로그램은이를 사용 하 여 사용자가 데이터를 선택 하는 방법을 결정할 수 있습니다. 예를 들어 Xbase 및 Paradox 사용자는 종종 데이터를 파일에 저장 된 것으로 생각 하는 반면, ORACLE 및 Microsoft Access 사용자는 일반적으로 데이터를 테이블에 저장 된 것으로 간주 합니다.<br /><br /> 사용자가 **파일** 메뉴에서 **데이터 파일 열기** 를 선택 하면 응용 프로그램에서 **Windows 파일 열기** 일반 대화 상자를 표시할 수 있습니다. 파일 형식 목록에는 **Fileextns** 키워드에 지정 된 파일 확장명을 사용 합니다 .이 파일은 **fileusage** 값을 1로 지정 하 고 "Y"는 **connectfunctions** 키워드 값의 두 번째 문자로 지정 합니다. 사용자가 파일을 선택 하면 응용 프로그램은 **DRIVER** 키워드를 사용 하 여 **SQLDriverConnect** 를 호출한 다음 **SELECT \* FROM *table-name* ** 문을 실행 합니다.<br /><br /> 사용자가 **파일** 메뉴에서 **데이터 가져오기** 를 선택 하면 응용 프로그램은 **fileusage** 값 0 또는 2를 지정 하는 드라이버에 대 한 설명 목록을 표시 하 고 **connectfunctions** 키워드 값의 두 번째 문자로 "Y"를 표시할 수 있습니다. 사용자가 드라이버를 선택 하면 응용 프로그램은 **driver** 키워드를 사용 하 여 **SQLDriverConnect** 를 호출한 다음 사용자 지정 **테이블 선택** 대화 상자를 표시 합니다.|  
|**SQLLevel**|드라이버에서 지 원하는 SQL-92 문법을 나타내는 숫자입니다.<br /><br /> 0 = SQL-92 항목<br /><br /> 1 = FIPS127 전환<br /><br /> 2 = SQL-92 중간<br /><br /> 3 = SQL-92 Full<br /><br /> 이 값은 **SQLGetInfo**의 SQL_SQL_CONFORMANCE 옵션에 대해 반환 되는 값과 동일 해야 합니다.|  
  
 사용 횟수에 대 한 자세한 내용은이 섹션의 앞부분에 나오는 [사용량 계산](../../../odbc/reference/install/usage-counting.md) 을 참조 하세요.  
  
 응용 프로그램은 사용 횟수를 설정 하면 안 됩니다. ODBC는이 수를 유지 합니다.  
  
 예를 들어 형식이 지정 된 텍스트 파일에 대 한 드라이버에 Text.dll 이라는 드라이버 DLL이 있고 Txtsetup.dll 라는 별도의 드라이버 설치 DLL이 있는 경우 3 번 설치 되어 있다고 가정 합니다. 드라이버가 수준 1 API 규칙 수준을 지원 하 고, 최소 SQL 문법 규칙 수준을 지원 하 고, 파일을 테이블로 처리 하 고, .txt 및 .csv 확장명을 가진 파일을 사용할 수 있는 경우 Text 하위 키 아래의 값은 다음과 같을 수 있습니다.  
  
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
