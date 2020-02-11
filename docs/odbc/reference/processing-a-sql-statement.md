---
title: SQL 문 처리 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076277"
---
# <a name="processing-a-sql-statement"></a>SQL 문 처리
SQL을 프로그래밍 방식으로 사용 하는 방법에 대해 설명 하기 전에 SQL 문을 처리 하는 방법을 설명 해야 합니다. 각 기술이 각기 다른 시간에 수행 하는 경우에도 관련 된 단계는 세 가지 기술 모두에 공통적입니다. 다음 그림은이 섹션의 나머지 부분에서 설명 하는 SQL 문 처리와 관련 된 단계를 보여 줍니다.  
  
 ![SQL 문 처리 단계](../../odbc/reference/media/pr01.gif "pr01")  
  
 DBMS는 SQL 문을 처리 하기 위해 다음 5 단계를 수행 합니다.  
  
1.  DBMS는 먼저 SQL 문을 구문 분석 합니다. 토큰 이라는 개별 단어로 문을 분리 하 여 문에 유효한 동사와 유효한 절이 있는지를 확인할 수 있습니다. 이 단계에서는 구문 오류 및 맞춤법 오류를 검색할 수 있습니다.  
  
2.  DBMS에서 문의 유효성을 검사 합니다. 시스템 카탈로그에 대해 문을 확인 합니다. 문에 이름이 지정 된 모든 테이블이 데이터베이스에 존재 합니까? 모든 열이 존재 하며 열 이름이 명확 하지 않나요? 사용자에 게 문을 실행 하는 데 필요한 권한이 있나요? 이 단계에서는 특정 의미 오류를 검색할 수 있습니다.  
  
3.  DBMS는 문에 대 한 액세스 계획을 생성 합니다. 액세스 계획은 문을 수행 하는 데 필요한 단계를 이진 방식으로 표현한 것입니다. 실행 코드에 해당 하는 DBMS입니다.  
  
4.  DBMS는 액세스 계획을 최적화 합니다. 액세스 계획을 수행 하는 다양 한 방법을 탐색 합니다. 검색 속도를 높이는 데 인덱스를 사용할 수 있나요? DBMS에서 먼저 검색 조건을 테이블 A에 적용 한 다음 테이블 B에 조인 해야 합니다. 그렇지 않으면 나중에 조인으로 시작 하 고 나중에 검색 조건을 사용 해야 합니다. 테이블에 대 한 순차 검색을 테이블의 하위 집합으로 피하고 축소할 수 있나요? 대체 항목을 탐색 한 후 DBMS에서 하나를 선택 합니다.  
  
5.  DBMS는 액세스 계획을 실행 하 여 문을 실행 합니다.  
  
 SQL 문을 처리 하는 데 사용 되는 단계는 필요한 데이터베이스 액세스의 양과 소요 되는 시간에 따라 다릅니다. SQL 문을 구문 분석 하는 것은 데이터베이스에 대 한 액세스가 필요 하지 않으며 매우 빠르게 수행할 수 있습니다. 반면에 최적화는 CPU를 많이 사용 하는 프로세스 이며 시스템 카탈로그에 대 한 액세스가 필요 합니다. 복잡 한 multitable 쿼리를 위해 최적화 프로그램은 수천 개의 다른 방법을 탐색 하 여 동일한 쿼리를 수행할 수 있습니다. 그러나 쿼리를 비효율적으로 실행 하는 비용은 일반적으로 증가 하므로 최적화에 소요 된 시간이 증가 하 여 쿼리 실행 속도가 향상 됩니다. 이와 같은 최적화 된 액세스 계획을 반복 쿼리를 수행 하는 데 사용할 수 있는 경우에도 훨씬 더 중요 합니다.
