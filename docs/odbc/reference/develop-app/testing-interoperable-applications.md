---
title: 상호 운용 가능한 응용 프로그램 테스트 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 59f6f5a37e65c802c8d51a1f56a40380f054e39b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114094"
---
# <a name="testing-interoperable-applications"></a>상호 운용 가능한 애플리케이션 테스트
상호 운용 가능한 응용 프로그램을 테스트 하는 것은 시간이 많이 걸리는 비즈니스 이며 새로운 드라이버가 시장에 지속적으로 표시 되기 때문에 최악의 경우 불가능 합니다. 그러나 적절 한 테스트 수준이 가능 합니다. 상호 운용성이 제한적 이거나 낮은 응용 프로그램은 지원 되는 드라이버만 테스트할 수 있어야 합니다. 그러나 이러한 드라이버에 대해 완전히 테스트 해야 합니다.  
  
 상호 운용 가능성이 매우 큰 응용 프로그램은 실제로 모든 드라이버에 대해 테스트할 수 없습니다. 대부분의 응용 프로그램 개발자는 소수의 드라이버와 cursorily에 대해 완전히 테스트 하는 것이 가장 좋습니다. 테스트 된 드라이버는 응용 프로그램 시장에서 가장 인기 있는 Dbms에 가장 인기 있는 드라이버를 포함 해야 합니다. 시장의 모든 Dbms를 포함 하는 경우 데스크톱 및 서버 Dbms에 대 한 드라이버를 테스트 해야 합니다.  
  
 ODBC 응용 프로그램 테스트의 문제 중 하나는 관련 구성 요소 수입니다. 여기에는 응용 프로그램 자체, 드라이버 관리자, 드라이버, DBMS 및 네트워크 소프트웨어나 게이트웨이가 있습니다. 응용 프로그램을 사용 하면 **SQLGetDiagField** 및 **SQLGETDIAGREC**를 통해 ODBC 함수에서 반환 된 오류 메시지를 게시 하 여 오류를 보다 쉽게 추적할 수 있습니다. 이러한 메시지는 오류가 발생 하는 제조업체 및 구성 요소를 식별 합니다. 자세한 내용은 [진단](../../../odbc/reference/develop-app/diagnostics.md)을 참조 하세요.
