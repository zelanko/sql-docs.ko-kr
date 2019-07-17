---
title: SQL 문 처리는 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], processing
- SQL [ODBC], processing statements
- statement processing [ODBC]
- SQL statements [ODBC]
- ODBC [ODBC], SQL
ms.assetid: 96270c4f-2efd-4dc1-a985-ed7fd5658db2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dfbf23f0be369ae540dac33d33a3e3c1505d5ebe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076277"
---
# <a name="processing-a-sql-statement"></a>SQL 문 처리
프로그래밍 방식으로 SQL을 사용 하는 것에 대 한 기술에 설명 하기 전에 SQL 문을 처리 하는 방법에 대해 설명 하는 데 필요한 됩니다. 단계는 각 기술에서는 서로 다른 시간에 수행 하지만 세 가지 기술 모두에 공통적으로 적용 합니다. 다음 그림과 단계와 관련 된이 섹션의 나머지 부분 전체에서 설명 하는 SQL 문 처리 합니다.  
  
 ![SQL 문 처리 단계](../../odbc/reference/media/pr01.gif "pr01")  
  
 SQL 문을 처리 하는 DBMS 다음 5 단계를 수행 합니다.  
  
1.  DBMS는 먼저 SQL 문을 구문 분석합니다. 문이 토큰을 개별 단어로 분리, 문이 올바른 동사 및 유효한 절 등에 있도록 합니다. 이 단계에서 구문 오류 및 맞춤법 오류를 검색할 수 있습니다.  
  
2.  DBMS의 문의 유효성을 검사 합니다. 시스템 카탈로그에 대해 해당 문의 확인합니다. 문에서 지정 된 모든 테이블 데이터베이스에 없습니다? 가 모든 열 및는 열 이름이 모호? 문을 실행할 수 있는 권한이 사용자에 게 있습니까? 이 단계에서는 특정 의미 체계 오류를 검색할 수 있습니다.  
  
3.  DBMS 문에 대 한 액세스 계획을 생성합니다. 문이 수행 하는 데 필요한 단계 중 이진 표현인 액세스 계획 실행 코드에 해당 하는 DBMS는 것입니다.  
  
4.  DBMS는 액세스 계획을 최적화합니다. 액세스 계획을 수행 하는 다양 한 방법으로 탐색 합니다. 검색 속도 높일 인덱스를 사용할 수 있습니까? 해야 DBMS 먼저 테이블 A에 검색 조건을 적용 한 후 테이블 B에 조인 하거나 조인으로 시작 하며 나중에 검색 조건을 사용 해야? 테이블을 통해 순차 검색할 수 있습니다 방지할 또는 테이블의 하위 집합으로 감소? DBMS 대안을 탐색 한 후 그 중 하나를 선택 합니다.  
  
5.  DBMS는 액세스 계획을 실행 하 여 문을 실행 합니다.  
  
 SQL 문을 처리 하는 데 사용 하는 단계는 필요한 데이터베이스 액세스 및/또는 걸리는 시간의 양을 입력 다릅니다. SQL 문을 구문 분석 데이터베이스에 액세스할 필요가 없고 매우 신속 하 게 수행할 수 있습니다. 최적화에는 CPU를 많이 다른 한편으로 처리 하 고 시스템 카탈로그에 액세스 해야 합니다. 복잡 하 고 다중 테이블 쿼리를 위해 최적화 프로그램은 수천 개의 동일한 쿼리를 수행 하는 여러 가지를 탐색할 수 있습니다. 그러나 쿼리를 비효율적으로 실행 비용은 일반적으로 최적화에 소요 된 시간이 향상 된 쿼리 실행 속도가 됨 보다 더 높은 합니다. 이 기능은 동일한 최적화 액세스 계획을 사용할 수 있는 경우 계속 해 서 반복 쿼리를 수행 하에 더욱 중요 합니다.
