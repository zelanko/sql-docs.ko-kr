---
title: 상호 운용 가능한 응용 프로그램 테스트 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], testing interoperable applications
- testing interoperable applications [ODBC]
ms.assetid: 489083cb-8430-40be-9ef2-d75b9a2eea88
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1d43c7aad2501591c497475f6c250ac33712aa7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307744"
---
# <a name="testing-interoperable-applications"></a>상호 운용 가능한 애플리케이션 테스트
상호 운용 가능한 응용 프로그램을 테스트하는 것은 시간이 많이 소요되는 비즈니스이며 새로운 드라이버가 지속적으로 시장에 출시되므로 최악의 경우 불가능합니다. 그러나 합리적인 수준의 테스트가 가능합니다. 상호 운용성이 제한적이거나 낮은 응용 프로그램은 지원이 보장되는 드라이버에 대해서만 테스트하면 됩니다. 그러나 이러한 드라이버에 대해 완전히 테스트해야 합니다.  
  
 상호 운용성이 높은 응용 프로그램은 모든 드라이버에 대해 실질적으로 테스트할 수 없습니다. 대부분의 응용 프로그램 개발자가 할 수 있는 가장 좋은 방법은 소수의 드라이버에 대해 완전히 테스트하고 몇 가지 드라이버에 대해 커서합니다. 테스트된 드라이버에는 응용 프로그램 시장에서 가장 인기 있는 DBMS에 대한 가장 인기 있는 드라이버가 포함되어야 합니다. 시장이 모든 DBMS를 다루는 경우 데스크톱 및 서버 DBMS 모두에 대한 드라이버를 테스트해야 합니다.  
  
 ODBC 응용 프로그램을 테스트할 때 의 문제 중 하나는 응용 프로그램 자체, 드라이버 관리자, 드라이버, DBMS 및 네트워크 소프트웨어 또는 게이트웨이와 관련된 구성 요소의 수입니다. 응용 프로그램을 사용하면 **SQLGetDiagField 및 SQLGetDiagRec** 을 통해 ODBC **SQLGetDiagRec**함수에서 반환된 오류 메시지를 게시하여 오류를 보다 쉽게 추적할 수 있습니다. 이러한 메시지는 오류가 발생하는 제조업체 및 구성 요소를 식별합니다. 자세한 내용은 진단 을 [참조하십시오.](../../../odbc/reference/develop-app/diagnostics.md)
