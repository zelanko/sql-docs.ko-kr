---
title: 수준 2 인터페이스 규칙 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306165"
---
# <a name="level-2-interface-conformance"></a>수준 2 인터페이스 적합성
수준 2 인터페이스 규칙 수준은 수준 1 인터페이스 규칙 수준 기능 및 다음 기능을 포함 합니다.  
  
|||  
|-|-|  
|201|데이터베이스 테이블 및 뷰의 세 부분으로 된 이름을 사용 합니다. 자세한 내용은 [수준 1 인터페이스 규칙](../../../odbc/reference/develop-app/level-1-interface-conformance.md)의 두 부분으로 구성 된 명명 지원 기능 101을 참조 하세요.|  
|202|**SQLDescribeParam**를 호출 하 여 동적 매개 변수를 설명 합니다.|  
|203|입력 매개 변수 뿐만 아니라 출력 및 입/출력 매개 변수와 저장 프로시저의 결과 값을 사용 합니다.|  
|204|열 번호 0에서 **SQLDescribeCol** 및 **sqlcolattribute** 를 호출 하 여 책갈피 검색을 포함 한 책갈피를 사용 합니다. *Fetchorientation* 인수가 SQL_FETCH_BOOKMARK로 설정 된 **sqlfetchscroll** 을 호출 하 여 책갈피를 기반으로 인출 합니다. SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK 또는 SQL_FETCH_BY_BOOKMARK로 설정 된 *Operation* 인수를 사용 하 여 **SQLBulkOperations** 를 호출 하 여 책갈피 작업으로 업데이트, 삭제 및 인출 합니다.|  
|205|**Sqlcolumnprivileges**, **SQLForeignKeys**및 **sqlcolumnprivileges**을 호출 하 여 데이터 사전에 대 한 고급 정보를 검색 합니다.|  
|206|SQL 문 대신 ODBC 함수를 사용 하 여 추가 데이터베이스 작업을 수행 하는 데 SQL_ADD를 사용 하 여 **SQLBulkOperations** 를 호출 하거나 SQL_DELETE 또는 SQL_UPDATE로 **SQLSetPos** 를 호출 합니다. *LockType* 인수가 SQL_LOCK_EXCLUSIVE 또는 SQL_LOCK_UNLOCK로 설정 된 **SQLSetPos** 호출에 대 한 지원은 규칙 수준의 일부가 아니지만 선택적 기능입니다.|  
|207|지정 된 개별 문에 대해 ODBC 함수를 비동기적으로 실행할 수 있습니다.|  
|208|**SQLSpecialColumns**를 호출 하 여 테이블의 SQL_ROWVER 행 식별 열을 가져옵니다. 자세한 내용은 **SQLSpecialColumns** 에 대 한 지원을 참조 하세요. *IdentifierType* 인수는 [코어 인터페이스 규칙](../../../odbc/reference/develop-app/core-interface-conformance.md)에서 기능 20으로 SQL_BEST_ROWID로 설정 됩니다.|  
|209|SQL_ATTR_CONCURRENCY statement 특성 SQL_CONCUR_READ_ONLY 아닌 하나 이상의 값으로 설정 합니다.|  
|210|로그인 요청 및 SQL 쿼리 (SQL_ATTR_LOGIN_TIMEOUT 및 SQL_ATTR_QUERY_TIMEOUT)의 시간을 제한 하는 기능입니다.|  
|211|기본 격리 수준을 변경 하는 기능 "serializable" 격리 수준으로 트랜잭션을 실행할 수 있습니다.|
