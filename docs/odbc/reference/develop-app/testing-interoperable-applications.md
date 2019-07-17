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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114094"
---
# <a name="testing-interoperable-applications"></a>상호 운용 가능한 애플리케이션 테스트
상호 운용 가능한 응용 프로그램 테스트는 시간이 오래 걸리는 가장 좋은 비즈니스 및 새 드라이버 시장에서 지속적으로 표시 되므로 최악의 불가능 합니다. 단, 적정 수준의 테스트 가능 합니다. 지원 보장 되 해당 드라이버에 대 한 제한 또는 낮은 상호 운용성을 사용 하 여 응용 프로그램을 테스트만 필요 합니다. 그러나 이러한 완벽 하 게 테스트 해야 이러한 드라이버에 대 한 합니다.  
  
 모든 드라이버에 대 한 실질적으로 매우 상호 운용 가능한 응용 프로그램을 테스트할 수 없습니다. 대부분의 응용 프로그램 개발자가 수행할 수 있는 최상의 cursorily 몇 개 더 적은 수의 드라이버에 대해 완벽 하 게 테스트 하는 것입니다. 테스트 드라이버; 응용 프로그램의 시장에서 가장 인기 있는 Dbms에 대 한 가장 인기 있는 드라이버를 포함 해야 합니다. 시장의 모든 Dbms를 포함 하는 경우 데스크톱 및 서버 모두 Dbms 용 드라이버를 테스트 해야 합니다.  
  
 ODBC 응용 프로그램 테스트의 문제 중 하나는 관련 된 구성 요소의 수가: 자체 응용 프로그램, 드라이버 관리자, 드라이버, DBMS 및 가능한 경우 네트워크 소프트웨어 또는 게이트웨이. 응용 프로그램 수 있도록 ODBC 함수에서 반환 된 오류 메시지를 게시 하 여 오류를 추적 하기 쉽도록 **SQLGetDiagField** 하 고 **SQLGetDiagRec**합니다. 이러한 메시지는 제조업체와 오류가 발생 하는 구성 요소를 식별 합니다. 자세한 내용은 [진단](../../../odbc/reference/develop-app/diagnostics.md)합니다.
