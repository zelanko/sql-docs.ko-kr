---
title: "팩트 관계 및 팩트 관계 속성 정의 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
- fact dimensions [Analysis Services]
ms.assetid: d8e41724-da77-4ac1-bc42-956b5d91ea5d
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0b86ebd4da388cbaf303bcdab92fe3fce3994fe1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="define-a-fact-relationship-and-fact-relationship-properties"></a>팩트 관계 및 팩트 관계 속성 정의
  새 큐브 차원이나 새 측정값 그룹을 정의하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 팩트 차원 관계가 존재하는지 확인한 후 차원 용도 설정을 **팩트**로 지정하려고 합니다. 큐브 디자이너의 **차원 용도** 탭에서 팩트 차원 관계를 보거나 편집할 수 있습니다. 차원과 측정값 그룹 간의 팩트 관계에는 다음과 같은 제약 조건이 있습니다.  
  
-   큐브 차원은 특정 측정값 그룹에 대해 하나의 팩트 관계만 가질 수 있습니다.  
  
-   큐브 차원은 여러 측정값 그룹에 대해 별도의 팩트 관계를 가질 수 있습니다.  
  
-   관계에 대한 세분성 특성은 차원에 대한 키 특성(예: Transaction Number)이어야 하므로 차원과 팩트 테이블의 팩트 간에 일 대 일 관계가 생성됩니다.  
  
  

