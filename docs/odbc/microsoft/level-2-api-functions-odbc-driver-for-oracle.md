---
title: 레벨 2 API 기능(오라클용 ODBC 드라이버) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1e181c5863d6b906eaf9a3ba499728c595f0449
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284183"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>수준 2 API 함수(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 이 수준의 함수는 레벨 1 인터페이스 적합성과 북마크 지원, 동적 매개 변수 및 ODBC 함수의 비동기 실행과 같은 추가 기능을 제공합니다.  
  
|API 기능|메모|  
|------------------|-----------|  
|**SQLBindParameter**|버퍼를 SQL 문의 매개 변수 마커와 연결합니다.|  
|**SQLBrowseConnect**|연속적인 수준의 특성 및 특성 값을 반환합니다.|  
|**SQLDataSource**|데이터 원본 이름을 나열합니다. 드라이버 관리자에 의해 구현됩니다.|  
|**SQLDescribeParam**|준비된 SQL 문과 연결된 매개 변수 마커에 대한 설명을 반환합니다.<br /><br /> 문을 구문 분석하여 매개 변수가 무엇인지 가장 잘 추측합니다. 매개 변수 형식을 확인할 수 없는 경우 SQL_VARCHAR 길이 2000으로 반환됩니다.|  
|**SQLDrivers**|드라이버 관리자에 의해 구현됩니다.|  
|**SQLExtendedFetch**|**SQLFetch와** 유사하지만 각 열에 대한 배열을 사용하여 여러 행을 반환합니다. 결과 집합은 앞으로 스크롤할 수 있으며 커서가 정적이고 앞으로만 지정되지 않은 경우 뒤로 스크롤할 수 있습니다. 기본 열 바인딩이 있는 정방향 전용 커서의 경우 BUFFERSIZE 연결 특성보다 큰 데이터 집합의 열 데이터가 데이터 버퍼로 직접 가져옵니다. 길이가 가변책마크는 지원하지 않으며 책갈피에서 오프셋(0이 아닌)에서 행 집합 가져오기를 지원하지 않습니다.|  
|**SQLForeignKeys**|단일 테이블의 외래 키 목록 또는 단일 테이블을 참조하는 다른 테이블의 외래 키 목록을 반환합니다.|  
|**SQLMoreResults**|SELECT, UPDATE, INSERT 또는 DELETE 문을 포함하는 문 핸들, hstmt, hstmt에 더 많은 결과가 보류 중인지 여부를 결정하고, 그렇다면 해당 결과에 대한 처리를 초기화합니다.<br /><br /> 오라클은 {resultset... } 이스케이프 시퀀스를 사용하는 경우 저장 프로시저에서만 여러 결과 집합을 지원합니다.|  
|**SQLNativeSql**|사용에 대한 자세한 내용은 [저장 프로시저의 배열 매개 변수 반환을](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)참조하십시오.|  
|**SQLNumParams**|SQL 문의 매개 변수 수를 반환합니다. 매개 변수 의 수는 **SQLPrepare**에 전달 된 SQL 문의 물음표의 수와 같아야 합니다.|  
|**SQLPrimaryKeys**|테이블의 기본 키를 구성하는 열 이름을 반환합니다.|  
|**SQLProcedureColumns**|입력 및 출력 매개 변수 목록, 반환 값, 단일 프로시저의 결과 집합의 열 및 두 개의 추가 열인 오버로드 및 ORDINAL_POSITION 반환합니다. 오버로드는 Oracle 데이터 사전 보기의 ALL_ARGUMENTS 테이블의 오버로드 열입니다. ORDINAL_POSITION Oracle 데이터 사전 보기의 ALL_ARGUMENTS 테이블의 시퀀스 열입니다. 패키지된 프로시저의 경우 프로시저 이름 열은 *packagename.procedurename* 형식입니다. 프로시저 또는 함수를 참조하는 생성된 동의어의 프로시저 열을 반환하지 않습니다.|  
|**SQLProcedures**|데이터 원본의 프로시저 목록을 반환합니다. 패키지된 프로시저의 경우 프로시저 이름 열은 *packagename.procedurename* 형식입니다.<br /><br /> Oracle은 패키지된 프로시저를 패키지된 함수와 구분하는 방법을 제공하지 않으므로 드라이버는 PROCEDURE_TYPE 열에 대한 SQL_PT_UNKNOWN 반환합니다.|  
|**SQLSetPos**|행 집합에서 커서 위치를 설정합니다. **SQLGetData를** 사용하여 커서를 행 집합의 특정 행에 배치한 후 바인딩되지 않은 열에서 행을 검색할 수 있습니다. **SQLSetPos** *fOption* SQL_ADD 사용하여 결과 집합에 추가된 행은 결과 집합의 마지막 행 후에 추가됩니다.|  
|**SQLSet스크롤 옵션**|명령문 핸들 hstmt와 연관된 커서의 동작을 제어하는 옵션을 설정합니다. 자세한 내용은 [커서 유형 및 동시성 조합을](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)참조하십시오.|
