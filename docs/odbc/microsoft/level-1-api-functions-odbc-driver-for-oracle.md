---
title: 수준 1 API 함수 (Oracle 용 ODBC 드라이버) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a70116fb0e8ef1236b18cb478184e96fe08fce5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47829421"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>수준 1 API 함수(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 이 수준 제공 핵심 인터페이스 적합성에 대 한 함수 및 트랜잭션 같은 추가 기능을 지원 합니다.  
  
|API 함수|참고|  
|------------------|-----------|  
|**SQLColumns**|지정한 테이블의 열 목록에는 테이블을 사용 하거나 테이블에 결과 집합을 만듭니다. 공용 동의어에 대 한 열을 요청 하면 있어야 SYNONYMCOLUMNS 연결 특성을 설정 하 고 빈 문자열로 지정 합니다 *szTableOwner* 인수입니다. 공용 동의어에 대 한 열을 반환할 때 드라이버 테이블 이름 열을 빈 문자열로 설정 합니다. 추가 열을 각 행의 끝에 서 수 위치를 포함 하는 결과 집합입니다. 이 값은 테이블의 열 서 수 위치입니다.|  
|**SQLDriverConnect**|기존 데이터 원본에 연결합니다. 자세한 내용은 참조 하세요 [연결 문자열 형식 및 특성](../../odbc/microsoft/connection-string-format-and-attributes.md)합니다.|  
|**SQLGetConnectOption**|연결 옵션의 현재 설정을 반환 합니다. 이 함수는 부분적으로 지원 합니다. 드라이버에 대 한 모든 값을 지원 합니다 *fOption* 인수 하지만 일부 지원 하지 않습니다 *갖고* 에 대 한 값을 *fOption* 인수 [SQL_TXN_ISOLATION ](../../odbc/microsoft/connect-options.md). 자세한 내용은 [연결 옵션](../../odbc/microsoft/connect-options.md)합니다.|  
|**SQLGetData**|지정 된 결과 집합의 현재 레코드의 단일 필드의 값을 검색 합니다.|  
|**SQLGetFunctions**|모든 지원 되는 함수에 대해 TRUE를 반환. 드라이버 관리자에 의해 구현 됩니다.|  
|**SQLGetInfo**|SQLHDBC "," SQLUSMALLINT "," 대 SQLPOINTER "," SQLSMALLINT, "및" SQLSMALLINT를 포함 하 여 정보를 반환 \*, Oracle 및 데이터 원본 연결 핸들을 사용 하 여 연결에 대 한 ODBC 드라이버에 대 한 *hdbc*합니다.|  
|**SQLGetStmtOption**|문 옵션의 현재 설정을 반환합니다. 자세한 내용은 [문 옵션](../../odbc/microsoft/statement-options.md)합니다.|  
|**SQLGetTypeInfo**|데이터 원본에서 지 원하는 데이터 형식에 대 한 정보를 반환 합니다. 드라이버는 SQL 결과 집합의 정보를 반환합니다.|  
|**SQLParamData**|와 함께 사용할 **SQLPutData** 문 실행 시 데이터 매개 변수를 지정 합니다.|  
|**SQLPutData**|문 실행 시 드라이버에 매개 변수 또는 열에 대 한 데이터를 보내도록 응용을 프로그램을 수 있습니다.|  
|**SQLSetConnectOption**|연결의 측면을 제어 하는 옵션에 대 한 액세스를 제공 합니다. 이 함수는 부분적으로 지원: 드라이버에 대 한 모든 값을 지원 합니다 *fOption* 인수 하지만 일부 지원 하지 않습니다 *갖고* 에 대 한 값을 *fOption* 인수 [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)합니다. 자세한 내용은 [연결 옵션](../../odbc/microsoft/connect-options.md)합니다.|  
|**SQLSetStmtOption**|문 핸들을 관련 된 옵션을 설정 합니다 *hstmt*합니다. 자세한 내용은 [문 옵션](../../odbc/microsoft/statement-options.md)합니다.|  
|**SQLSpecialColumns**|테이블의 행을 고유 하 게 식별 하는 최적의 열 집합을 검색 합니다.|  
|**SQLStatistics**|단일 테이블 및 인덱스 또는 테이블에 연결 된 태그 이름에 대 한 통계의 목록을 검색 합니다. 드라이버 정보 결과 집합으로 반환 합니다.|  
|**SQLTables**|매개 변수에서 지정한 테이블 이름 목록을 반환 합니다 **SQLTables** 문입니다. 없는 매개 변수를 지정 하는 경우에 현재 데이터 원본에 저장 된 테이블 이름을 반환 합니다. 드라이버 정보 결과 집합으로 반환 합니다.<br /><br /> 열거형 형식 호출에는 원격 뷰 또는 로컬 매개 변수가 있는 뷰에 대 한 결과 집합 항목을 수신 하지 않습니다. 그러나 호출 **SQLTables** 고유 테이블이 포함 된 이름이 있는 경우 이름 지정자 이러한 보기에 대 한 일치 하는 것은 이렇게 하면 새 테이블을 만들기 전에 이름 충돌을 확인 하는 API입니다.<br /><br /> 공용 동의어 TABLE_OWNER 값으로 반환 됩니다 ""입니다.<br /><br /> SYS 또는 시스템을 소유 하는 뷰는 시스템 뷰로 식별 됩니다.|
