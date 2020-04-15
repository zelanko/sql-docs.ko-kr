---
title: 레벨 1 인터페이스 적합성 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d31d5fe8aea1df4e7937104580efb820ba6f031
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306184"
---
# <a name="level-1-interface-conformance"></a>수준 1 인터페이스 적합성
수준 1 인터페이스 준수 수준에는 일반적으로 OLTP 관계형 DBMS에서 사용할 수 있는 코어 인터페이스 준수 수준 기능과 트랜잭션과 같은 추가 기능이 포함됩니다. 레벨 1 인터페이스 준수 드라이버를 사용하면 코어 인터페이스 준수 수준의 기능 외에도 응용 프로그램에서 다음을 수행할 수 있습니다.  
  
|||  
|-|-|  
|101|데이터베이스 테이블 및 뷰의 스키마를 지정합니다(두 부분으로 구성된 이름 지정 사용). 자세한 내용은 [레벨 2 인터페이스 적합성의](../../../odbc/reference/develop-app/level-2-interface-conformance.md)세 부분으로 구성된 명명 기능 201을 참조하십시오.|  
|102|해당 ODBC 함수가 모두 동기 또는 지정된 연결에서 모두 비동기인 ODBC 함수의 진정한 비동기 실행을 호출합니다.|  
|103|스크롤 가능한 커서를 사용 하 여 그리 하면 SQL_FETCH_NEXT 이외의 *FetchOrientation* 인수를 사용 하 여 **앞으로** 전용 이외의 메서드에서 결과 집합에 대 한 액세스를 얻을 수 있습니다. (SQL_FETCH_BOOKMARK *FetchOrientation은* [레벨 2 인터페이스 적합성의](../../../odbc/reference/develop-app/level-2-interface-conformance.md)기능 204에 있습니다.)|  
|104|**SQLPrimaryKeys를**호출하여 테이블의 기본 키를 가져옵니다.|  
|105|ODBC 이스케이프 시퀀스를 통해 프로시저 호출을 통해 저장 프로시저를 사용하고 **SQLProcedureColumns** 및 SQLProcedures를 호출하여 저장 프로시저에 대한 데이터 **사전을 쿼리합니다.** (프로시저를 만들고 데이터 원본에 저장하는 프로세스는 이 문서의 범위를 벗어납니다.)|  
|106|**SQLBrowseConnect**를 호출하여 사용 가능한 서버를 대화식으로 탐색하여 데이터 원본에 연결합니다.|  
|107|SQL 문 대신 ODBC 함수를 사용하여 SQL_POSITION 및 SQL_REFRESH 있는 **SQLSetPos와** 같은 특정 데이터베이스 작업을 수행합니다.|  
|108|**SQLMoreResults**를 호출하여 일괄 처리 및 저장 프로시저에 의해 생성된 여러 결과 집합의 내용에 액세스합니다.|  
|109|**SQLEndTran에서**SQL_ROLLBACK 지정하는 기능과 함께 여러 ODBC 함수에 걸친 트랜잭션을 구분합니다.|
