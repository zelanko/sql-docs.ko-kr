---
title: 처리 및 저장소 위치 (파티션 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.specifyprocessingandstorage.f1
ms.assetid: dda2dc57-923d-4db9-93a7-38e95770f3df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 73340613b14c8f0e90340b589c8b97bad7cd5599
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070645"
---
# <a name="processing-and-storage-locations-partition-wizard"></a>처리 및 스토리지 위치(파티션 마법사)
  **처리 및 스토리지 위치** 페이지를 사용하여 파티션에 대한 데이터를 저장하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스뿐만 아니라 해당 파티션을 소유하는 큐브의 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스도 지정할 수 있습니다. 원격 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스 또는 기본 스토리지 위치 이외의 스토리지 위치를 지정하여 파티션을 원격 파티션으로 정의할 수 있습니다. 원격 파티션에 대한 자세한 내용은 [원격 파티션](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)을 참조하세요.  
  
## <a name="processing-location-options"></a>처리 위치 옵션  
 **현재 서버 인스턴스**  
 현재 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에서 파티션을 처리하도록 지정합니다.  
  
 **원격 Analysis Services 데이터 원본**  
 원격 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에서 파티션을 처리하도록 지정합니다.  
  
 드롭다운 목록에서 파티션을 처리할 원격 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스를 나타내는 데이터 원본을 선택합니다.  
  
> [!NOTE]  
>  `Initial Catalog` 연결 문자열 속성이 유효한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스로 설정되어 있지 않은 데이터 원본을 선택하거나 `Initial Catalog` 연결 문자열 속성에서 지정한 데이터베이스가 원격 파티션을 지원하지 않는 경우, 즉 지정한 데이터베이스의 `MasterDatasourceID` 속성이 유효한 값으로 설정되어 있지 않은 경우 오류가 발생합니다.  
  
 **신규**  
 파티션을 처리할 원격 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스를 나타내는 새 데이터 원본을 만듭니다.  
  
## <a name="storage-location-options"></a>스토리지 위치 옵션  
 **기본 서버 위치**  
 현재 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스의 데이터 폴더를 파티션에 대한 집계 및 인덱싱 데이터의 스토리지 위치로 지정합니다.  
  
 **지정한 폴더**  
 파티션에 대한 집계 및 인덱싱 데이터의 스토리지 위치를 지정합니다.  
  
 **...**  
 **지정한 폴더** 에 대한 폴더를 선택할 수 있는 **원격 폴더 찾아보기**대화 상자를 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [파티션 마법사 F1 도움말 &#40;Analysis Services 다차원 데이터&#41;](partition-wizard-f1-help-analysis-services-multidimensional-data.md)   
 [파티션 &#40;Analysis Services 다차원 데이터&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [원격 폴더 찾아보기 대화 상자 &#40;Analysis Services 다차원 데이터&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)  
  
  
