---
title: "수준 1 인터페이스 규칙에 따라 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- level 1 interface conformance levels [ODBC]
ms.assetid: ee3f5c08-0583-4f3b-8354-ef71b6086a7e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c1f9e266e4379b2d1cfc9ee771ac49694cd3c58b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="level-1-interface-conformance"></a>수준 1 인터페이스 규칙
OLTP 관계형 DBMS에서 일반적으로 사용할 수 있는 트랜잭션과 같은 추가 기능을 포함 하는 핵심 인터페이스 규칙에 따라 수준 기능 수준 1 인터페이스 규칙 수준에 포함 되어 있습니다. 수준 1 드라이버 인터페이스 –와 호환 되는 핵심 인터페이스 규칙 수준에서 기능 외에도 다음을 수행 하는 응용 프로그램 수 있습니다.  
  
|||  
|-|-|  
|101|데이터베이스의 스키마 테이블 및 뷰 (두 부분 사용)을 지정 합니다. (자세한 내용은 참조에 201 기능 세 부분으로 이루어진 명명 [수준 2 인터페이스 규칙에 따라](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|102|True 비동기 실행의 모든 동기 또는 지정된 된 연결에서 비동기 모든 ODBC 함수를 적용할 수 있는 ODBC 함수를 호출 합니다.|  
|103|스크롤 가능 커서를 사용 하 고 되므로 결과 집합 메서드에서 전진 전용 이외의 호출 하 여에 대 한 액세스를 달성 **SQLFetchScroll** 와 *FetchOrientation* SQL_FETCH_NEXT 이외의 인수입니다. (SQL_FETCH_BOOKMARK는 *FetchOrientation* 204 기능에 [수준 2 인터페이스 규칙에 따라](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|104|호출 하 여 테이블의 기본 키를 가져올 **SQLPrimaryKeys**합니다.|  
|105|프로시저 호출에 대 한 ODBC 이스케이프 시퀀스를 통해 저장된 프로시저를 사용 하 고 호출 하 여 저장된 프로시저에 대 한 데이터 사전 쿼리 **SQLProcedureColumns** 및 **SQLProcedures**합니다. (프로시저 기준인 생성 및 데이터 원본에 저장 된 프로세스를 벗어난 경우이 문서의 범위)|  
|106|호출 하 여 사용 가능한 서버를 대화형으로 찾아봄으로써 데이터 원본에 연결 **SQLBrowseConnect**합니다.|  
|107|SQL 문 대신 ODBC 함수를 사용 하 여 특정 데이터베이스 작업을 수행: **SQLSetPos** SQL_POSITION과 SQL_REFRESH 합니다.|  
|108|호출 하 여 일괄 처리 및 저장된 프로시저에서 생성 된 여러 결과 집합의 내용에 액세스할 **SQLMoreResults**합니다.|  
|109|완벽 한 원자성 및 SQL_ROLLBACK에서 지정 하는 기능 사용 하 여 몇 가지 ODBC 함수에 걸쳐 있는 트랜잭션을 구분 **SQLEndTran**합니다.|

