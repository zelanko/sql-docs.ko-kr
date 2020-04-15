---
title: 수직 응용 프로그램 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc88f38fd1ffe8b2ee0033ad0a2abc4f15fd5cf3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300378"
---
# <a name="vertical-applications"></a>수직 애플리케이션
수직 응용 프로그램은 일반적으로 단일 DBMS에 대해 잘 정의된 작업을 수행합니다. 예를 들어 주문 입력 응용 프로그램은 회사의 주문을 추적합니다. 이러한 유형의 응용 프로그램의 공통점은 데이터베이스 스키마는 일반적으로 응용 프로그램 개발자가 설계하고 응용 프로그램이 여러 DBMS에서 작동할 수 있지만 단일 고객을 위한 단일 DBMS에서 작동한다는 것입니다.  
  
 세로 응용 프로그램에는 일반적으로 스크롤 가능한 커서 나 트랜잭션과 같은 특정 기능이 필요하므로 모든 DBMS를 거의 지원하지 않습니다. 대신 제한된 DBMS 집합 간에 상호 운용성이 높은 경향이 있습니다. 일반적으로 수직 응용 프로그램 개발자는 시장의 큰 부분을 나타내는 DBMS를 지원하고 나머지는 무시하도록 선택합니다. 테스트 및 제품 지원 비용을 줄이기 위해 해당 DBMS에 대한 특정 드라이버를 지원하도록 선택할 수도 있습니다.  
  
 세로 응용 프로그램은 알려진 DBMS 집합을 지원할 수 있으므로 드라이버별 또는 DBMS 관련 코드를 포함하는 경우도 있습니다. 그러나 이러한 코드는 유지 관리 하는 데 추가 시간이 필요 하기 때문에 최소한으로 유지 하는 것이 좋습니다.
