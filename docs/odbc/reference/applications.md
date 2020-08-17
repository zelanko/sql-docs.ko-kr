---
description: 애플리케이션
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dc811b075eb698e5127fc321406bf906012c6d12
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386139"
---
# <a name="applications"></a>애플리케이션
*응용 프로그램* 은 ODBC API를 호출 하 여 데이터에 액세스 하는 프로그램입니다. 대부분의 응용 프로그램은 가능 하지만이 가이드 전체에서 예로 사용 되는 세 가지 범주에 해당 합니다.  
  
-   **일반 응용 프로그램** 이러한 기능을 축소 래핑된 응용 프로그램 또는 응용 프로그램 외부 응용 프로그램이 라고도 합니다. 제네릭 응용 프로그램은 다양 한 Dbms에서 작동 하도록 설계 되었습니다. 예를 들어 추가 분석을 위해 ODBC를 사용 하 여 데이터를 가져오고 ODBC를 사용 하 여 데이터베이스에서 메일링 리스트를 가져오는 워드 프로세서를 사용 하는 스프레드시트 또는 통계 패키지를 예로 들 수 있습니다.  
  
     일반 응용 프로그램의 중요 한 하위 범주는 PowerBuilder 또는 Microsoft® Visual Basic®와 같은 응용 프로그램 개발 환경입니다. 이러한 환경을 사용 하 여 구성 된 응용 프로그램은 단일 DBMS로만 작동 하기는 하지만 환경 자체는 여러 Dbms로 작업 해야 합니다.  
  
     모든 일반 응용 프로그램은 일반적으로 Dbms 간에 상호 운용이 가능 하 고 비교적 일반적인 방식으로 ODBC를 사용 해야 한다는 것입니다. 상호 운용성에 대 한 자세한 내용은 [상호 운용성 수준 선택](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)을 참조 하세요.  
  
-   **수직 응용 프로그램** 수직 응용 프로그램은 주문 입력 또는 추적 제조 데이터와 같은 단일 유형의 작업을 수행 하 고 응용 프로그램 개발자가 제어 하는 데이터베이스 스키마를 사용 하 여 작업 합니다. 특정 고객의 경우 응용 프로그램은 단일 DBMS로 작동 합니다. 예를 들어 소규모 비즈니스는 dBase를 사용 하는 응용 프로그램을 사용할 수 있지만, 규모가 많은 비즈니스는 Oracle과 함께 사용할 수 있습니다.  
  
     응용 프로그램은 비슷한 기능을 제공 하는 제한 된 수의 Dbms에 연결 될 수 있지만 응용 프로그램이 하나의 DBMS에 연결 되지 않는 방식으로 ODBC를 사용 합니다. 따라서 응용 프로그램 개발자는 DBMS와 독립적으로 응용 프로그램을 판매할 수 있습니다. 수직 응용 프로그램은 개발 될 때 상호 운용이 가능 하지만 고객이 DBMS를 선택 하면 상호 운용할 수 없는 코드를 포함 하도록 수정 되는 경우도 있습니다.  
  
-   **사용자 지정 응용 프로그램** 사용자 지정 응용 프로그램은 단일 회사에서 특정 작업을 수행 하는 데 사용 됩니다. 예를 들어 대기업의 응용 프로그램은 여러 디비전 (각각 다른 DBMS를 사용 하는)에서 판매 데이터를 수집 하 고 단일 보고서를 만들 수 있습니다. ODBC는 일반적인 인터페이스 이며 프로그래머가 여러 인터페이스를 학습할 필요가 없기 때문에 사용 됩니다. 이러한 응용 프로그램은 일반적으로 상호 운용할 수 없고 특정 Dbms 및 드라이버에 기록 됩니다.  
  
 많은 태스크는 ODBC를 사용 하는 방법에 관계 없이 모든 응용 프로그램에 공통적으로 사용 됩니다. 모든 ODBC 응용 프로그램의 흐름을 주로 정의 합니다. 작업은 다음과 같습니다.  
  
-   데이터 원본 선택 및 연결  
  
-   실행할 SQL 문을 전송 합니다.  
  
-   결과 검색 (있는 경우)  
  
-   처리 오류입니다.  
  
-   SQL 문을 포함 하는 트랜잭션을 커밋하거나 롤백합니다.  
  
-   데이터 원본에서 연결을 끊는 중입니다.  
  
 대부분의 데이터 액세스 작업은 SQL을 사용 하 여 수행 되므로 응용 프로그램이 ODBC를 사용 하는 기본 작업은 SQL 문을 전송 하 고 해당 문에서 생성 된 결과 (있는 경우)를 검색 하는 것입니다. 응용 프로그램이 ODBC를 사용 하는 다른 작업에는 드라이버 기능을 결정 하 고 조정 하 고 데이터베이스 카탈로그를 검색 하는 작업이 포함 됩니다.
