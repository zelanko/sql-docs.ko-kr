---
title: Extendedansisql을 설정 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063605"
---
# <a name="setting-extendedansisql"></a>ExtendedAnsiSQL 설정
특성은 Extendedansisql을 특성을 추가 하 여 연결 문자열에서 제어할 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|Extendedansisql을 = 0 (기본값)|이 설정은 새 기능을 사용 하도록 설정 하지 않습니다.|  
|Extendedansisql을 = 1|이 설정을 통해 새로운 기능을 사용할 수 있습니다.|  
  
 제어판을 통해 DSN을 구성할 때 **고급 옵션** 대화 상자를 통해 dsn에서 특성을 설정할 수도 있습니다.  
  
 특성을 0으로 설정 하면 새 기능을 사용할 수 없습니다. 1로 설정 하면 새 기능을 사용할 수 있습니다.  
  
 SQLSetConnectAttr ()를 사용 하 여 특성을 설정할 수도 있습니다. 특성 값이 65501이 고 앞의 표에 설명 된 대로 SQLINTEGER 값 1 또는 0으로 설정 됩니다. 연결 하기 전이나 후에 호출할 수 있지만 드라이버가 캐시 된 연결 특성 및 연결 문자열을 처리 하는 순서 때문에 연결 후에 호출 하는 것이 좋습니다.
