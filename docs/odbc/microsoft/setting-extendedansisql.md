---
title: Extendedansisql 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], setting
ms.assetid: 37b775d1-65ac-45ac-8572-454bc4e3c1a2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 330b55ef2d4fee090c453990d3fe75e6e2dacb6f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063605"
---
# <a name="setting-extendedansisql"></a>ExtendedAnsiSQL 설정
Extendedansisql을 특성을 추가 하 여 연결 문자열에서 특성을 제어할 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|Extendedansisql을 = 0 (기본값)|이 설정은 새 기능을 사용 하지 않습니다.|  
|ExtendedAnsiSQL=1|이 설정은 새 기능을 제공 합니다.|  
  
 특성을 통해 DSN에 설정할 수도 있습니다는 **고급 옵션** 제어판을 통해 DSN을 구성 하는 경우 대화 상자.  
  
 새 기능을 0 특성 설정 새 기능을 사용할 수를 1로 설정 합니다.  
  
 특성은 SQLSetConnectAttr()를 사용 하 여 설정할 수 있습니다. 특성 값을 65501 이며 앞의 표에 설명 된 대로 SQLINTEGER 값 1 또는 0으로 설정 됩니다. 전이나 연결한 후 호출할 수 있지만는 드라이버 프로세스 연결 특성 및 연결 문자열을 캐시 하는 순서 때문에 연결한 후 호출 하는 것이 좋습니다.
