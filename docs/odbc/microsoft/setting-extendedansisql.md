---
title: "ExtendedAnsiSQL 설정 | Microsoft Docs"
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
helpviewer_keywords: extendedANSISQL [ODBC], setting
ms.assetid: 37b775d1-65ac-45ac-8572-454bc4e3c1a2
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d263d57d9fecbcb03f737dc73472452367900a47
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="setting-extendedansisql"></a>ExtendedAnsiSQL 설정
ExtendedAnsiSQL 특성을 추가 하 여 연결 문자열에서 특성을 제어할 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 (기본값)|이 설정은 새 기능을 사용 하지 않습니다.|  
|ExtendedAnsiSQL = 1|이 설정은 새 기능을 사용할 수 있습니다.|  
  
 특성을 통해 DSN에 설정할 수도 있습니다는 **고급 옵션** 제어판을 통해 DSN을 구성할 때 대화 상자.  
  
 특성을로 설정 해제 합니다. 0의 새로운 기능입니다. 새 기능을 사용할 수를 1로 설정 합니다.  
  
 특성은 SQLSetConnectAttr()를 사용 하 여 설정할 수 있습니다. 특성 값 65501 되며 앞의 표에 설명 된 대로 SQLINTEGER 값 1 또는 0으로 설정 됩니다. 전이나을 연결한 후 호출 될 수 있지만 연결 특성 및 연결 문자열 드라이버 프로세스 캐시 되는 순서 때문에 연결한 후 호출 하는 것이 좋습니다.
