---
title: "특성 관계 속성 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- flexible relationships (Analysis Services)
- attributes [Analysis Services], relationships
- relationships [Analysis Services], attributes
- properties [Analysis Services], attribute relationships
- rigid relationships (Analysis Services)
ms.assetid: fce511af-66d7-42fc-bb3a-6c516f16b10e
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b43a3d43e189279b45d5347b746a047f8f76eb88
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-relationships---configure-attribute-properties"></a>특성 관계-특성 속성 구성
  다음 표에서는 특성 관계 속성을 나열하고 설명합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|Attribute|특성의 이름을 포함합니다.|  
|카디널리티|관계의 카디널리티를 나타냅니다. 사용 가능한 값은 Many(다 대 일 관계의 경우) 또는 One(일 대 일 관계의 경우)입니다. 기본값은 Many입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 카디널리티 속성은 아무런 영향을 미치지 않으며 나중에 구현할 때 사용할 수 있도록 예약됩니다.|  
|이름|특성의 이름을 포함합니다.|  
|RelationshipType|멤버 관계가 시간에 따라 변경되는지 나타냅니다. 사용 가능한 값은 Rigid(멤버 간의 관계가 시간에 따라 변경되지 않는 경우) 또는 Flexible(멤버 간의 관계가 시간에 따라 변경되는 경우)입니다. 기본값은 Flexible입니다. 유연한 관계(Flexible)로 정의하면 증분 업데이트의 일부로서 집계가 삭제되고 다시 계산됩니다. 집계는 새 멤버가 추가된 경우에만 삭제되지 않습니다. 고정된 관계로 정의할 경우 차원이 증분 업데이트되면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 집계를 보유합니다. 고정된 관계로 정의한 관계가 실제로 변경되면 증분 처리 중에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 오류를 생성합니다. 관계와 관계 속성을 적절히 지정하면 쿼리와 처리 성능이 향상됩니다.|  
|Visible|특성 관계의 표시 유형을 결정합니다. 사용 가능한 값은 True 또는 False입니다. 기본값은 True입니다.|  
  
  

