---
title: 유니코드 함수 인수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: eafe8c7e-f6d2-44d7-99ee-cf2148a30f4f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a25dd6fe0a77aad5c5ec9ba15eaf12bd2ec3fc18
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284293"
---
# <a name="unicode-function-arguments"></a>유니코드 함수 인수
ODBC 3.5(또는 그 이상) 드라이버 관리자는 인수에서 문자 문자열 또는 SQLPOINTER에 대한 포인터를 허용하는 모든 함수의 ANSI 및 유니코드 버전을 모두 지원합니다. 유니코드 함수는 매크로가 아닌 *W*접미사가 있는 함수로 구현됩니다. ANSI *함수(A의*접미사 유무에 관계없이 호출될 수 있음)는 현재 ODBC API 함수와 동일합니다.  
  
## <a name="remarks"></a>설명  
 항상 문자열 또는 길이 인수를 반환하거나 받는 유니코드 함수는 문자 수로 전달됩니다. 서버 데이터에 대한 길이 정보를 반환하는 함수의 경우 표시 크기와 정밀도가 문자 수에 설명되어 있습니다. 길이(데이터 전송 크기)가 문자열 또는 비문자열 데이터를 참조할 수 있는 경우 길이는 옥텟 길이로 설명됩니다. 예를 들어 **SQLGetInfoW는** 여전히 바이트 수로 길이를 사용하지만 **SQLExecDirectW는** 문자 수를 사용합니다.  
  
 문자 수는 ANSI 함수의 바이트 수(옥텟)와 UNICODE 함수의 WCHAR(16비트 단어) 수를 나타냅니다. 특히, 이중 바이트 문자 시퀀스(DBCS) 또는 다중 바이트 문자 시퀀스(MBCS)는 다중 바이트로 구성될 수 있다. UTF-16 유니코드 문자 시퀀스는 여러 WCHARs로 구성될 수 있습니다.  
  
 다음은 유니코드(W) 및 ANSI(A) 버전을 모두 지원하는 ODBC API 함수 목록입니다.  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagRec**|  
|**SQLColAttribute**|**SQLGetInfo**|  
|**SQLCol속성**|**SQLGetStmtAttr**|  
|**SQLColumnPrivileges**|**SQLGetTypeInfo**|  
|**SQLColumns**|**SQL네이티브SQL**|  
|**SQLConnect**|**SQLPrepare**|  
|**SQLDataSource**|**SQLPrimaryKeys**|  
|**SQLDescribeCol**|**SQLProcedureColumns**|  
|**SQLDriverConnect**|**SQLProcedures**|  
|**SQLDrivers**|**SQLSetConnectAttr**|  
|**SQL오류**|**SQLSet연결옵션**|  
|**SQLExecDirect**|**SQLSetCursorName**|  
|**SQLForeignKeys**|**SQLSetDescField**|  
|**SQLGetConnectAttr**|**SQLSetStmtAttr**|  
|**SQLGet연결 옵션**|**SQLSpecialColumns**|  
|**SQLGetCursorName**|**SQLStatistics**|  
|**SQLGetDescField**|**SQLTablePrivileges**|  
|**SQLGetDescRec**|**SQLTables**|  
|**SQLGetDiagField**||  
  
 다음은 유니코드(W) 및 ANSI(A) 버전을 모두 지원하는 ODBC 설치 프로그램 및 ODBC 번역기 함수 목록입니다.  
  
|||  
|-|-|  
|**SQLConfigDataSource**|**SQLInstallDriver관리자**|  
|**SQLCreate데이터 소스**|**SQLInstaller오류**|  
|**SQLDataSourceTo드라이버**|**SQLInstallODBC**|  
|**SQLDriverToData소스**|**SQLReadFileDSN**|  
|**SQLGet사용 가능한 드라이버**|**SQLRemoveDSNInI**|  
|**SQLGetInstalled드라이버**|**SQLValidDSN**|  
|**SQLGetTranslator**|**SQLWriteDSNToINI**|  
|**SQLInstallDriver**||  
  
> [!NOTE]
>  ODBC *3.x* 드라이버 관리자는 UNICODE **#define**ODBC *2.x* 응용 프로그램을 다시 컴파일할 수 있기 때문에 더 이상 사용되지 않은 함수에는 유니코드-ANSI 매핑 지원이 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [유니코드 애플리케이션](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [유니코드 드라이버](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [드라이버 관리자의 함수 매핑](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
