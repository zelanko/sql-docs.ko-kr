---
title: 필터 대화 상자(Excel용 MDS 추가 기능) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b987b141-5abf-4161-a073-4cfc3e7f5aae
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 57b24ed1096078529e4e46a094737c8b37bf7020
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68092262"
---
# <a name="filter-dialog-box-mds-add-in-for-excel"></a>필터 대화 상자(Excel용 MDS 추가 기능)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서 **필터** 대화 상자를 사용하여 Excel로 로드하기 전에 MDS 관리 데이터 목록의 범위를 좁힐 수 있습니다.  
  
 이 대화 상자는 세 가지 섹션이 포함 되어 있습니다. **열**하십시오 **행**, 및 **요약**합니다.  
  
## <a name="columns"></a>열  
 **열** 섹션에서는 Excel에 표시할 특성(열)을 확인할 수 있습니다.  
  
|컨트롤 이름|Description|  
|------------------|-----------------|  
|특성 유형|특성 유형은 사용하려는 멤버 유형을 설명합니다. 대부분의 경우 **리프**입니다. 멤버 형식에 대한 자세한 내용은 [멤버&#40;Master Data Services&#41;](../../master-data-services/members-master-data-services.md)를 참조하세요.|  
|명시적 계층|**통합** 특성 유형을 선택한 경우 통합 멤버가 속하는 계층을 선택합니다. 자세한 내용은 [명시적 계층&#40;Master Data Services&#41;](../../master-data-services/explicit-hierarchies-master-data-services.md)을 참조하세요.|  
|특성 그룹|특성 그룹은 특성 하위 집합을 그룹화하는 방법입니다. 사용 가능한 특성 하위 집합을 표시하려면 특성 그룹을 선택합니다. 특성 그룹에 대한 자세한 내용은 [특성 그룹&#40;Master Data Services&#41;](../../master-data-services/attribute-groups-master-data-services.md)을 참조하세요.|  
|모두 선택|목록에 표시된 모든 특성을 선택하려면 클릭합니다.|  
|모두 지우기|목록에 표시된 선택한 특성을 지우려면 클릭합니다.<br /><br /> **이름** 및 **코드**특성은 지울 수 없습니다.|  
|위쪽 화살표/아래쪽 화살표|선택한 특성을 목록에서 위아래로 이동하려면 클릭합니다. 열이 워크시트에 왼쪽에서 오른쪽으로 표시된 순서에 따라 위에서 아래쪽의 순서로 표시됩니다.|  
  
## <a name="rows"></a>행  
 **행** 섹션에서는 Excel에 표시할 멤버(행)를 확인할 수 있습니다. 이렇게 하려면 표시되는 행을 필터링할 조건을 정의합니다.  
  
|컨트롤 이름|Description|  
|------------------|-----------------|  
|attribute|필터링할 특성을 표시합니다. 나열된 특성이 없으면 추가되지 않았기 때문입니다.<br /><br /> 참고: 워크시트에 표시 하지 않으려는 특성으로 필터링 할 수 있습니다.|  
|연산자|선택한 특성 유형에 해당하는 연산자를 표시합니다. 자세한 내용은 [필터 연산자&#40;Master Data Services&#41;](../../master-data-services/filter-operators-master-data-services.md)를 참조하세요.|  
|조건|필터링할 조건입니다.|  
|업데이트 요약|큰 데이터 세트를 사용 중일 때 로드된 데이터 양 세부 정보와 함께 **요약** 섹션을 업데이트하려면 클릭합니다.|  
|추가|**열** 섹션에서 특성을 클릭하고 **추가**를 클릭하면 특성이 필터 목록에 추가됩니다.|  
|모두 제거|목록에서 모든 필터를 제거합니다.|  
|제거|목록에서 선택한 필터를 제거합니다.|  
  
## <a name="summary"></a>요약  
 **요약** 섹션을 사용하여 데이터를 로드하기 전에 로드할 데이터 양에 대한 세부 정보를 표시합니다.  
  
|컨트롤 이름|Description|  
|------------------|-----------------|  
|Model|모델의 이름입니다.|  
|버전|버전의 이름입니다.|  
|엔터티|엔터티의 이름입니다.|  
|행|**행** 섹션에 따라 Excel에 로드되는 행 수입니다.|  
|열|**열** 섹션에서 선택한 특성에 따라 Excel에 로드되는 열 수입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [내보내기 전 데이터 필터링&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)   
 [개요: Excel로 데이터 내보내기&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  
