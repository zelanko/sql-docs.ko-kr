---
title: "수직 응용 프로그램 | Microsoft Docs"
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
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a3f4f8eca8309cb40b6ef9d2a7f9baac77c05f84
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="vertical-applications"></a>수직 응용 프로그램
수직 응용 프로그램에는 일반적으로 단일 DBMS에 대해 잘 정의 된 작업을 수행합니다. 예를 들어 주문 입력 응용 프로그램 회사의 주문을 추적 합니다. 어떻게 이러한 유형의 응용 프로그램의 공통점은 데이터베이스 스키마는 일반적으로 응용 프로그램 개발자가 설계, 단일 고객에 대 한 단일 DBMS와 함께 작동 응용 프로그램 수 다양 한 다른 Dbms 사용 하는 동안입니다.  
  
 수직 응용 프로그램은 일반적으로 트랜잭션, 스크롤 가능 커서 등의 특정 기능을 필요 하기 때문에 거의 모든 Dbms 지원 합니다. 대신 예제 규모도 더 매우 제한 된 집합을 Dbms 간에 상호 운용 가능 합니다. 일반적으로 세로 응용 프로그램 개발자는 이러한 Dbms를 나타내며 늘어나 시장 고 나머지는 무시를 지원 하도록 선택 합니다. 도 이러한 해당 테스트를 줄이기 위해 Dbms와 제품 지원 비용에 대 한 특정 드라이버를 지원 하도록 선택할 수도 있습니다.  
  
 수직 응용 프로그램 Dbms의 알려진된 집합을 지원 하기 때문에 드라이버별 또는 DBMS 관련 코드 경우가 포함 됩니다. 그러나 이러한 코드 유지 관리 하는 데 약간의 시간이 필요 하기 때문에 가장 잘를 최소한으로 유지 됩니다.
