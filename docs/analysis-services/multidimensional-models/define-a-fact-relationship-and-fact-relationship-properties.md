---
title: "팩트 관계 및 팩트 관계 속성 정의 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: fact dimensions [Analysis Services]
ms.assetid: d8e41724-da77-4ac1-bc42-956b5d91ea5d
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e1e58f9616fc40ad895858a6eb6b3cfa7e0bbed1
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="define-a-fact-relationship-and-fact-relationship-properties"></a>팩트 관계 및 팩트 관계 속성 정의
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]새 큐브 차원이 나 새 측정값 그룹을 정의할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 경우 팩트 차원 관계가 존재 확인 한 후 차원 용도 설정을 하려고 **팩트**합니다. 큐브 디자이너의 **차원 용도** 탭에서 팩트 차원 관계를 보거나 편집할 수 있습니다. 차원과 측정값 그룹 간의 팩트 관계에는 다음과 같은 제약 조건이 있습니다.  
  
-   큐브 차원은 특정 측정값 그룹에 대해 하나의 팩트 관계만 가질 수 있습니다.  
  
-   큐브 차원은 여러 측정값 그룹에 대해 별도의 팩트 관계를 가질 수 있습니다.  
  
-   관계에 대한 세분성 특성은 차원에 대한 키 특성(예: Transaction Number)이어야 하므로 차원과 팩트 테이블의 팩트 간에 일 대 일 관계가 생성됩니다.  
  
  
