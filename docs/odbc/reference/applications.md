---
title: 신청서 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- off-the-shelf applications [ODBC]
- ODBC architecture [ODBC], applications
- shrink-wrapped applications [ODBC]
- application development [ODBC], types
- custom applications [ODBC]
- virtual applications [ODBC]
- generic applications [ODBC]
ms.assetid: 39d6461f-0d24-4b7d-a723-843ade15ad73
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9184986883f64bd082ca1db472d887609d3071bd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306554"
---
# <a name="applications"></a>애플리케이션
*응용 프로그램은* 데이터에 액세스하기 위해 ODBC API를 호출하는 프로그램입니다. 많은 유형의 응용 프로그램이 가능하지만 대부분의 응용 프로그램은 이 가이드 전체에서 예제로 사용되는 세 가지 범주로 나뉩니다.  
  
-   **일반 응용 프로그램** 수축 래핑 응용 프로그램 또는 상용 응용 프로그램이라고도 합니다. 일반 응용 프로그램은 다양한 DBMS와 함께 작동하도록 설계되었습니다. 예를 들어 ODBC를 사용하여 추가 분석을 위해 데이터를 가져오는 스프레드시트 또는 통계 패키지와 ODBC를 사용하여 데이터베이스에서 메일링 리스트를 가져오는 워드 프로세서가 있습니다.  
  
     일반 응용 프로그램의 중요한 하위 범주는 PowerBuilder 또는 Microsoft ® Visual Basic® 같은 응용 프로그램 개발 환경입니다. 이러한 환경으로 구성된 응용 프로그램은 단일 DBMS에서만 작동하지만 환경 자체는 여러 DBMS에서 작동해야 합니다.  
  
     모든 일반 응용 프로그램의 공통점은 DBMS 간에 상호 운용성이 높으며 비교적 일반적인 방식으로 ODBC를 사용해야 한다는 것입니다. 상호 운용성에 대한 자세한 내용은 [상호 운용성 수준 선택을](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)참조하십시오.  
  
-   **수직 응용 프로그램** 수직 응용 프로그램은 주문 입력 또는 제조 데이터 추적과 같은 단일 유형의 작업을 수행하고 응용 프로그램 개발자가 제어하는 데이터베이스 스키마로 작업합니다. 특정 고객의 경우 응용 프로그램은 단일 DBMS와 함께 작동합니다. 예를 들어 중소기업은 dBase에서 응용 프로그램을 사용할 수 있지만 대기업에서는 Oracle에서 응용 프로그램을 사용할 수 있습니다.  
  
     응용 프로그램은 유사한 기능을 제공하는 제한된 수의 DBMS에 연결될 수 있지만 응용 프로그램이 하나의 DBMS에 연결되지 않도록 ODBC를 사용합니다. 따라서 응용 프로그램 개발자는 DBMS와 독립적으로 응용 프로그램을 판매할 수 있습니다. 수직 응용 프로그램은 개발될 때 상호 운용가능하지만 고객이 DBMS를 선택한 후 상호 운용할 수 없는 코드를 포함하도록 수정되는 경우도 있습니다.  
  
-   **사용자 지정 응용 프로그램** 사용자 지정 응용 프로그램은 단일 회사에서 특정 작업을 수행하는 데 사용됩니다. 예를 들어 대기업의 응용 프로그램은 여러 부서(각각 다른 DBMS를 사용하는)에서 판매 데이터를 수집하고 단일 보고서를 만들 수 있습니다. ODBC는 공통 인터페이스이며 프로그래머가 여러 인터페이스를 학습할 필요가 없기 때문에 사용됩니다. 이러한 응용 프로그램은 일반적으로 상호 운용할 수 없으며 특정 DBMS 및 드라이버에 기록됩니다.  
  
 ODBC를 사용하는 방법에 관계없이 모든 응용 프로그램에 공통적인 작업입니다. 종합하면 ODBC 응용 프로그램의 흐름을 크게 정의합니다. 작업은 다음과 같습니다.  
  
-   데이터 원본을 선택하고 연결합니다.  
  
-   실행을 위해 SQL 문을 제출합니다.  
  
-   결과 검색(있는 경우).  
  
-   처리 오류.  
  
-   SQL 문을 둘러싸는 트랜잭션을 커밋하거나 롤백합니다.  
  
-   데이터 원본에서 연결 끊기.  
  
 대부분의 데이터 액세스 작업은 SQL을 사용하여 수행되므로 응용 프로그램에서 ODBC를 사용하는 기본 작업은 SQL 문을 제출하고 해당 명령문에서 생성된 결과(있는 경우)를 검색하는 것입니다. 응용 프로그램에서 ODBC를 사용하는 다른 작업에는 드라이버 기능 결정 및 조정 및 데이터베이스 카탈로그 탐색이 포함됩니다.
