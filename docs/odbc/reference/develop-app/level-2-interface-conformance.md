---
title: 수준 2 인터페이스 적합성 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bff3de6a9b9ec57f1ea96d6db17b9b30c5a22996
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52515313"
---
# <a name="level-2-interface-conformance"></a>수준 2 인터페이스 적합성
수준 2 인터페이스 적합성 수준 수준 1 인터페이스 적합성 수준 기능 및 다음 기능을 포함 합니다.  
  
|||  
|-|-|  
|201|데이터베이스 테이블 및 뷰 세 부분으로 이루어진 이름을 사용 합니다. (자세한 내용은 참조의 두 부분으로 이루어진 명명 지원 기능 101 [수준 1 인터페이스 적합성](../../../odbc/reference/develop-app/level-1-interface-conformance.md).)|  
|202|동적 매개 변수를 호출 하 여 설명 **SQLDescribeParam**합니다.|  
|203|뿐만 아니라 입력된 매개 변수가 있지만 출력 및 입/출력 매개 변수 및 저장된 프로시저의 결과 값을 사용 합니다.|  
|204|책갈피를 호출 하 여 검색을 포함 하 여 책갈피를 사용 하 여 **SQLDescribeCol** 하 고 **SQLColAttribute** 열에 숫자 0; 호출 하 여 책갈피를 따라 가져오는 **SQLFetchScroll** 사용 하 여 합니다 *FetchOrientation* SQL_FETCH_BOOKMARK; 업데이트를 설정 하는 인수를 삭제 및 호출 하 여 책갈피 작업에 의해 인출 **SQLBulkOperations** 합니다 를사용하여*작업* 인수 SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK, 또는 SQL_FETCH_BY_BOOKMARK로 설정 합니다.|  
|205|데이터 사전에 대 한 정보를 호출 하 여 고급 검색 **SQLColumnPrivileges**하십시오 **SQLForeignKeys**, 및 **SQLTablePrivileges**합니다.|  
|206|SQL 문 대신 ODBC 함수를 사용 하 여 호출 하 여 추가 데이터베이스 작업을 수행할 **SQLBulkOperations** SQL_ADD를 사용 하 여 또는 **SQLSetPos** SQL_DELETE 또는 SQL_UPDATE 합니다. (에 대 한 호출에 대 한 지원을 **SQLSetPos** 사용 하 여 합니다 *LockType* SQL_LOCK_EXCLUSIVE 또는 SQL_LOCK_UNLOCK로 설정 하는 인수 적합성 수준 포함 되지 않지만 선택적 기능입니다.)|  
|207|지정 된 개별 문에 대 한 ODBC 함수의 비동기 실행을 사용 하도록 설정 합니다.|  
|208|호출 하 여 테이블의 SQL_ROWVER 행 식별 열을 가져올 **SQLSpecialColumns**합니다. (자세한 내용은 참조에 대 한 지원 **SQLSpecialColumns** 사용 하 여 합니다 *IdentifierType* 인수와 함께 SQL_BEST_ROWID 20에서 기능으로 [핵심 인터페이스 적합성](../../../odbc/reference/develop-app/core-interface-conformance.md) .)|  
|209|하나 이상의 값 SQL_CONCUR_READ_ONLY 이외의 문 특성 SQL_ATTR_CONCURRENCY를 설정 합니다.|  
|210|로그인 요청 시간 초과 및 SQL 쿼리 (SQL_ATTR_LOGIN_TIMEOUT 및 SQL_ATTR_QUERY_TIMEOUT) 수 있습니다.|  
|211|기본 격리 수준을; 변경 하는 기능 "직렬화" 격리 수준으로 트랜잭션을 실행할 수 있습니다.|
