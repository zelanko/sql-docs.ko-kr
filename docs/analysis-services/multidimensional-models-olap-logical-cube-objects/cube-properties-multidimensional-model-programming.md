---
title: 큐브 속성-다차원 모델 프로그래밍 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 85453133ab9facd9f3ed56ad98fa2761ac527e40
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022200"
---
# <a name="cube-properties---multidimensional-model-programming"></a>큐브 속성-다차원 모델 프로그래밍
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  큐브에는 큐브 차원 동작에 영향을 주기 위해 설정할 수 있는 많은 속성이 있습니다. 다음 표에서는 이러한 속성을 요약하여 설명합니다.  
  
> [!NOTE]  
>  일부 속성은 큐브를 만들 때 자동으로 설정되며 변경할 수 없습니다.  
  
 큐브 속성을 설정 하는 방법에 대 한 자세한 내용은 참조 [큐브 디자이너 &#40;Analysis Services-다차원 데이터&#41;](http://msdn.microsoft.com/library/a6692467-da88-4312-8b03-d812f2ae5a96)합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**AggregationPrefix**|집계 이름에 사용되는 공통 접두사를 지정합니다.|  
|**데이터 정렬**|LCID(로캘 ID)와 비교 플래그를 밑줄로 구분하여 지정합니다(예: Latin1_General_C1_AS).|  
|**DefaultMeasure**|큐브의 기본 측정값을 정의하는 MDX(Multidimensional Expressions) 식을 포함합니다.|  
|**설명**|큐브에 대한 설명을 제공합니다. 이 설명은 클라이언트 응용 프로그램에 노출될 수 있습니다.|  
|**ErrorConfiguration**|중복 키, 알 수 없는 키, 오류 제한, 오류 감지 시 수행 동작, 오류 로그 파일 및 Null 키 처리 등에 대한 구성 가능한 오류 처리 설정을 포함합니다.|  
|**EstimatedRows**|큐브의 예상 행 수를 지정합니다.|  
|**ID**|큐브의 ID(고유 식별자)를 포함합니다.|  
|**언어**|큐브의 기본 언어 식별자를 지정합니다.|  
|**이름**|큐브의 이름을 지정합니다.|  
|**ProactiveCaching**|큐브에 대한 자동 관리 캐싱 설정을 정의합니다.|  
|**ProcessingMode**|인덱싱 및 집계를 처리 중에 수행할지 아니면 처리 후에 수행할지를 나타냅니다. 옵션은 **일반** 또는 **지연**합니다.|  
|**ProcessingPriority**|지연 집계 및 지연 인덱싱과 같이 백그라운드 작업 중의 큐브 처리 우선 순위를 결정합니다. 기본값은 **0**입니다.|  
|**ScriptCacheProcessingMode**|스크립트 캐시를 처리 중에 작성할지, 아니면 처리 후에 작성할지를 나타냅니다. 옵션은 **일반** 및 **지연**합니다.|  
|**ScriptErrorHandlingMode**|오류 처리를 결정합니다. 옵션은 **IgnoreNone** 또는 **IgnoreAll**|  
|**원본**|큐브에 사용된 데이터 원본 뷰를 표시합니다.|  
|**StorageLocation**|큐브의 파일 시스템 저장소 위치를 지정합니다. 아무 위치도 지정하지 않으면 큐브 개체를 포함하는 데이터베이스에서 위치를 상속받습니다.|  
|**StorageMode**|큐브의 저장소 모드를 지정합니다. 값은 **MOLAP**, **ROLAP**, 또는 **HOLAP**합니다.|  
|**Visible**|큐브의 표시 여부를 결정합니다.|  
  
> [!NOTE]  
>  Null 값과 다른 데이터 무결성 문제를 작업할 때 ErrorConfiguration 속성에 대 한 값을 설정 하는 방법에 대 한 자세한 내용은 참조 [Analysis Services 2005에서 데이터 무결성 문제 처리](http://go.microsoft.com/fwlink/?LinkId=81891)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [자동 관리 캐싱 & #40; 파티션 & #41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)  
  
  
