---
title: 수준 1 인터페이스 적합성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- level 1 interface conformance levels [ODBC]
ms.assetid: ee3f5c08-0583-4f3b-8354-ef71b6086a7e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d75c374a7d9d57483dd56e34b51fcb6d89e1b52
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213483"
---
# <a name="level-1-interface-conformance"></a>수준 1 인터페이스 적합성
수준 1 인터페이스 적합성 수준에는 핵심 인터페이스 적합성 수준 기능 및 OLTP 관계형 DBMS는 일반적으로 사용할 수 있는 트랜잭션과 같은 추가 기능을 포함 합니다. 수준 1 인터페이스와 호환 되는 드라이버는 핵심 인터페이스 적합성 수준에서 기능 외에 다음을 수행 하 여 응용 프로그램을 사용 수 있습니다.  
  
|||  
|-|-|  
|101|데이터베이스의 스키마 테이블 및 뷰 (두 부분으로 사용)을 지정 합니다. (자세한 내용은 참조에서 201 기능 세 부분으로 이루어진 명명 [수준 2 인터페이스 적합성](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|102|모두 동기 이거나 모두 비동기 지정된 된 연결에 ODBC 함수를 적용할 수 있는 ODBC 함수의 true 비동기 실행을 호출 합니다.|  
|103|스크롤 가능 커서를 사용 하 고 여는 메서드에서 전진 전용 이외의 호출 하면 결과 집합에 대 한 액세스를 달성 **SQLFetchScroll** 사용 하 여 합니다 *FetchOrientation* SQL_FETCH_NEXT 이외의 인수입니다. (의 SQL_FETCH_BOOKMARK *FetchOrientation* 204 기능에 [수준 2 인터페이스 적합성](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|104|호출 하 여 테이블의 기본 키를 가져올 **SQLPrimaryKeys**합니다.|  
|105|프로시저 호출에 대 한 ODBC 이스케이프 시퀀스를 통해 저장된 프로시저를 사용 하 고 호출 하 여 저장된 프로시저에 대 한 데이터 사전 쿼리 **SQLProcedureColumns** 하 고 **SQLProcedures**합니다. (프로세스는 프로시저 작성 되어 데이터 원본에 저장 된 경우이 문서의 범위 외부)|  
|106|호출 하 여 사용 가능한 서버를 대화형으로 찾아봄으로써 데이터 원본에 연결 **SQLBrowseConnect**합니다.|  
|107|SQL 문 대신 ODBC 함수를 사용 하 여 특정 데이터베이스 작업을 수행 합니다. **SQLSetPos** SQL_POSITION과 SQL_REFRESH 합니다.|  
|108|호출 하 여 일괄 처리 및 저장된 프로시저에서 생성 하는 여러 결과 집합의 내용에 액세스할 **SQLMoreResults**합니다.|  
|109|True 원자성 및 SQL_ROLLBACK에서 지정 하는 기능을 사용 하 여 여러 ODBC 함수에 걸쳐 있는 트랜잭션을 구분 **SQLEndTran**합니다.|
