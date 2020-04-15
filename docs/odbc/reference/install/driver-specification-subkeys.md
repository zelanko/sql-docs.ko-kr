---
title: 드라이버 사양 하위 키 | 마이크로 소프트 문서
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
ms.openlocfilehash: 47aa75f647e5fd8a88168611a3b21284962c70a4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280583"
---
# <a name="driver-specification-subkeys"></a>드라이버 사양 하위 키
ODBC 드라이버 하위 키에 나열된 각 드라이버에는 자체 하위 키가 있습니다. 이 하위 키의 이름은 ODBC 드라이버 하위 키 아래의 해당 값과 동일합니다. 이 하위 키 아래의 값에는 드라이버 및 드라이버 설정 DLL의 전체 경로, **SQLDriver에서**반환된 드라이버 키워드의 값 및 사용 수가 나열됩니다. 값의 형식은 다음 표에 나와 있습니다.  
  
|속성|데이터 형식|데이터|  
|----------|---------------|----------|  
|API 레벨|REG_SZ|**0** &#124; **1** &#124; **2**|  
|커넥트 기능|REG_SZ|{**Y**&#124;**N**}{**Y**&#124;**N**}{**Y**&#124;**N**}|  
|만들기DSN|REG_SZ|*드라이버 설명*|  
|드라이버|REG_SZ|*드라이버 DLL 경로*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|파일 익스트른|REG_SZ|**\*.** *파일 확장1*[**\*.** *파일 확장자2*] ...|  
|파일 사용|REG_SZ|**0** &#124; **1** &#124; **2**|  
|설치 프로그램|REG_SZ|*설정 DLL 경로*|  
|SQL수준|REG_SZ|**0** &#124; **1** &#124; **2**|  
|사용량 계산|REG_DWORD|*count*|  
  
 각 키워드의 사용은 다음 표에 나와 있습니다.  
  
|키워드|사용|  
|-------------|-----------|  
|**API 레벨**|드라이버에서 지원하는 ODBC 인터페이스 적합성 수준을 나타내는 숫자:<br /><br /> 0 = 없음<br /><br /> 1 = 레벨 1 지원<br /><br /> 2 = 레벨 2 지원<br /><br /> **SQLGetInfo**에서 SQL_ODBC_INTERFACE_CONFORMANCE 옵션에 대해 반환된 값과 같아야 합니다.|  
|**만들기DSN**|드라이버를 설치할 때 만들 하나 이상의 데이터 원본의 이름입니다. 시스템 정보에는 **CreateDSN** 키워드로 나열된 각 데이터 원본에 대해 하나의 데이터 원본 사양 섹션이 포함되어야 합니다. 이러한 섹션에는 드라이버 사양 섹션에 지정되어 있으므로 **드라이버** 키워드를 포함하지 않아야 하지만 대화 상자를 표시하지 않고 데이터 원본 사양을 만들 수 있도록 드라이버 설정 DLL에 **ConfigDSN** 함수에 대한 충분한 정보가 포함되어야 합니다. 데이터 원본 사양 섹션의 형식은 [데이터 원본 사양 하위 키를](../../../odbc/reference/install/data-source-specification-subkeys.md)참조하십시오.|  
|**커넥트 기능**|드라이버가 **SQLConnect,** **SQLDriverConnect**및 **SQLBrowseConnect를**지원하는지 여부를 나타내는 세 문자 문자열입니다. 드라이버가 **SQLConnect를**지원하는 경우 첫 번째 문자는 "Y"입니다. 그렇지 않으면 "N"입니다. 드라이버가 **SQLDriverConnect를**지원하는 경우 두 번째 문자는 "Y"입니다. 그렇지 않으면 "N"입니다. 드라이버가 **SQLBrowseConnect를**지원하는 경우 세 번째 문자는 "Y"입니다. 그렇지 않으면 "N"입니다. 예를 들어 드라이버가 **SQLConnect** 및 **SQLDriverConnect를** 지원하지만 **SQLBrowseConnect가**아닌 경우 세 문자 문자열은 "YYN"입니다.|  
|**DriverODBCVer**|드라이버가 지원하는 ODBC 버전이 있는 문자열입니다. 버전은 *nn.nn*양식으로, 처음 두 자리는 주 버전이고 다음 두 자리는 부 버전입니다. 이 설명서에 설명된 ODBC 버전의 경우 드라이버는 "03.00"을 반환해야 합니다.<br /><br /> 이 값은 **SQLGetInfo**에서 SQL_DRIVER_ODBC_VER 옵션에 대해 반환된 값과 같아야 합니다.|  
|**파일 익스트른**|파일 기반 드라이버의 경우 드라이버가 사용할 수 있는 파일의 쉼표로 구분된 확장자 목록입니다. 예를 들어 dBASE 드라이버는 \*.dbf를 지정할 수 있으며 \*서식이 지정된\*텍스트 파일 드라이버는 .txt, .csv를 지정할 수 있습니다. 응용 프로그램에서 이 정보를 사용하는 방법에 대한 예는 **FileUsage** 키워드를 참조하십시오.|  
|**파일 사용**|파일 기반 드라이버가 데이터 원본의 파일을 직접 처리하는 방법을 나타내는 숫자입니다.<br /><br /> 0 = 드라이버가 파일 기반 드라이버가 아닙니다. 예를 들어 ORACLE 드라이버는 DBMS 기반 드라이버입니다.<br /><br /> 1 = 파일 기반 드라이버는 데이터 원본의 파일을 테이블로 처리합니다. 예를 들어 Xbase 드라이버는 각 Xbase 파일을 테이블로 처리합니다.<br /><br /> 2 = 파일 기반 드라이버는 데이터 원본의 파일을 카탈로그로 처리합니다. 예를 들어 Microsoft® 액세스 드라이버는 각 Microsoft Access 파일을 전체 데이터베이스로 처리합니다.<br /><br /> 응용 프로그램은 사용자가 데이터를 선택하는 방법을 결정하기 위해 이 옵션을 사용할 수 있습니다. 예를 들어 Xbase 및 역설 사용자는 종종 데이터를 파일에 저장된 것으로 생각하지만 ORACLE 및 Microsoft Access 사용자는 일반적으로 데이터를 테이블에 저장된 것으로 간주합니다.<br /><br /> 사용자가 **파일** 메뉴에서 **데이터 파일 열기를** 선택하면 응용 프로그램에 **Windows 파일 열기** 공통 대화 상자가 표시될 수 있습니다. 파일 형식 목록은 **FileUsage** 값 1과 "Y"를 **ConnectFunctions** 키워드 값의 두 번째 문자로 지정하는 드라이버에 **대해 FileExtns** 키워드로 지정된 파일 확장자를 사용합니다. 사용자가 파일을 선택한 후 응용 프로그램은 **DRIVER** 키워드로 **SQLDriverConnect를** 호출한 다음 ** \* SELECT FROM *테이블 이름* ** 문을 실행합니다.<br /><br /> 사용자가 **파일** 메뉴에서 **데이터 가져오기를** 선택하면 응용 프로그램은 **FileUsage** 값을 0 또는 2로 지정하는 드라이버에 대한 설명 목록을 표시하고 **ConnectFunctions** 키워드 값의 두 번째 문자로 "Y"를 표시할 수 있습니다. 사용자가 드라이버를 선택한 후 응용 프로그램은 **DRIVER** 키워드를 사용 하 여 **SQLDriverConnect를** 호출 하 고 사용자 지정 **테이블 선택** 대화 상자를 표시 합니다.|  
|**SQL수준**|드라이버에서 지원하는 SQL-92 문법을 나타내는 숫자:<br /><br /> 0 = SQL-92 항목<br /><br /> 1 = FIPS127-2 과도기<br /><br /> 2 = SQL-92 중급<br /><br /> 3 = SQL-92 전체<br /><br /> 이 값은 **SQLGetInfo**에서 SQL_SQL_CONFORMANCE 옵션에 대해 반환된 값과 같아야 합니다.|  
  
 사용량 수에 대한 자세한 내용은 이 섹션의 앞에서 [사용 수를](../../../odbc/reference/install/usage-counting.md) 확인합니다.  
  
 응용 프로그램은 사용 수를 설정해서는 안 됩니다. ODBC는 이 수를 유지합니다.  
  
 예를 들어 서식이 지정된 텍스트 파일의 드라이버에 Text.dll이라는 드라이버 DLL, Txtsetup.dll이라는 별도의 드라이버 설정 DLL이 있고 세 번 설치되었다고 가정합니다. 드라이버가 수준 1 API 준수 수준을 지원하고 최소 SQL 문법 준수 수준을 지원하고 파일을 테이블로 처리하고 .txt 및 .csv 확장자를 사용하는 파일을 사용할 수 있는 경우 Text 하위 키 아래의 값은 다음과 같습니다.  
  
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
