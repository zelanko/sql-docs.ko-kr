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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df7a2d036692cefcd1b2ea2338d51938a11ea85a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208424"
---
# <a name="vertical-applications"></a>수직 애플리케이션
수직 응용 프로그램에는 일반적으로 단일 DBMS에 대해 잘 정의 된 작업을 수행 합니다. 예를 들어 주문 입력 응용 프로그램을 회사의 주문을 추적 합니다. 이러한 유형의 응용 프로그램의 공통점은 데이터베이스 스키마는 응용 프로그램 개발자가 일반적으로 설계, 단일 고객에 대 한 단일 DBMS를 사용 하 여 작동 한 수가 다른 Dbms 사용 하 여 응용 프로그램 작동이,입니다.  
  
 수직 응용 프로그램은 일반적으로 트랜잭션, 스크롤 가능 커서 등의 특정 기능 필요 하기 때문에 거의 모든 Dbms을 지원 합니다. 대신, 매우 제한 된 집합을 Dbms 간에 상호 운용 가능한 경우가 많습니다. 일반적으로 세로 응용 프로그램 개발자는 시장의 큰 분수를 나타내고 나머지를 무시 하는 해당 Dbms를 지원 하도록 선택 합니다. 도 해당 테스트를 줄이기 위해 Dbms와 제품 지원 비용에 대 한 특정 드라이버를 지원 하도록 선택할 수 있습니다.  
  
 수직 응용 프로그램은 Dbms의 알려진된 집합을 지원 하기 때문에 경우에 따라 드라이버 또는 DBMS 관련 코드를 포함 합니다. 그러나 이러한 코드 유지 관리 하는 데 추가 시간이 필요 하기 때문에 가장을 최소한으로 유지 됩니다.
