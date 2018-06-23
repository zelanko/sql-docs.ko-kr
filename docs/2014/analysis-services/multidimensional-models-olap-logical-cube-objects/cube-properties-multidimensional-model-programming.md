---
title: 큐브 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Collation property
- ID property
- ErrorConfiguration property
- cubes [Analysis Services], properties
- Description property
- DefaultMeasure property
- ProcessingMode property
- AggregationPrefix property
- EstimatedRows property
- Visible property
- StorageLocation property
- StorageMode property
- ScriptErrorHandlingMode property
- Source property
- ScriptCacheProcessingMode property
- Language property
- Name property
- properties [Analysis Services], cubes
- ProcessingPriority property
- ProactiveCaching property
ms.assetid: 72ca3387-620d-4473-8e23-7fe1f2b3d5bf
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: beae78f264c9ac0ce3aef5690f4e11e51ef191c3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081953"
---
# <a name="cube-properties"></a>큐브 속성
  큐브에는 큐브 차원 동작에 영향을 주기 위해 설정할 수 있는 많은 속성이 있습니다. 다음 표에서는 이러한 속성을 요약하여 설명합니다.  
  
> [!NOTE]  
>  일부 속성은 큐브를 만들 때 자동으로 설정되며 변경할 수 없습니다.  
  
 큐브 속성을 설정 하는 방법에 대 한 자세한 내용은 참조 [큐브 디자이너 &#40;Analysis Services-다차원 데이터&#41;](../cube-designer-analysis-services-multidimensional-data.md)합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|`AggregationPrefix`|집계 이름에 사용되는 공통 접두사를 지정합니다.|  
|`Collation`|LCID(로캘 ID)와 비교 플래그를 밑줄로 구분하여 지정합니다(예: Latin1_General_C1_AS).|  
|`DefaultMeasure`|큐브의 기본 측정값을 정의하는 MDX(Multidimensional Expressions) 식을 포함합니다.|  
|`Description`|큐브에 대한 설명을 제공합니다. 이 설명은 클라이언트 응용 프로그램에 노출될 수 있습니다.|  
|`ErrorConfiguration`|중복 키, 알 수 없는 키, 오류 제한, 오류 감지 시 수행 동작, 오류 로그 파일 및 Null 키 처리 등에 대한 구성 가능한 오류 처리 설정을 포함합니다.|  
|`EstimatedRows`|큐브의 예상 행 수를 지정합니다.|  
|`ID`|큐브의 ID(고유 식별자)를 포함합니다.|  
|`Language`|큐브의 기본 언어 식별자를 지정합니다.|  
|`Name`|큐브의 이름을 지정합니다.|  
|`ProactiveCaching`|큐브에 대한 자동 관리 캐싱 설정을 정의합니다.|  
|`ProcessingMode`|인덱싱 및 집계를 처리 중에 수행할지 아니면 처리 후에 수행할지를 나타냅니다. 옵션은 **일반** 또는 `lazy`합니다.|  
|`ProcessingPriority`|지연 집계 및 지연 인덱싱과 같이 백그라운드 작업 중의 큐브 처리 우선 순위를 결정합니다. 기본값은 **0**입니다.|  
|`ScriptCacheProcessingMode`|스크립트 캐시를 처리 중에 작성할지, 아니면 처리 후에 작성할지를 나타냅니다. 옵션은 **일반** 및 `lazy`합니다.|  
|`ScriptErrorHandlingMode`|오류 처리를 결정합니다. 사용할 수 있는 옵션은 `IgnoreNone` 또는 `IgnoreAll`입니다.|  
|`Source`|큐브에 사용된 데이터 원본 뷰를 표시합니다.|  
|`StorageLocation`|큐브의 파일 시스템 저장소 위치를 지정합니다. 아무 위치도 지정하지 않으면 큐브 개체를 포함하는 데이터베이스에서 위치를 상속받습니다.|  
|`StorageMode`|큐브의 저장소 모드를 지정합니다. 값은 `MOLAP`, `ROLAP`, 또는 `HOLAP``.`|  
|`Visible`|큐브의 표시 여부를 결정합니다.|  
  
> [!NOTE]  
>  Null 값과 다른 데이터 무결성 문제를 작업할 때 ErrorConfiguration 속성에 대 한 값을 설정 하는 방법에 대 한 자세한 내용은 참조 [Analysis Services 2005에서 데이터 무결성 문제 처리](http://go.microsoft.com/fwlink/?LinkId=81891)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [자동 관리 캐싱 &#40;파티션&#41;](partitions-proactive-caching.md)  
  
  