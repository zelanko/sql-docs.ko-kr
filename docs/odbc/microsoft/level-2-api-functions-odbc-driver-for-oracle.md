---
title: 수준 2 API 함수 (Oracle 용 ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC level 2 API functions [ODBC]
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- ODBC API functions [ODBC]
- API functions [ODBC]
- level 2 API functions [ODBC]
ms.assetid: d9f49520-72d7-4234-8635-260d0ce4199c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7600734fef44071b1f5e35c136a6b9facdb8b390
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949032"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>수준 2 API 함수(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 이 수준에서 함수 수준 1 인터페이스 적합성 및 책갈피, 동적 매개 변수 및 ODBC 함수의 비동기 실행에 대 한 지원 같은 추가 기능을 제공합니다.  
  
|API 함수|참고|  
|------------------|-----------|  
|**SQLBindParameter**|SQL 문에서 매개 변수 표식을 사용 하 여 버퍼를 연결합니다.|  
|**SQLBrowseConnect**|연속 수준의 특성 및 특성 값을 반환합니다.|  
|**SQLDataSources**|데이터 원본 이름을 나열합니다. 드라이버 관리자에 의해 구현 됩니다.|  
|**SQLDescribeParam**|준비 된 SQL 문과 사용 하 여 연결 하는 매개 변수 표식에 대 한 설명을 반환 합니다.<br /><br /> 문이 구문 분석에 따라, 어떤 매개 변수는 최상의 추측을 반환 합니다. 매개 변수 형식을 확인할 수 없는 경우 SQL_VARCHAR 길이 2000 사용 하 여 반환 합니다.|  
|**SQLDrivers**|드라이버 관리자에 의해 구현 됩니다.|  
|**SQLExtendedFetch**|비슷합니다 **SQLFetch** 배열을 사용 하 여 각 열에 대해 여러 행을 반환 합니다. 결과 집합은 정방향 스크롤 가능 하 고 이전 버전과 스크롤할 수 있는 정적, 정방향 전용 커서가 정의 된 경우 가능 합니다. 기본 열 바인딩 사용 하 여 정방향 전용 커서에 대 한 데이터 버퍼에 직접 BUFFERSIZE 연결 특성 보다 큰 데이터 집합에서 열 데이터가 페치됩니다. 가변 길이 책갈피를 지원 하지 않습니다 및 책갈피에서 오프셋 (0)이 아닌 행 집합을 인출 하는 것을 지원 하지 않습니다.|  
|**SQLForeignKeys**|단일 테이블을 사용 하거나 단일 테이블을 참조 하는 다른 테이블의 외래 키의 목록에서 외래 키 목록을 반환 합니다.|  
|**SQLMoreResults**|더 많은 결과 보류 중인지 여부를 결정 hstmt, 문 핸들에 대해 SELECT, UPDATE, INSERT 또는 DELETE 문을 포함 하 고 그렇다면 이러한 결과 대 한 처리를 초기화 합니다.<br /><br /> Oracle {... resultset} 이스케이프 시퀀스를 사용 하는 경우 저장된 프로시저에서 여러 결과 집합을 지원 합니다.|  
|**SQLNativeSql**|사용량에 대 한 내용은 [저장 프로시저에서 배열 매개 변수 반환](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)합니다.|  
|**SQLNumParams**|SQL 문에서 매개 변수 개수를 반환합니다. 매개 변수 수가 SQL 문에 전달할 물음표의 수와 같아야 **SQLPrepare**합니다.|  
|**SQLPrimaryKeys**|테이블에 대 한 기본 키를 구성 하는 열 이름을 반환 합니다.|  
|**SQLProcedureColumns**|입력 및 출력 매개 변수, 반환 값, 단일 프로시저가 결과 집합의 열 및 두 개의 추가 열 오버 로드 하 고 ORDINAL_POSITION의 목록을 반환합니다. 오버 로드에는 Oracle 데이터 사전 뷰의 ALL_ARGUMENTS 테이블에서 오버 로드 열입니다. ORDINAL_POSITION는 Oracle 데이터 사전 뷰의 ALL_ARGUMENTS 테이블에서 순서 열입니다. 패키지 된 프로시저에 대 한 프로시저 이름 열이 속한 *packagename.procedurename* 형식입니다. 프로시저에 대 한 열의 프로시저 또는 함수를 가리키는 만든된 동의어를 반환 하지 않습니다.|  
|**SQLProcedures**|데이터 원본에 프로시저의 목록을 반환합니다. 패키지 된 프로시저에 대 한 프로시저 이름 열이 속한 *packagename.procedurename* 형식입니다.<br /><br /> Oracle 패키지 함수에서 패키지 된 프로시저를 구별 하는 방법을 제공 하지 않으므로, 드라이버 SQL_PT_UNKNOWN PROCEDURE_TYPE 열에 반환 합니다.|  
|**SQLSetPos**|행 집합의 커서 위치를 설정합니다. 사용할 수 있습니다 **SQLSetPos** 사용 하 여 **SQLGetData** 행 집합의 특정 행에 커서를 놓고 후 바인딩되지 않은 열에서 행을 검색 합니다. 결과 사용 하 여 집합에 추가 된 행 *fOption* SQL_ADD 결과 집합의 마지막 행 뒤에 추가 됩니다.|  
|**SQLSetScrollOptions**|Hstmt 문 핸들을 사용 하 여 연결 된 커서의 동작을 제어 하는 옵션을 설정 합니다. 자세한 내용은 참조 하세요 [커서 유형 및 동시성 조합](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)합니다.|
