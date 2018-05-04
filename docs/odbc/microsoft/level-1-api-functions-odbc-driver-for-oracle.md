---
title: 수준 1 API 함수 (ODBC Driver for Oracle) | Microsoft Docs
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
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e3f6f331dc283c25fa9e6a36b7272db56763f53
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>수준 1 API 함수 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 이 수준 제공 핵심 인터페이스 규칙에 대 한 함수 및 트랜잭션 같은 추가 기능을 지원 합니다.  
  
|API 함수|참고|  
|------------------|-----------|  
|**SQLColumns**|지정된 된 테이블에 대 한 열 목록은 테이블 또는 테이블에 대 한 결과 집합을 만듭니다. 공용 동의어에 대 한 열을 요청할 때 SYNONYMCOLUMNS 연결 특성을 설정 하 고 해야으로 빈 문자열을 지정 된 *szTableOwner* 인수입니다. 공용 동의어에 대 한 열을 반환할 때 드라이버는 테이블 이름 열을 빈 문자열로 설정 합니다. 결과 집합에는 추가 열 서 수 위치에 각 행의 끝에 포함 되어 있습니다. 이 값은 테이블의 열 서 수 위치입니다.|  
|**SQLDriverConnect**|기존 데이터 원본에 연결합니다. 자세한 내용은 참조 [연결 문자열 형식 및 특성](../../odbc/microsoft/connection-string-format-and-attributes.md)합니다.|  
|**SQLGetConnectOption**|연결 옵션의 현재 설정을 반환합니다. 이 함수는 부분적으로 지원 합니다. 드라이버 지원에 대 한 모든 값은 *fOption* 인수 하지만 일부를 지원 하지 않습니다 *vParam* 에 대 한 값은 *fOption* 인수 [SQL_TXN_ISOLATION ](../../odbc/microsoft/connect-options.md). 자세한 내용은 참조 [연결 옵션](../../odbc/microsoft/connect-options.md)합니다.|  
|**SQLGetData**|지정 된 결과 집합의 현재 레코드의 단일 필드의 값을 검색 합니다.|  
|**SQLGetFunctions**|지원 되는 모든 함수에 대 한 TRUE를 반환 합니다. 드라이버 관리자에서 구현 됩니다.|  
|**SQLGetInfo**|SQLHDBC, SQLUSMALLINT, 대 SQLPOINTER, SQLSMALLINT, 및 SQLSMALLINT 등의 정보를 반환 \*, 연결 핸들에 연결 된 Oracle 및 데이터 원본에 대 한 ODBC 드라이버에 대 한 *hdbc*합니다.|  
|**SQLGetStmtOption**|문 옵션의 현재 설정을 반환합니다. 자세한 내용은 참조 [문 옵션](../../odbc/microsoft/statement-options.md)합니다.|  
|**SQLGetTypeInfo**|데이터 원본에서 지 원하는 데이터 형식에 대 한 정보를 반환 합니다. 드라이버는 SQL 결과 집합의 정보를 반환 합니다.|  
|**SQLParamData**|와 함께 사용할 **SQLPutData** 문 실행 시 데이터 매개 변수를 지정할 수 있습니다.|  
|**SQLPutData**|문 실행 시 드라이버에는 매개 변수 또는 열에 대 한 데이터를 보내는 응용 프로그램을 허용 합니다.|  
|**SQLSetConnectOption**|연결의 한 측면을 제어 하는 옵션에 대 한 액세스를 제공 합니다. 이 함수는 부분적으로 지원: 드라이버 지원에 대 한 모든 값은 *fOption* 인수 하지만 일부를 지원 하지 않습니다 *vParam* 에 대 한 값은 *fOption* 인수 [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)합니다. 자세한 내용은 참조 [연결 옵션](../../odbc/microsoft/connect-options.md)합니다.|  
|**SQLSetStmtOption**|문 핸들에 관련 된 옵션 설정 *hstmt*합니다. 자세한 내용은 참조 [문 옵션](../../odbc/microsoft/statement-options.md)합니다.|  
|**SQLSpecialColumns**|테이블의 행을 고유 하 게 식별 하는 열의 최적 집합을 검색 합니다.|  
|**SQLStatistics**|단일 테이블, 인덱스 또는 테이블에 연결 된 태그 이름에 대 한 통계 목록을 검색 합니다. 드라이버 정보 결과 집합으로 반환 합니다.|  
|**SQLTables**|매개 변수에서 지정한 테이블 이름 목록을 반환 하는 **SQLTables** 문. 없는 매개 변수를 지정 하는 경우 현재 데이터 원본에 저장 된 테이블 이름을 반환 합니다. 드라이버 정보 결과 집합으로 반환 합니다.<br /><br /> 열거형 형식 호출 원격 뷰 또는 로컬 매개 변수화 된 보기에 대 한 결과 집합 항목을 수신 하지 않습니다. 그러나에 대 한 호출 **SQLTables** 고유 테이블이 포함 된 이름이 있는 경우 이름 지정자 이러한 보기에 대 한 일치를 찾으려고 합니다; 이렇게 하면 새 테이블의 이전 이름 충돌을 확인 하는 API입니다.<br /><br /> 공용 동의어 TABLE_OWNER 값으로 반환 됩니다 ""입니다.<br /><br /> SYS 또는 시스템에서 소유 하는 뷰는 시스템 뷰로 식별 됩니다.|
