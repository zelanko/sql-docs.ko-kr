---
title: "일반 관계 및 일반 관계 속성 정의 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- granularity attribute
- relationships [Analysis Services], regular relationships
ms.assetid: 840280d8-20c3-46c0-99ea-62479469c36b
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bc2ee7a49cddc8b5d6b0ce0905e2cbcd084a8897
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="define-a-regular-relationship-and-regular-relationship-properties"></a>일반 관계 및 일반 관계 속성 정의
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
새 큐브 차원이나 새 측정값 그룹을 정의하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 일반 관계가 존재하는지 확인한 후 차원 용도 설정을 **Regular**로 지정하려고 합니다. 큐브 디자이너의 **차원 용도** 탭에서 일반 차원 관계를 보거나 편집할 수 있습니다.  
  
 측정값 그룹에 대한 큐브 차원 관계를 정의할 때 해당 관계에 대한 세분성 특성도 지정합니다. 세분성 특성은 해당 차원에 대해 큐브에서 사용할 수 있는 가장 낮은 상세 수준을 정의하며 이 수준은 일반적으로 차원의 키 특성에 해당합니다. 그러나 가끔 특정 측정값 그룹의 특정 큐브 차원에 대한 세분성을 다르게 설정하려고 할 수도 있습니다. 예를 들어 Sales Quotas 또는 Budget 측정값 그룹을 사용하는 경우 Time 차원에 대한 세분성 특성을 Day 특성이 아닌 Month 특성으로 설정하려고 할 수 있습니다. 세분성 특성을 키 특성 이외의 특성으로 지정하면 차원의 다른 모든 특성이 특성 관계를 통해 다른 특성에 직간접적으로 연결되는지 확인해야 합니다. 그렇지 않으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 데이터를 제대로 집계할 수 없습니다.  
  
  
