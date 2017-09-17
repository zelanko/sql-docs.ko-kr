---
title: "상호 운용 가능한 응용 프로그램 테스트 | Microsoft Docs"
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
- interoperability [ODBC], testing interoperable applications
- testing interoperable applications [ODBC]
ms.assetid: 489083cb-8430-40be-9ef2-d75b9a2eea88
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d36c443cb6bc4a189006a3d63e90deead3f11e66
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="testing-interoperable-applications"></a>상호 운용 가능한 응용 프로그램 테스트
상호 운용 가능한 응용 프로그램 테스트 계산은 아무리 잘는 시간이 많이 걸리는 비즈니스 및 새 드라이버 시장에 지속적으로 표시 되기 때문에 최악의 불가능 합니다. 그러나 테스트는 적절 한 수준의 수는 없습니다. 해당 드라이버를 지원 하도록 보장 됩니다에 대 한 제한 된 또는 낮은 상호 운용성와 응용 프로그램을 테스트만 필요 합니다. 그러나 이러한 완벽 하 게 테스트 해야 이러한 드라이버에 대 한 합니다.  
  
 모든 드라이버에 대해 항상 상호 운용 가능한 응용 프로그램을 실제로 테스트할 수 없습니다. 대부분의 응용 프로그램 개발자가 작업을 수행할 수 있는 최상의 cursorily 몇 개 더 적은 수의 드라이버에 대해 완벽 하 게 테스트 하는 것입니다. 응용 프로그램의 시장;에서 가장 인기 있는 Dbms에 대 한 가장 인기 있는 드라이버를 포함 해야 테스트 한 드라이버 시장 모든 Dbms를 포함 하는 경우 Dbms 데스크톱 및 서버 모두에 대 한 드라이버를 테스트 해야 합니다.  
  
 ODBC 응용 프로그램 테스트 문제 중 하나는 관련 된 구성 요소 수가: 응용 프로그램 자체, 드라이버 관리자, 드라이버, DBMS 및 수 있는 네트워크 소프트웨어 또는 게이트웨이 합니다. 응용 프로그램 쉽게 만들 수를 통해 ODBC 함수에서 반환 된 오류 메시지를 게시 하 여 오류를 추적 **SQLGetDiagField** 및 **SQLGetDiagRec**합니다. 이러한 메시지는 제조업체 및 오류가 발생 하는 구성 요소를 식별 합니다. 자세한 내용은 참조 [진단](../../../odbc/reference/develop-app/diagnostics.md)합니다.
