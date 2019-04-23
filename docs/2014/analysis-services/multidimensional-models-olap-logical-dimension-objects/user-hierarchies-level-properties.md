---
title: 수준 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
ms.assetid: dabb7335-887b-442a-b67c-4901ba1242b7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c55a596461e03ce91a822e4578f7de56fe27f8f1
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60156530"
---
# <a name="level-properties"></a>수준 속성 
  다음 표에서는 사용자 정의 계층의 수준 속성을 나열하고 설명합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|Description|수준에 대한 설명을 포함합니다.|  
|HideMemberIf|클라이언트 애플리케이션에서 수준의 멤버를 숨길지 여부와 숨길 조건을 나타냅니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> 안 함<br /> 멤버를 숨기지 않습니다. 이것은 기본값입니다.<br /><br /> OnlyChildWithNoName<br /> 멤버가 부모의 유일한 자식이고 멤버의 이름이 비어 있는 경우 멤버를 숨깁니다.<br /><br /> OnlyChildWithParentName<br /> 멤버가 부모의 유일한 자식이고 멤버와 부모의 이름이 같을 때 멤버를 숨깁니다.<br /><br /> NoName<br /> 멤버의 이름이 비어 있을 때 멤버를 숨깁니다.<br /><br /> ParentName<br /> 멤버와 부모의 이름이 같을 때 멤버를 숨깁니다.|  
|ID|수준의 고유 ID를 포함합니다.|  
|이름|수준 이름을 포함합니다. 기본적으로 수준 이름은 원본 특성 이름과 같습니다.|  
|SourceAttribute|수준의 기반이 되는 원본 특성 이름을 포함합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [사용자 계층 속성](user-hierarchies-properties.md)  
  
  
