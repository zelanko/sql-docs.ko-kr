---
title: ASSL 개체 및 개체 특징 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 55150d0835fc0a9e3324acfb8007a1d22e9b55d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208505"
---
# <a name="assl-objects-and-object-characteristics"></a>ASSL 개체 및 개체 특징
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  ASSL(Analysis Services Scripting Language)의 개체는 개체 그룹, 상속, 명명, 확장 및 처리에 관한 특정 지침을 따릅니다.  
  
## <a name="object-groups"></a>개체 그룹  
 모든 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체에는 XML 표현이 있습니다. 개체는 다음과 같은 두 그룹으로 나뉩니다.  
  
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
  
|열거형 값|에 대 한 허용 \<Alter >|설명|  
|-----------------------|---------------------------|-----------------|  
|*ReferenceOnly*|no|요청된 개체와 포함된 모든 주요 개체에 대한 이름, ID 및 타임스탬프만을 재귀적으로 반환합니다.|  
|*ObjectProperties*|예|요청된 개체와 포함된 보조 개체를 확장합니다. 그러나 포함된 주요 개체를 반환하지는 않습니다.|  
|*ExpandObject*|no|*ObjectProperties*와 같지만 포함된 주요 개체에 대한 이름, ID 및 타임스탬프도 반환합니다.|  
|*ExpandFull*|예|요청된 개체와 포함된 모든 개체를 재귀적으로 완전히 확장합니다.|  
  
 이 ASSL 참조 섹션에서는 *ExpandFull* 표현에 대해 설명합니다. 다른 모든 **ObjectExpansion** 수준은 이 수준에서 파생됩니다.  
  
## <a name="object-processing"></a>개체 처리  
 ASSL에는 **LastProcessed**인스턴스에서 읽을 수 있지만 명령 스크립트가 인스턴스에 제출될 때는 생략되는 읽기 전용 요소 또는 속성이 있습니다(예: [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ). [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 경고나 오류 없이 읽기 전용 요소의 수정된 값을 무시합니다.  
  
 또한 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 유효성 검사 오류를 발생시키지 않고 적절하지 않거나 관련이 없는 속성을 무시합니다. 예를 들어, Y 요소의 값이 특정 값인 경우에만 X 요소가 존재해야 하는 경우 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스는 Y 요소의 값에 대해 X 요소의 유효성을 검사하는 대신 X 요소를 무시합니다.  
  
  
