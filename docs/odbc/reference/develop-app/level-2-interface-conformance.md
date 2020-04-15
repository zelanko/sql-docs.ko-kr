---
title: 레벨 2 인터페이스 적합성 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- level 2 interface conformance levels [ODBC]
- conformance levels [ODBC], interface
ms.assetid: 2dc87840-f2fe-43dd-9d7b-bd95523081d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ee57d716cbb93f855e1fd78d41bff62a681eb6c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306165"
---
# <a name="level-2-interface-conformance"></a>수준 2 인터페이스 적합성
수준 2 인터페이스 준수 수준에는 수준 1 인터페이스 적합성 수준 기능과 다음 기능이 포함됩니다.  
  
|||  
|-|-|  
|201|데이터베이스 테이블 및 뷰의 세 부분으로 구성된 이름을 사용합니다. 자세한 내용은 [레벨 1 인터페이스 적합성의](../../../odbc/reference/develop-app/level-1-interface-conformance.md)두 부분으로 구성된 명명 지원 기능 101을 참조하십시오.|  
|202|**SQLDescribeParam을**호출하여 동적 매개 변수를 설명합니다.|  
|203|입력 매개 변수뿐만 아니라 출력 및 입력/출력 매개 변수및 저장 프로시저의 결과 값도 사용합니다.|  
|204|열 번호 0에서 **SQLDescribeCol** 및 **SQLColAttribute를** 호출하여 책갈피 검색을 포함한 책갈피를 사용합니다. 책갈피를 기반으로 가져오기, **sqlFetchScroll** 를 호출 하 여 *FetchOrientation* SQL_FETCH_BOOKMARK 설정 된 방향 인수; bookbulk 작업별로 update, 삭제 및 가져오기를 사용하여 **SQLBulkOperations를** SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK 또는 SQL_FETCH_BY_BOOKMARK 로 설정된 *작업* 인수를 호출합니다.|  
|205|**SQLColumnPrivileges,** **SQLForeignKeys**및 **SQLTablePrivileges를**호출하여 데이터 사전에 대한 고급 정보를 검색합니다.|  
|206|SQL 문 대신 ODBC 함수를 사용하여 **sqlBulkOperations를** SQL_ADD 호출하거나 SQL_DELETE 또는 SQL_UPDATE **SQLSetPos를** 호출하여 추가 데이터베이스 작업을 수행합니다. SQL_LOCK_EXCLUSIVE 또는 SQL_LOCK_UNLOCK 로 설정된 *LockType* 인수를 사용하여 **SQLSetPos** 호출에 대한 지원은 적합성 수준에 포함되지 않지만 선택적 기능입니다.|  
|207|지정된 개별 문에 대해 ODBC 함수의 비동기 실행을 활성화합니다.|  
|208|**SQLSpecialColumns를**호출하여 테이블의 행 식별 열을 SQL_ROWVER 가져옵니다. 자세한 내용은 [핵심 인터페이스 적합성의](../../../odbc/reference/develop-app/core-interface-conformance.md)기능 20으로 SQL_BEST_ROWID *identifierType* 인수가 설정된 **SQLSpecialColumns에** 대한 지원을 참조하십시오.|  
|209|SQL_ATTR_CONCURRENCY 문 특성을 SQL_CONCUR_READ_ONLY 이외의 하나 이상의 값으로 설정합니다.|  
|210|로그인 요청 및 SQL 쿼리(SQL_ATTR_LOGIN_TIMEOUT 및 SQL_ATTR_QUERY_TIMEOUT)를 시간 중지하는 기능입니다.|  
|211|기본 격리 수준을 변경할 수 있는 기능; "직렬화 가능" 격리 수준으로 트랜잭션을 실행할 수 있습니다.|
