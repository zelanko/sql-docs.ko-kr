---
title: 일반 (파티션 속성 대화 상자) (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.partitionproperties.general.f1
ms.assetid: efb505be-354f-4d23-8f2d-3e76fa50d27b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05d840d4e43d9856dedeb3fd446c8158f23275b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081069"
---
# <a name="general-partition-properties-dialog-box-ssms"></a>일반(파티션 속성 대화 상자)(SSMS)
  SQL Server Management Studio에서 **파티션 속성** 대화 상자의 **일반** 페이지를 사용하여 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에 있는 큐브에 대해 측정값 그룹 내 파티션의 일반 속성을 설정할 수 있습니다.  
  
## <a name="options"></a>옵션  
  
|용어|정의|  
|----------|----------------|  
|**집계 디자인 ID**|파티션에서 사용하는 집계 디자인의 식별자를 표시합니다.|  
|**Aggregation Prefix**|파티션에 포함된 집계 인스턴스의 기본 접두사를 표시합니다.|  
|**타임 스탬프 만들기**|파티션이 생성된 날짜와 시간을 표시합니다.|  
|**현재 스토리지 모드**|파티션의 현재 스토리지 모드를 표시합니다.<br /><br /> 참고: 이 모드는 파티션의 자동 관리 캐싱 설정에 따라 달라질 수 있습니다. 자동 관리 캐싱에 대한 자세한 내용은 [자동 관리 캐싱&#40;파티션&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)을 참조하세요.|  
|**설명**|파티션에 대한 설명을 변경하려면 입력합니다.|  
|**예상 행 수**|파티션이 나타내는 기본 데이터 원본에 예상되는 행 수를 입력합니다. 이 값은 파티션을 처리하는 동안 해당 처리에 필요한 시간과 스토리지를 예상하는 데 사용됩니다.|  
|**예상 크기**|파티션의 예상 크기를 표시합니다.|  
|**ID**|파티션의 식별자를 표시합니다.|  
|**마지막 처리**|파티션을 마지막으로 처리한 날짜와 시간을 표시합니다.|  
|**최종 스키마 업데이트**|파티션의 메타데이터가 마지막으로 업데이트된 날짜와 시간을 표시합니다.|  
|**이름**|파티션 이름을 표시합니다.|  
|**처리 모드**|파티션의 처리 모드를 선택합니다. 개체의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 처리 모드에 대 한 자세한 내용은 [다차원 모델 개체 처리](multidimensional-models/processing-a-multidimensional-model-analysis-services.md)를 참조 하세요.|  
|**원격 데이터 원본 ID**|파티션의 원본 데이터를 검색할 원격 데이터 원본의 식별자를 표시합니다.<br /><br /> 참고: 이 속성은 원격 파티션에 대한 값만 포함합니다.|  
|**조각**|파티션이 나타내는 데이터 조각을 식별하는 식을 표시합니다.|  
|**원본**|파티션에 대한 원본 데이터를 제공하는 테이블 또는 쿼리를 표시합니다.|  
|**시스템 상태**|파티션의 현재 처리 상태를 표시합니다.|  
|**스토리지 위치**|파티션에 대한 데이터가 저장된 폴더를 표시합니다.<br /><br /> 참고: 이 속성은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 대해 기본 스토리지 위치 이외의 스토리지 위치가 지정된 경우에만 값을 포함합니다.|  
|**형식**|파티션의 유형을 표시합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [파티션 &#40;Analysis Services 다차원 데이터&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [원격 파티션](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)   
 [파티션 속성 대화 상자 &#40;SSMS&#41;](partition-properties-dialog-box-ssms.md)   
 [선택 &#40;파티션 속성 대화 상자&#41; &#40;SSMS&#41;](selection-partition-properties-dialog-box-ssms.md)   
 [자동 관리 캐싱 &#40;파티션 속성 대화 상자&#41; &#40;SSMS&#41;](proactive-caching-partition-properties-dialog-box-ssms.md)   
 [SSAS-다차원&#41;&#40;큐브, 파티션 및 차원 처리에 대 한 오류 구성](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
  
