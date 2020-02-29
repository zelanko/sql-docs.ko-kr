---
title: 파티션 편집 또는 삭제 (Analysis Services-다차원) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying partitions
- partitions [Analysis Services], modifying
ms.assetid: fb7a64ca-d021-4926-b92d-83476fbc40a3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 089b99663753a9e9424e991ca5245c73ea577e49
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175763"
---
# <a name="edit-or-delete-partitions-analyisis-services---multidimensional"></a>파티션 편집 또는 삭제(Analyisis Services - 다차원)
  큐브 파티션은 **에서 큐브 디자이너의** 파티션 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]탭을 사용하여 수정됩니다. 
  **파티션** 탭에서는 큐브에 있는 모든 측정값 그룹의 파티션을 나열합니다. 또한 쓰기 저장(writeback)이 설정된 쓰기 저장 파티션을 나열합니다.

 측정값 그룹에 대 한 파티션을 편집 하려면 **파티션** 탭에서 측정값 그룹을 확장 합니다. 측정값 그룹의 파티션은 다음 표에 나열 된 열과 함께 테이블 형식으로 서 수로 나열 됩니다.

 연결된 측정값 그룹에 대한 설정은 원본 큐브에서 편집해야 합니다.

 대상 파티션에 원본 파티션을 병합하면 파티션이 자동으로 삭제됩니다. 원본으로 지정된 파티션은 병합이 완료된 후 삭제됩니다. 
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 에서 또는 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]의 파티션 탭에서 수동으로 파티션을 삭제할 수도 있습니다. 마우스 오른쪽 단추를 클릭한 다음 **삭제**를 선택합니다. 파티션을 삭제하면 데이터와 집계도 삭제됩니다. 예방 조치로, 나중에 이 단계를 되돌려야 하는 경우에 대비하여 데이터베이스의 최신 백업을 가지고 있어야 합니다.

> [!NOTE]
>  또는 파티션 빌드, 병합 및 삭제 태스크를 자동화하는 XMLA 스크립트를 사용할 수 있습니다. 
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 또는 예약된 태스크로 실행되는 사용자 지정 SSIS 패키지에서 XMLA 스크립트를 만들고 실행할 수 있습니다. 자세한 내용은 [Automate Analysis Services Administrative Tasks with SSIS](../instances/automate-analysis-services-administrative-tasks-with-ssis.md)를 참조하세요.

## <a name="partition-source"></a>파티션 원본
 파티션의 원본 테이블 또는 명명된 쿼리를 지정합니다. 원본 테이블을 변경하려면 셀을 클릭한 다음 찾아보기 (**...**) 단추를 클릭합니다.

 ![파티션 창의 원본 열](../media/ssas-partitionsource.png "파티션 창의 원본 열")

 파티션이 쿼리를 기반으로 하는 경우 찾아보기 (**...**) 단추를 클릭하여 쿼리를 편집합니다. 이렇게 하면 파티션의 **원본** 속성이 편집됩니다. 자세한 내용은 [다른 팩트 테이블을 사용 하도록 파티션 원본 변경](change-a-partition-source-to-use-a-different-fact-table.md)을 참조 하세요.

 데이터가 검색되는 외부 데이터 원본의 원래 원본 테이블과 동일한 구조를 가진 데이터 원본 뷰의 테이블을 지정할 수 있습니다. 원본은 큐브 데이터베이스의 모든 데이터 원본 또는 데이터 원본 뷰에 있을 수 있습니다.

## <a name="storage-settings"></a>스토리지 설정
 큐브 디자이너의 파티션 탭에서 **스토리지 설정**을 클릭하여 MOLAP, ROLAP 또는 HOLAP 스토리지에 대한 표준 설정 중 하나를 선택하거나 스토리지 모드 및 자동 관리 캐싱에 대한 사용자 지정 설정을 구성할 수 있습니다. MOLAP가 가장 빠른 쿼리 성능을 제공하기 때문에 기본값은 MOLAP입니다. 각 설정에 대한 자세한 내용은 [파티션 스토리지 설정&#40;Analysis Services - 다차원&#41;](set-partition-storage-analysis-services-multidimensional.md)을 참조하세요.

 큐브에 있는 각 측정값 그룹의 각 파티션에 대해 스토리지를 별도로 구성할 수 있습니다. 큐브 또는 측정값 그룹에 대한 기본 스토리지 설정을 구성할 수도 있습니다. 스토리지는 큐브 마법사의 **파티션** 탭에서 구성합니다.

## <a name="see-also"></a>참고 항목
 [로컬 파티션 만들기 및 관리 &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md) [집계 &#40;](designing-aggregations-analysis-services-multidimensional.md) Analysis Services&#41;[SSAS-다차원 Analysis Services 병합 파티션](merge-partitions-in-analysis-services-ssas-multidimensional.md)


