---
title: 수직 응용 프로그램 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300378"
---
# <a name="vertical-applications"></a>수직 애플리케이션
수직 응용 프로그램은 일반적으로 단일 DBMS에 대해 잘 정의 된 작업을 수행 합니다. 예를 들어 주문 입력 응용 프로그램은 회사의 주문을 추적 합니다. 이러한 유형의 응용 프로그램은 일반적으로 응용 프로그램 개발자가 디자인 하지만 응용 프로그램은 여러 다른 Dbms를 사용 하 여 작업할 수 있지만 단일 고객에 대해 단일 DBMS로 작동 합니다.  
  
 수직 응용 프로그램은 일반적으로 스크롤 가능 커서 또는 트랜잭션과 같은 특정 기능을 필요로 하기 때문에 모든 Dbms를 거의 지원 하지 않습니다. 대신 제한 된 Dbms 집합 간에 상호 운용성이 매우 높습니다. 일반적으로 수직 응용 프로그램 개발자는 많은 양의 시장을 나타내는 Dbms를 지원 하 고 나머지는 무시 하도록 선택 합니다. 이러한 Dbms에서 테스트 및 제품 지원 비용을 줄이기 위해 특정 드라이버를 지원 하도록 선택할 수도 있습니다.  
  
 수직 응용 프로그램은 알려진 Dbms 집합을 지원할 수 있으므로 드라이버 특정 또는 DBMS 관련 코드를 포함 하는 경우도 있습니다. 그러나 이러한 코드는 유지 관리 하는 데 시간이 더 필요 하므로 최소한으로 유지 됩니다.
