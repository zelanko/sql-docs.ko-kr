---
title: OPENXML XPath 식을 지원 되지 않는 함수를 제거 하려면 업데이트 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENXML queries
ms.assetid: b459abaf-8787-4b65-9231-ae30e5469fd0
caps.latest.revision: 17
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 87a35ea41c36250c1173df22204e6222dae0d384
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37172074"
---
# <a name="update-openxml-xpath-expressions-to-remove-unsupported-functions"></a>OPENXML XPath 식을 업데이트하여 지원되지 않는 함수를 제거합니다.
  업그레이드 관리자가 XPath 기능이 사용되는 것을 감지했습니다. 업그레이드한 후 OPENXML 기능에 대한 XPath 기능의 변경에 따른 영향을 받을 수 있습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 이제 MSXML 3.0은 OPENXML 쿼리에 사용된 XPath 식을 처리하는 기본 엔진입니다. MSXML 3.0에는 다음 함수를 더 이상 지원하지 않는 좀 더 엄격한 XPath 1.0 엔진이 있습니다.  
  
-   format-number()  
  
-   formatNumber()  
  
-   current()  
  
-   element-available()  
  
-   function-available()  
  
-   system-property()  
  
## <a name="corrective-action"></a>수정 동작  
 format-number() 및 formatNumber()의 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)]를 사용합니다. 위에 나온 지원되지 않는 다른 함수의 경우에는 직접적인 해결 방법이 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
