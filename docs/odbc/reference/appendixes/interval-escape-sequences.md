---
title: "Interval 이스케이프 시퀀스 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: faaafb71236b9d3b2aa15aa67a80211bbce493a1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="interval-escape-sequences"></a>Interval 이스케이프 시퀀스
ODBC 간격 리터럴에 대 한 이스케이프 시퀀스를 사용 합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
 {*간격 리터럴*}  
  
 BNF 구문에 대 한 *간격 리터럴*, 참조는 [간격 리터럴 구문을](../../../odbc/reference/appendixes/interval-literal-syntax.md) 이 부록의 뒷부분에 나오는 섹션.  
  
 간격 리터럴의 이스케이프 시퀀스는 데이터 소스에서 interval 데이터 형식을 지 원하는 경우 지원 됩니다. 응용 프로그램 호출 해야 **SQLGetTypeInfo** 를 이러한 데이터 형식이 지원 되는지 확인 합니다.
