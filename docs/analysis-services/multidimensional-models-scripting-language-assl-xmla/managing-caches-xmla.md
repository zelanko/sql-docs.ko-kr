---
title: "캐시 관리 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6dad9f3bb8c577ea8fb975d4f8ba4eac054f0a3e
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="managing-caches-xmla"></a>캐시 관리(XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]사용할 수는 [ClearCache](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md) 명령을 XML for Analysis (XMLA) 지정 된 차원 또는 파티션의 캐시를 지웁니다. 캐시를 지우면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 해당 개체에 대 한 캐시를 다시 작성 해야 합니다.  
  
## <a name="specifying-objects"></a>개체 지정  
 [개체](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) 의 속성은 **ClearCache** 명령은 개체 참조에는 다음과 같은 개체 중 하나에 대해서만 포함 될 수 있습니다. 따라서 다음 개체 이외의 다른 개체에 대한 개체 참조인 경우 오류가 발생합니다.  
  
 데이터베이스  
 데이터베이스 내의 모든 차원 및 파티션에 대한 캐시를 지웁니다.  
  
 차원  
 지정된 차원에 대한 캐시를 지웁니다.  
  
 Cube  
 큐브의 측정값 그룹에 포함된 모든 파티션에 대한 캐시를 지웁니다.  
  
 측정값 그룹  
 측정값 그룹에 포함된 모든 파티션에 대한 캐시를 지웁니다.  
  
 Partition  
 지정된 파티션에 대한 캐시를 지웁니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services에서 XMLA를 사용하여 개발](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
