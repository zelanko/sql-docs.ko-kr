---
title: 유니코드 함수 인수 | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: eafe8c7e-f6d2-44d7-99ee-cf2148a30f4f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0b2e30db5cacd2266ee14ec847210d7ff8407b1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="unicode-function-arguments"></a>유니코드 함수 인수
ODBC 3.5 (또는 이상) 드라이버 관리자는 해당 인수에 문자열 또는 대 SQLPOINTER에 대 한 포인터를 허용 하는 모든 함수의 ANSI 및 유니코드 버전을 지원 합니다. 유니코드 함수 함수로 구현 됩니다 (의 접미사와 함께 *W*), 매크로로 하지 않습니다. ANSI 함수 (또는의 접미사 없이 호출할 수 있는 *A*)는 현재 ODBC API 함수에 동일 합니다.  
  
## <a name="remarks"></a>주의  
 문자열 또는 길이 인수를 사용 하거나 항상 반환 하는 유니코드 함수는 문자 수로 전달 됩니다. 서버 데이터에 대 한 길이 정보를 반환 하는 함수에 대 한 표시 크기 및 정밀도 문자 수에 설명 되어 있습니다. 길이 (데이터의 전송 크기) 문자열 또는 문자열이 아닌 데이터를 참조할 수, 하는 경우 8 진수 길이 길이 설명 합니다. 예를 들어 **SQLGetInfoW** 바이트 수로 길이 여전히 걸립니다 하지만 **SQLExecDirectW** 문자 개수를 사용 합니다.  
  
 문자 수 (8 진수) ANSI 함수에 대 한 바이트 수와 유니코드 함수에 대 한 WCHAR (16 비트 단어)의 수를 나타냅니다. 특히, 더블 바이트 문자 시퀀스 (DBCS) 또는 멀티 바이트 문자 시퀀스 (MBCS) 여러 바이트 구성 될 수 있습니다. U t F-16으로 유니코드 문자 시퀀스를 여러 WCHARs 구성 될 수 있습니다.  
  
 다음은 유니코드 (W) 및 ANSI (A) 모두 버전을 지 원하는 ODBC API 함수 목록입니다.  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagField**|  
|**SQLColAttribute**|**SQLGetDiagRec**|  
|**SQLColAttributes**|**SQLGetInfo**|  
|**SQLColumnPrivileges**|**SQLGetStmtAttr**|  
|**SQLColumns**|**SQLNativeSQL**|  
|**SQLConnect**|**SQLPrepare**|  
|**SQLDataSources**|**SQLPrimaryKeys**|  
|**SQLDescribeCol**|**SQLProcedureColumns**|  
|**SQLDriverConnect**|**SQLProcedures**|  
|**SQLDrivers**|**SQLSetConnectAttr**|  
|**SQLError**|**SQLSetConnectOption**|  
|**SQLExecDirect**|**SQLSetCursorName**|  
|**SQLForeignKeys**|**SQLSetDescField**|  
|**SQLGetConnectAttr**|**SQLSetStmtAttr**|  
|**SQLGetConnectOption**|**SQLSpecialColumns**|  
|**SQLGetCursorName**|**SQLStatistics**|  
|**SQLGetDescField**|**SQLTablePrivileges**|  
|**SQLGetDescRec**|**SQLTables**|  
  
 다음은 유니코드 (W) 및 ANSI (A) 모두 버전을 지 원하는 ODBC 설치 및 ODBC 변환기 함수 목록.  
  
|||  
|-|-|  
|**SQLConfigDataSource**|**SQLInstallDriverManager**|  
|**SQLCreateDataSource**|**SQLInstallerError**|  
|**SQLDataSourceToDriver**|**SQLInstallODBC**|  
|**SQLDriverToDataSource**|**SQLReadFileDSN**|  
|**SQLGetAvailableDrivers**|**SQLRemoveDSNFromINI**|  
|**SQLGetInstalledDrivers**|**SQLValidDSN**|  
|**SQLGetTranslator**|**SQLWriteDSNToINI**|  
|**SQLInstallDriver**||  
  
> [!NOTE]  
>  사용 되지 않는 함수는 유니코드에서 ANSI 매핑을 지원 하므로 ODBC 3*.x* 드라이버 관리자가 지 원하는 ODBC 2를 다시 컴파일하지. *x* 응용 프로그램에서 유니코드를 사용한 **#define**합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [유니코드 응용 프로그램](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [유니코드 드라이버](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [드라이버 관리자의 함수 매핑](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
