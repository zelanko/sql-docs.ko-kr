---
title: 수준 1 인터페이스 규칙 | Microsoft Docs
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
ms.openlocfilehash: 29f59cf06eac1ce0f6589ad9c7cba8491e8383b5
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363427"
---
# <a name="level-1-interface-conformance"></a>수준 1 인터페이스 적합성
수준 1 인터페이스 규칙 수준에는 OLTP 관계형 DBMS에서 일반적으로 사용할 수 있는 핵심 인터페이스 규칙 수준 기능 및 트랜잭션과 같은 추가 기능이 포함 됩니다. 수준 1 인터페이스 준수 드라이버를 통해 응용 프로그램은 핵심 인터페이스 규칙 수준의 기능 외에도 다음 작업을 수행할 수 있습니다.  
  
|기능 번호|설명|  
|-|-|  
|101|데이터베이스 테이블 및 뷰 (두 부분으로 구성 된 이름 지정)의 스키마를 지정 합니다. 자세한 내용은 [수준 2 인터페이스 규칙](../../../odbc/reference/develop-app/level-2-interface-conformance.md)의 세 부분으로 구성 된 이름 지정 기능 201을 참조 하세요.|  
|102|지정 된 연결에서 해당 ODBC 함수가 모두 동기 이거나 모두 비동기 인 경우 ODBC 함수에 대해 진정한 비동기 실행을 호출 합니다.|  
|103|스크롤 가능 커서를 사용 하 여 SQL_FETCH_NEXT 이외의 *Fetchorientation* 인수로 **sqlfetchscroll** 을 호출 하 여 앞 으로만 이동이 아닌 다른 방법으로 결과 집합에 액세스할 수 있습니다. SQL_FETCH_BOOKMARK *Fetchorientation* 는 [수준 2 인터페이스 규칙](../../../odbc/reference/develop-app/level-2-interface-conformance.md)의 기능 204에 있습니다.|  
|104|**Sqlprimarykeys**를 호출 하 여 테이블의 기본 키를 가져옵니다.|  
|105|프로시저 호출에 대해 ODBC 이스케이프 시퀀스를 통해 저장 프로시저를 사용 하 고 **SQLProcedureColumns** 및 **sqlprocedures**를 호출 하 여 저장 프로시저에 대 한 데이터 사전을 쿼리 합니다. (프로시저를 만들어 데이터 소스에 저장 하는 프로세스는이 문서의 범위를 벗어납니다.)|  
|106|**SQLBrowseConnect**을 호출 하 여 사용 가능한 서버를 대화식으로 검색 하 여 데이터 원본에 연결 합니다.|  
|107|SQL 문 대신 ODBC 함수를 사용 하 여 특정 데이터베이스 작업을 수행 합니다. **SQLSetPos** 는 SQL_POSITION 및 SQL_REFRESH입니다.|  
|108|**SQLMoreResults**를 호출 하 여 일괄 처리 및 저장 프로시저에 의해 생성 된 여러 결과 집합의 콘텐츠에 대 한 액세스 권한을 얻습니다.|  
|109|진정한 원자성 및 **Sqlendtran**에서 SQL_ROLLBACK를 지정 하는 기능을 사용 하 여 여러 ODBC 함수에 걸친 트랜잭션을 구분 합니다.|
