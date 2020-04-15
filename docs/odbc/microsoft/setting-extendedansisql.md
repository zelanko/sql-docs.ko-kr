---
title: 확장 설정AnsiSQL | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b5c2e4ed4d8bd64d02fb6a62861db832f6b0898
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300803"
---
# <a name="setting-extendedansisql"></a>ExtendedAnsiSQL 설정
익스텐드AnsiSQL 특성을 추가하여 연결 문자열에서 특성을 제어할 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|익스텐드안시SQL=0(기본값)|이 설정은 새 기능을 사용할 수 없습니다.|  
|익스텐드안시SQL=1|이 설정을 사용하면 새 기능을 사용할 수 있습니다.|  
  
 제어판을 통해 DSN을 구성할 때 **고급 옵션** 대화 상자를 통해 DSN에서 속성을 설정할 수도 있습니다.  
  
 속성을 0으로 설정하면 새 기능이 비활성화됩니다. 1로 설정하면 새 기능을 사용할 수 있습니다.  
  
 SQLSetConnectAttr()를 사용하여 특성을 설정할 수도 있습니다. 특성 값은 65501이며 이전 표에 설명된 대로 SQLINTEGER 값은 1 또는 0으로 설정됩니다. 연결 전이나 후에 호출할 수 있지만 드라이버가 캐시된 연결 특성 및 연결 문자열을 처리하는 순서 때문에 연결 한 후 호출하는 것이 좋습니다.
