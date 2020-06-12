---
title: 팩트 관계 및 팩트 관계 속성 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- fact dimensions [Analysis Services]
ms.assetid: d8e41724-da77-4ac1-bc42-956b5d91ea5d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 15f67a4bdf699bbc6443fc76ce54bcfb35831827
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547095"
---
# <a name="define-a-fact-relationship-and-fact-relationship-properties"></a>팩트 관계 및 팩트 관계 속성 정의
  새 큐브 차원이나 새 측정값 그룹을 정의하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 팩트 차원 관계가 존재하는지 확인한 후 차원 용도 설정을 `Fact`로 지정하려고 합니다. 큐브 디자이너의 **차원 용도** 탭에서 팩트 차원 관계를 보거나 편집할 수 있습니다. 차원과 측정값 그룹 간의 팩트 관계에는 다음과 같은 제약 조건이 있습니다.  
  
-   큐브 차원은 특정 측정값 그룹에 대해 하나의 팩트 관계만 가질 수 있습니다.  
  
-   큐브 차원은 여러 측정값 그룹에 대해 별도의 팩트 관계를 가질 수 있습니다.  
  
-   관계에 대한 세분성 특성은 차원에 대한 키 특성(예: Transaction Number)이어야 하므로 차원과 팩트 테이블의 팩트 간에 일 대 일 관계가 생성됩니다.  
  
  
