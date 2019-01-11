---
title: 데이터베이스 차원 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- metadata [Analysis Services]
- dimensions [Analysis Services], characteristics
- properties [Analysis Services], dimensions
ms.assetid: 075548ef-08a3-413c-8ee0-4a074c276fcc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 34de23fca71f4dc7949a04a36323d19d35826fa9
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359825"
---
# <a name="database-dimension-properties"></a>데이터베이스 차원 속성
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], 차원의 특성 및 특성 또는 계층을 차원에 포함 된 다양 한 차원 속성의 설정에 따라 차원에 대 한 메타 데이터에 의해 정의 됩니다. 다음 표에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 차원 속성을 설명합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|`AttributeAllMemberName`|차원의 특성에 대한 All 멤버의 이름을 지정합니다.|  
|`Collation`|차원에 사용되는 데이터 정렬을 결정합니다.|  
|`CurrentStorageMode`|차원의 현재 저장소 모드를 포함합니다.|  
|`DependsOnDimension`|차원이 종속되는 다른 차원이 있는 경우 이 차원의 ID를 포함합니다.|  
|`Description`|차원에 대한 설명을 포함합니다.|  
|`ErrorConfiguration`|중복 키, 알 수 없는 키, 오류 제한, 오류 감지 시 수행 동작, 오류 로그 파일 및 Null 키 등에 대한 구성 가능한 오류 처리 설정을 제공합니다.|  
|`ID`|차원의 고유 ID를 포함합니다.|  
|`Language`|차원의 기본 언어를 지정합니다.|  
|`MdxMissingMemberMode`|MDX(Multidimensional Expressions) 문에 대해 누락된 멤버가 처리되는 방식을 결정합니다.|  
|`MiningModelID`|데이터 마이닝 차원이 연결된 마이닝 모델의 ID를 포함합니다. 차원이 마이닝 모델 차원인 경우에만 이 속성을 적용할 수 있습니다.|  
|`Name`|차원의 이름을 지정합니다.|  
|`ProactiveCaching`|차원의 자동 관리 캐싱 설정을 정의합니다.|  
|`ProcessingGroup`|처리 그룹을 지정합니다. ByAttribute 또는 ByTable 값을 지정할 수 있으며 기본값은 `ByAttribute`입니다.|  
|`ProcessingMode`|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 인덱싱 및 집계를 처리 중에 수행할지 아니면 처리 후에 수행할지를 나타냅니다.|  
|`ProcessingPriority`|지연 집계, 인덱싱 또는 클러스터링과 같은 백그라운드 작업을 수행하는 동안 차원의 처리 우선 순위를 결정합니다.|  
|`Source`|차원이 바인딩되는 데이터 원본 뷰를 식별합니다.|  
|`StorageMode`|차원의 스토리지 모드를 결정합니다.|  
|`Type`|차원의 유형을 지정합니다.|  
|`UnknownMember`|알 수 없는 멤버의 표시 여부를 나타냅니다.|  
|`UnknownMemberName`|차원의 알 수 없는 멤버에 대한 캡션을 차원의 기본 언어로 지정합니다.|  
|`WriteEnabled`|보안 권한에 따라 차원 쓰기 저장(writeback)을 사용할 수 있는지 여부를 나타냅니다.|  
  
> [!NOTE]  
>  Null 값 및 다른 데이터 무결성 문제를 작업할 때 ErrorConfiguration 및 UnknownMember 속성에 대 한 값을 설정 하는 방법에 대 한 자세한 내용은 참조 하세요. [Analysis Services 2005에서 데이터 무결성 문제 처리](https://go.microsoft.com/fwlink/?LinkId=81891)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [특성 및 특성 계층](attributes-and-attribute-hierarchies.md)   
 [사용자 계층](user-hierarchies.md)   
 [차원 관계](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [차원 & #40; Analysis Services-다차원 데이터 & #41;](dimensions-analysis-services-multidimensional-data.md)  
  
  
