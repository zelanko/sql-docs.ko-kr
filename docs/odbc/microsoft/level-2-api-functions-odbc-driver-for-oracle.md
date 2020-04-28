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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1e181c5863d6b906eaf9a3ba499728c595f0449
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284183"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>수준 2 API 함수(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 이 수준의 함수는 수준 1 인터페이스 규칙과 책갈피, 동적 매개 변수 및 ODBC 함수의 비동기 실행 등의 추가 기능을 제공 합니다.  
  
|API 함수|참고|  
|------------------|-----------|  
|**SQLBindParameter**|SQL 문의 매개 변수 표식과 버퍼를 연결 합니다.|  
|**SQLBrowseConnect**|특성 및 특성 값의 연속 수준을 반환 합니다.|  
|**SQLDataSources**|데이터 원본 이름을 나열 합니다. 드라이버 관리자에 의해 구현 됩니다.|  
|**SQLDescribeParam**|준비 된 SQL 문과 연결 된 매개 변수 표식에 대 한 설명을 반환 합니다.<br /><br /> 문의 구문 분석에 따라 매개 변수가 무엇 인지를 가장 잘 추측 합니다. 매개 변수 형식을 확인할 수 없는 경우 SQL_VARCHAR는 길이가 2000 인을 반환 합니다.|  
|**SQLDrivers**|드라이버 관리자에 의해 구현 됩니다.|  
|**SQLExtendedFetch**|**Sqlfetch** 와 유사 하지만 각 열에 대해 배열을 사용 하 여 여러 행을 반환 합니다. 결과 집합은 앞으로 스크롤할 수 있으며 커서가 전진 전용이 아닌 정적으로 정의 된 경우에는 뒤로 스크롤할 수 있습니다. 기본 열 바인딩을 사용 하는 앞 으로만 이동 가능한 커서의 경우에는 BUFFERSIZE 연결 특성 보다 큰 데이터 집합의 열 데이터가 데이터 버퍼로 직접 인출 됩니다. 는 가변 길이 책갈피를 지원 하지 않으며 책갈피에서 0이 아닌 오프셋에 있는 행 집합을 인출 하는 것을 지원 하지 않습니다.|  
|**SQLForeignKeys**|단일 테이블의 외래 키 목록과 단일 테이블을 참조 하는 다른 테이블의 외래 키 목록을 반환 합니다.|  
|**SQLMoreResults**|문 핸들, hstmt, SELECT, UPDATE, INSERT 또는 DELETE 문에서 보류 중인 결과가 더 있는지 여부를 확인 하 고, 해당 하는 경우 해당 결과에 대 한 처리를 초기화 합니다.<br /><br /> Oracle은 {resultset ...} 이스케이프 시퀀스를 사용 하는 경우 저장 프로시저 에서만 여러 결과 집합을 지원 합니다.|  
|**SQLNativeSql**|사용에 대 한 자세한 내용은 [저장 프로시저에서 배열 매개 변수 반환](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)을 참조 하세요.|  
|**SQLNumParams**|SQL 문의 매개 변수 수를 반환 합니다. 매개 변수 개수는 **Sqlprepare**에 전달 된 SQL 문의 물음표 수와 같아야 합니다.|  
|**SQLPrimaryKeys**|테이블의 기본 키를 구성 하는 열 이름을 반환 합니다.|  
|**SQLProcedureColumns**|입력 및 출력 매개 변수, 반환 값, 단일 프로시저의 결과 집합에 있는 열, 두 개의 추가 열, 오버 로드 및 ORDINAL_POSITION의 목록을 반환 합니다. 오버 로드는 Oracle 데이터 사전 뷰의 ALL_ARGUMENTS 테이블에 있는 오버 로드 열입니다. ORDINAL_POSITION은 Oracle 데이터 사전 뷰의 ALL_ARGUMENTS 테이블에 있는 시퀀스 열입니다. 패키지 프로시저의 경우 프로시저 이름 열은 *packagename. e* 형식입니다. 는 프로시저 또는 함수를 참조 하는 생성 된 동의어의 프로시저 열을 반환 하지 않습니다.|  
|**SQLProcedures**|데이터 원본에 있는 프로시저의 목록을 반환 합니다. 패키지 프로시저의 경우 프로시저 이름 열은 *packagename. e* 형식입니다.<br /><br /> Oracle은 패키지 된 프로시저를 패키지 된 함수와 구분 하는 방법을 제공 하지 않으므로 드라이버는 PROCEDURE_TYPE 열에 대 한 SQL_PT_UNKNOWN를 반환 합니다.|  
|**SQLSetPos**|행 집합에서 커서 위치를 설정 합니다. **SQLSetPos** 를 **SQLGetData** 와 함께 사용 하 여 행 집합의 특정 행에 커서를 놓은 후 바인딩되지 않은 열에서 행을 검색할 수 있습니다. *Foption* SQL_ADD를 사용 하 여 결과 집합에 추가 된 행은 결과 집합의 마지막 행 뒤에 추가 됩니다.|  
|**SQLSetScrollOptions**|문 핸들 hstmt와 연결 된 커서의 동작을 제어 하는 옵션을 설정 합니다. 자세한 내용은 [커서 유형 및 동시성 조합](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)을 참조 하세요.|
