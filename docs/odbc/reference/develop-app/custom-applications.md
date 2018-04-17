---
title: 사용자 지정 응용 프로그램 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8f2a4eab813bc691fd435dc00778cbfe41c8bdcc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="custom-applications"></a>사용자 지정 응용 프로그램
사용자 지정 응용 프로그램은 일반적으로 몇 가지 Dbms에 대 한 특정 작업을 수행 합니다. 예를 들어 응용 프로그램 단일 DBMS에서 데이터를 검색할 수 있습니다 및 보고서를 생성 또는 여러 Dbms 간에 데이터를 전송할 수 있습니다. 어떻게 이러한 응용 프로그램의 공통점은 이러한 Dbms 응용 프로그램 기록 하기 전에 알려진 응용 프로그램의 수명 기간 동안 변경 되지 않을입니다.  
  
 따라서 사용자 지정 응용 프로그램 거의 또는 전혀 상호 운용성을 필요합니다. 응용 프로그램 개발자는 각 DBMS 및 해당 드라이버에 직접 코드에 대 한 단일 드라이버를 선택할 수 있습니다. 응용 프로그램 해당 드라이버의 기능을 이용 하는 드라이버 관련 코드를 안전 하 게 포함 될 수 있습니다 및 ODBC에서 지원 하지 않는 기능이 사용 하도록 기본 데이터베이스 API에 대 한 호출 게 될 수 있습니다.  
  
 대부분의 사용자 지정 응용 프로그램의 주요 상호 운용성 문제는 대상 Dbms 나중에 변경 됩니다 되는지 여부입니다. 이 경우 더 상호 운용 가능한 코드를 작성 하 여이 프로세스를 단순화할 수 있습니다. 그러나 이러한 Dbms의 경우는 거의 변경과 일반적으로 많은 양의 작업을 포함 합니다. 이 때문에 사용자 지정 응용 프로그램 개발자는 거의 선택 기능; 취약 증가 일반적으로 Dbms 변경 될 때 해당 기능을 코딩 하 선택 합니다.
