---
title: SQL 문 처리 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349a62034d598c1bfb44b891b91359d5ff184b7e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280523"
---
# <a name="processing-a-sql-statement"></a>SQL 문 처리
프로그래밍 방식으로 SQL을 사용하는 방법에 대해 논의하기 전에 SQL 문이 처리되는 방법에 대해 설명해야 합니다. 각 기술은 서로 다른 시간에 수행하지만 관련된 단계는 세 가지 기술 모두에 공통적입니다. 다음 그림에서는 이 섹션의 나머지 부분에서 설명하는 SQL 문을 처리하는 데 관련된 단계를 보여 주며, 이 단계는 다음과 같습니다.  
  
 ![SQL 문 처리 단계](../../odbc/reference/media/pr01.gif "pr01")  
  
 SQL 문을 처리하기 위해 DBMS는 다음 다섯 단계를 수행합니다.  
  
1.  DBMS는 먼저 SQL 문을 구문 분석합니다. 문(tokens)이라고 하는 개별 단어로 문장을 나누고 문에 유효한 동사및 유효한 절이 있는지 확인하는 등의 것입니다. 이 단계에서구문 오류 및 맞춤법 오류오류를 감지할 수 있습니다.  
  
2.  DBMS는 명령문의 유효성을 검사합니다. 시스템 카탈로그에 대해 문을 확인합니다. 명령문에 명명된 모든 테이블이 데이터베이스에 있습니까? 모든 열이 존재하며 열 이름이 모호하지 않은가요? 사용자에게 문을 실행하는 데 필요한 권한이 있습니까? 이 단계에서특정 의미 체계 오류를 검색할 수 있습니다.  
  
3.  DBMS는 명령문에 대한 액세스 계획을 생성합니다. 액세스 계획은 문을 수행하는 데 필요한 단계의 이진 표현입니다. 실행 코드와 동일한 DBMS입니다.  
  
4.  DBMS는 액세스 계획을 최적화합니다. 액세스 계획을 실행하는 다양한 방법을 살펴봅습니다. 인덱스를 사용하여 검색 속도를 높일 수 있습니까? DBMS가 먼저 테이블 A에 검색 조건을 적용한 다음 테이블 B에 조인해야 합니까, 아니면 조인으로 시작하여 나중에 검색 조건을 사용해야 합니까? 테이블을 통한 순차적 검색을 피하거나 테이블의 하위 집합으로 줄일 수 있습니까? 대안을 탐색한 후 DBMS는 그 중 하나를 선택합니다.  
  
5.  DBMS는 액세스 계획을 실행하여 문을 실행합니다.  
  
 SQL 문을 처리하는 데 사용되는 단계는 필요한 데이터베이스 액세스 량과 소요되는 시간에 따라 다릅니다. SQL 문을 구문 분석하는 것은 데이터베이스에 대한 액세스가 필요하지 않으며 매우 빠르게 수행할 수 있습니다. 반면, 최적화는 CPU집약적인 프로세스이며 시스템 카탈로그에 액세스해야 합니다. 복잡한 다중 테이블 쿼리의 경우 최적화 프로그램은 동일한 쿼리를 수행하는 수천 가지 방법을 탐색할 수 있습니다. 그러나 쿼리를 비효율적으로 실행하는 데 드는 비용이 너무 높아서 최적화에 소요되는 시간이 쿼리 실행 속도 증가에 따라 회수되는 것보다 더 많습니다. 동일한 최적화된 액세스 계획을 반복 쿼리를 수행하기 위해 반복해서 사용할 수 있는 경우 더욱 중요합니다.
