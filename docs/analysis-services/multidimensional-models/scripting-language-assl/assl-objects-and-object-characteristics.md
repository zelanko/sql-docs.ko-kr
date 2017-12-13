---
title: "ASSL 개체 및 개체 특징 | Microsoft Docs"
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
- reference exceptions [Analysis Services Scripting Language]
- ASSL, objects
- inheritance [Analysis Services Scripting Language]
- localized names [Analysis Services Scripting Language]
- objects [Analysis Services Scripting Language]
- names [Analysis Services Scripting Language]
- Analysis Services Scripting Language, objects
- expansion [Analysis Services Scripting Language]
ms.assetid: 6e5c28b5-c0bc-4ccd-82e5-e174bbb71386
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2a3dc1f15f445d24522911a8d21b32e8d8ac6ca3
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="assl-objects-and-object-characteristics"></a>ASSL 개체 및 개체 특징
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]개체의 Analysis Services Scripting Language (ASSL) 개체 그룹, 상속, 명명, 확장 및 처리에 관한 특정 지침을 따릅니다.  
  
## <a name="object-groups"></a>개체 그룹  
 모든 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체는 XML 표현이 있습니다. 개체는 다음과 같은 두 그룹으로 나뉩니다.  
  
 **주요 개체**  
 주요 개체는 독립적으로 만들고 변경하고 삭제할 수 있습니다. 주요 개체는 다음과 같습니다.  
  
-   서버  
  
-   데이터베이스  
  
-   차원  
  
-   큐브  
  
-   측정값 그룹  
  
-   파티션  
  
-   큐브 뷰  
  
-   마이닝 모델  
  
-   역할  
  
-   서버 또는 데이터베이스에 연결된 명령  
  
-   데이터 원본  
  
 주요 개체에는 기록 및 상태를 추적할 수 있는 다음과 같은 속성이 있습니다.  
  
-   **CreatedTimestamp**  
  
-   **LastSchemaUpdate**  
  
-   **LastProcessed** (필요한 경우)  
  
> [!NOTE]  
>  개체를 주요 개체로 분류하는 작업은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스와 개체 정의 언어에서 해당 개체가 처리되는 방법에 영향을 줍니다. 그러나 이 분류가 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 관리 및 개발 도구에서 이러한 개체를 독립적으로 만들거나 수정하거나 삭제할 수 있다는 것을 보장하지는 않습니다.  
  
 **보조 개체**  
 보조 개체는 주요 부모 개체를 만들거나 변경하거나 삭제하는 작업의 일부로서만 만들거나 변경하거나 삭제할 수 있습니다. 보조 개체는 다음과 같습니다.  
  
-   계층 및 수준  
  
-   특성  
  
-   측정값  
  
-   마이닝 모델 열  
  
-   큐브에 연결된 명령  
  
-   Aggregations  
  
## <a name="object-expansion"></a>개체 확장  
 **ObjectExpansion** 제한은 서버에서 반환된 ASSL XML의 확장 수준을 제어하는 데 사용할 수 있습니다. 이 제한에는 다음 표에 나열된 옵션이 포함됩니다.  
  
|열거형 값|에 대 한 허용 \<Alter >|Description|  
|-----------------------|---------------------------|-----------------|  
|*ReferenceOnly*|아니요|요청된 개체와 포함된 모든 주요 개체에 대한 이름, ID 및 타임스탬프만을 재귀적으로 반환합니다.|  
|*ObjectProperties*|예|요청된 개체와 포함된 보조 개체를 확장합니다. 그러나 포함된 주요 개체를 반환하지는 않습니다.|  
|*ExpandObject*|아니요|*ObjectProperties*와 같지만 포함된 주요 개체에 대한 이름, ID 및 타임스탬프도 반환합니다.|  
|*ExpandFull*|예|요청된 개체와 포함된 모든 개체를 재귀적으로 완전히 확장합니다.|  
  
 이 ASSL 참조 섹션에서는 *ExpandFull* 표현에 대해 설명합니다. 다른 모든 **ObjectExpansion** 수준은 이 수준에서 파생됩니다.  
  
## <a name="object-processing"></a>개체 처리  
 ASSL에는 읽기 전용 요소 또는 속성이 포함 됩니다 (예를 들어 **LastProcessed**)에서 읽을 수 있는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 있지만 명령 스크립트가 인스턴스에 제출 될 때는 생략 되는 합니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 경고나 오류 없이 읽기 전용 요소의 수정된 값을 무시합니다.  
  
 또한 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 유효성 검사 오류를 발생시키지 않고 적절하지 않거나 관련이 없는 속성을 무시합니다. 예를 들어, Y 요소의 값이 특정 값인 경우에만 X 요소가 존재해야 하는 경우 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스는 Y 요소의 값에 대해 X 요소의 유효성을 검사하는 대신 X 요소를 무시합니다.  
  
  
