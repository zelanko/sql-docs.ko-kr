---
title: 레벨 1 API 기능(오라클용 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37305ee75ebeb0686bafe039f1102cb3c6e18674
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299953"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>수준 1 API 함수(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 이 수준의 함수는 핵심 인터페이스 적합성과 트랜잭션 지원과 같은 추가 기능을 제공합니다.  
  
|API 기능|메모|  
|------------------|-----------|  
|**SQLColumns**|지정된 테이블 또는 테이블의 열 목록인 테이블에 대한 결과 집합을 만듭니다. PUBLIC 동의어에 대한 열을 요청하는 경우 SYNONYMCOLUMNS 연결 특성을 설정하고 빈 문자열을 *szTableOwner* 인수로 지정해야 합니다. PUBLIC 동의어에 대한 열을 반환할 때 드라이버는 TABLE NAME 열을 빈 문자열로 설정합니다. 결과 집합에는 각 행의 끝에 ORDINAL POSITION라는 추가 열이 포함되어 있습니다. 이 값은 테이블의 열의 서수 위치입니다.|  
|**SQLDriverConnect**|기존 데이터 원본에 연결합니다. 자세한 내용은 [연결 문자열 형식 및 특성을](../../odbc/microsoft/connection-string-format-and-attributes.md)참조하십시오.|  
|**SQLGet연결 옵션**|연결 옵션의 현재 설정을 반환합니다. 이 함수는 부분적으로 지원됩니다. 드라이버는 *fOption* 인수에 대한 모든 값을 지원하지만 *fOption* 인수 [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)대한 일부 *vParam* 값을 지원하지 않습니다. 자세한 내용은 [연결 옵션을](../../odbc/microsoft/connect-options.md)참조하십시오.|  
|**SQLGetData**|지정된 결과 집합의 현재 레코드에서 단일 필드 값을 검색합니다.|  
|**SQLGetFunctions**|지원되는 모든 함수에 대해 TRUE를 반환합니다. 드라이버 관리자에 의해 구현됩니다.|  
|**SQLGetInfo**|오라클의 ODBC 드라이버및 연결 핸들, *hdbc와*관련된 데이터 소스에 \*대한 SQLHDBC, SQLUSMALLINT, SQLTHEINT, SQLSMALLINT 및 SQLSMALLINT를 포함한 정보를 반환합니다.|  
|**SQLGetStmt옵션**|명령문 옵션의 현재 설정을 반환합니다. 자세한 내용은 [명령문 옵션을](../../odbc/microsoft/statement-options.md)참조하십시오.|  
|**SQLGetTypeInfo**|데이터 원본에서 지원하는 데이터 형식에 대한 정보를 반환합니다. 드라이버는 SQL 결과 집합의 정보를 반환합니다.|  
|**SQLParamData**|**SQLPutData와** 함께 사용하여 문 실행 시간에 매개 변수 데이터를 지정합니다.|  
|**SQLPutData**|응용 프로그램이 명령문 실행 시간에 매개 변수 또는 열에 대한 데이터를 드라이버에 보낼 수 있습니다.|  
|**SQLSet연결옵션**|연결의 측면을 제어하는 옵션에 대한 액세스를 제공합니다. 이 함수는 부분적으로 지원됩니다: 드라이버는 *fOption* 인수에 대한 모든 값을 지원하지만 *fOption* 인수 [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)대한 일부 *vParam* 값을 지원하지 않습니다. 자세한 내용은 [연결 옵션을](../../odbc/microsoft/connect-options.md)참조하십시오.|  
|**SQLSetStmt옵션**|명령문 핸들, *hstmt와*관련된 옵션을 설정합니다. 자세한 내용은 [명령문 옵션을](../../odbc/microsoft/statement-options.md)참조하십시오.|  
|**SQLSpecialColumns**|테이블의 행을 고유하게 식별하는 최적의 열 집합을 검색합니다.|  
|**SQLStatistics**|단일 테이블과 테이블과 연결된 인덱스 또는 태그 이름에 대한 통계 목록을 검색합니다. 드라이버는 결과 집합으로 정보를 반환합니다.|  
|**SQLTables**|SQLTables 문의 매개 변수에 의해 지정 된 테이블 이름 목록을 반환 **합니다.** 매개 변수를 지정하지 않으면 현재 데이터 원본에 저장된 테이블 이름을 반환합니다. 드라이버는 결과 집합으로 정보를 반환합니다.<br /><br /> 열거 형 호출은 원격 보기 또는 로컬 매개 변수뷰에 대한 결과 집합 항목을 수신하지 않습니다. 그러나 고유한 테이블 이름 지정기를 사용하여 **SQLTables를** 호출하면 해당 이름과 함께 해당 뷰에 대한 일치 항목이 검색됩니다. 이렇게 하면 API가 새 테이블을 만들기 전에 이름 충돌을 확인할 수 있습니다.<br /><br /> 공용 동의어는 ""의 TABLE_OWNER 값으로 반환됩니다.<br /><br /> SYS 또는 SYSTEM이 소유한 뷰는 시스템 보기로 식별됩니다.|
