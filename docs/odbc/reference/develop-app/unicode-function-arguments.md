---
title: 유니코드 함수 인수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 88ce592ebbf5a1b44d55b1b3119ef96e713112bc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74833024"
---
# <a name="unicode-function-arguments"></a>유니코드 함수 인수
ODBC 3.5 이상 드라이버 관리자는 해당 인수에서 문자 문자열 또는 SQLPOINTER에 대 한 포인터를 허용 하는 모든 함수의 ANSI 및 유니코드 버전을 모두 지원 합니다. 유니코드 함수는 매크로가 아니라 함수 ( *W*접두사 포함)로 구현 됩니다. *의 접미사*를 사용 하거나 사용 하지 않고 호출할 수 있는 ANSI 함수는 현재 ODBC API 함수와 동일 합니다.  
  
## <a name="remarks"></a>설명  
 항상 문자열이 나 길이 인수를 반환 하거나 사용 하는 유니코드 함수는 문자 수로 전달 됩니다. 서버 데이터의 길이 정보를 반환 하는 함수의 경우 표시 크기와 전체 자릿수는 문자 수로 설명 됩니다. 길이 (데이터의 전송 크기)가 문자열 또는 문자열이 아닌 데이터를 참조할 수 있는 경우 길이는 8 진수 길이에 설명 되어 있습니다. 예를 들어 **SQLGetInfoW** 는 길이가 바이트 수로 계속 사용 되지만 **Sqlexecdirectw** 는 문자 수를 사용 합니다.  
  
 문자 수는 ANSI 함수의 바이트 수 (8 진수)와 유니코드 함수의 WCHAR (16 비트 단어) 수를 나타냅니다. 특히 DBCS (더블 바이트 문자 시퀀스) 또는 MBCS (멀티 바이트 문자 시퀀스)를 여러 바이트로 구성할 수 있습니다. UTF-16 유니코드 문자 시퀀스는 여러 개의 WCHARs로 구성 될 수 있습니다.  
  
 다음은 유니코드 (W) 및 ANSI (A) 버전을 모두 지 원하는 ODBC API 함수 목록입니다.  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagRec**|  
|**SQLColAttribute**|**SQLGetInfo**|  
|**SQLColAttributes**|**SQLGetStmtAttr**|  
|**SQLColumnPrivileges**|**SQLGetTypeInfo**|  
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
|**SQLGetDiagField**||  
  
 다음은 유니코드 (W) 및 ANSI (A) 버전을 모두 지 원하는 ODBC 설치 관리자 및 ODBC 변환기 함수 목록입니다.  
  
|||  
|-|-|  
|**SQLConfigDataSource**|**SQLInstallDriverManager**|  
|**SQLCreateDataSource**|**SQLInstallerError**|  
|**SQLDataSourceToDriver**|**SQLInstallODBC**|  
|**SQLDriverToDataSource**|**SQLReadFileDSN**|  
|**SQLGetAvailableDrivers**|**SQLRemoveDSNFromINI**|  
|**SQLGetInstalledDrivers**|**Sql유효한 Dsn**|  
|**SQLGetTranslator**|**SQLWriteDSNToINI**|  
|**SQLInstallDriver**||  
  
> [!NOTE]
>  사용 되지 않는 함수는 유니코드 **#define**를 사용 하 여 odbc *2.x 응용 프로그램* 을 다시 컴파일할 수 있도록 지원 하기 때문에 유니코드-ANSI 매핑 지원이 *있습니다.*  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [유니코드 애플리케이션](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [유니코드 드라이버](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [드라이버 관리자의 함수 매핑](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
