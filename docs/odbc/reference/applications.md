---
title: 응용 프로그램 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc655740701822d8c6ff9595327b906ee9a67026
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62734999"
---
# <a name="applications"></a>애플리케이션
*응용 프로그램* 는 데이터에 액세스 하는 ODBC API를 호출 하는 프로그램입니다. 다양 한 유형의 응용 프로그램을 사용할 수 있지만 대부분이이 가이드 전체에서 예제로 사용 되는 세 가지 범주로 구분 됩니다.  
  
-   **일반 응용 프로그램** 이러한 라고도 축소 래핑된 응용 프로그램 또는 상업용 응용 프로그램입니다. 일반 응용 프로그램은 다양 한 다른 Dbms 사용 하 여 작동 하도록 설계 됩니다. 스프레드시트 또는 추가 분석을 위해 데이터를 가져오는 ODBC를 사용 하는 통계 패키지 및 ODBC를 사용 하 여 데이터베이스에서 메일 그룹을 가져옵니다는 워드 프로세서를 예로 들 수 있습니다.  
  
     일반 응용 프로그램의 중요 한 subcategory는 PowerBuilder, Microsoft® Visual Basic® 등의 응용 프로그램 개발 환경 이며 이러한 환경을 사용 하 여 생성 하는 응용 프로그램은 호환 될 가능성이 단일 DBMS, 있지만 환경 자체는 여러 Dbms를 사용 하 여 작동 해야 합니다.  
  
     모든 일반 응용 프로그램의 공통점은 Dbms 간에 상호 운용성이 매우는 비교적 일반적인 방식으로 ODBC를 사용 해야입니다. 상호 운용성에 대 한 자세한 내용은 참조 하세요. [운용성 수준 선택](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)합니다.  
  
-   **수직 응용 프로그램과** 세로 응용 프로그램이 단일 유형의 주문 입력 또는 제조 데이터를 추적 하는 등의 태스크를 수행 하 고 개발자는 응용 프로그램에 의해 제어 되는 데이터베이스 스키마를 사용 하 여 작동 합니다. 특정 고객에 대해 응용 프로그램이 단일 DBMS를 사용 하 여 작동 합니다. 예를 들어 소규모 기업 대규모 비즈니스 Oracle을 사용 하 여 사용할 수도 있고 dBase를 사용 하 여 응용 프로그램을 사용할 수 있습니다.  
  
     응용 프로그램이 제한 된 수의 유사한 기능을 제공 하는 Dbms에 연결 될 수 있지만 응용 프로그램을 하나 모든 DBMS에 연결 되지 않은 방식으로 ODBC를 사용 합니다. 따라서 응용 프로그램 개발자는 DBMS에서 독립적으로 응용 프로그램을 판매할 수 있습니다. 세로 응용 프로그램에 상호 운용 가능한 개발 됩니다 있지만 고객에 DBMS를 선택한 후 noninteroperable 코드를 포함 하도록 경우에 따라 수정 되었습니다.  
  
-   **사용자 지정 응용 프로그램** 사용자 지정 응용 프로그램은 단일 회사에서 특정 작업을 수행 하는 데 사용 됩니다. 예를 들어, 대기업에서 응용 프로그램 (각각 다른 DBMS를 사용 함) 하는 여러 부서에서 영업 데이터를 수집 및 단일 보고서를 만들 수 있습니다. ODBC는 일반적인 인터페이스 이며 여러 인터페이스를 배울 필요가에서 프로그래머에 게 저장 하기 때문에 사용 됩니다. 이러한 응용 프로그램은 일반적으로 상호 운용 되지는 않습니다 및 특정 Dbms 및 드라이버에 기록 됩니다.  
  
 많은 작업을 ODBC를 사용 하는 방법에 관계 없이 모든 응용 프로그램에 공통적으로 적용 됩니다. 전체적으로 볼 때, 주로 정의 ODBC 응용 프로그램의 흐름입니다. 작업은:  
  
-   데이터 원본을 선택 하 고 연결 하는 것입니다.  
  
-   실행에 대 한 SQL 문을 제출합니다.  
  
-   (해당 되는 경우) 결과 검색 합니다.  
  
-   오류를 처리 합니다.  
  
-   커밋 또는 SQL 문을 바깥쪽 트랜잭션을 롤백합니다.  
  
-   데이터 원본에서 연결을 해제 합니다.  
  
 대부분의 데이터 액세스 작업을 수행 하 여 SQL을 사용 하 여, 응용 프로그램 ODBC 사용 하는 주 작업 이므로 SQL 문을 제출 하 고 해당 문에 의해 생성 된 결과 (있는 경우)를 검색 합니다. 응용 프로그램을 ODBC를 사용 하는 다른 작업에는 확인 및 드라이버 기능에 대 한 조정 및 데이터베이스 카탈로그를 탐색 포함 됩니다.
