---
title: Analysis Services 테이블 형식 모델 테이블 및 열 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f7a9844032ad24de1c81144ca742bfb185aecc36
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072160"
---
# <a name="tables-and-columns"></a>테이블 및 열 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  테이블 가져오기 마법사를 사용하여 테이블과 데이터를 모델에 추가한 후에는 데이터의 새 열 추가, 테이블 간의 관계 만들기, 데이터를 확장하는 계산 정의, 보기 쉽게 테이블의 데이터 필터링 및 정렬 등을 수행하여 테이블 작업을 시작할 수 있습니다.  
  
 이 항목의 섹션:  
  
-   [이점](#bkmk_benefits)  
  
-   [테이블 및 열 작업](#bkmk_working)  
  
-   [관련 작업](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> 이점  
 테이블 형식 모델에서 테이블은 열 및 기타 메타데이터가 정의되는 프레임 워크를 제공합니다. 테이블에는 다음이 포함됩니다.  
  
 **테이블 정의**  
 테이블 정의에는 열 집합이 포함됩니다. 데이터 원본에서 열을 가져오거나 계산 열과 같이 열을 수동으로 추가할 수 있습니다.  
  
 **테이블 메타데이터**  
 관계, 측정값, 역할, 큐브 뷰 및 붙여넣은 데이터는 모두 테이블 컨텍스트 내에서 개체를 정의하는 메타데이터입니다.  
  
 **데이터**  
 테이블 가져오기 마법사를 사용하거나 계산 열에서 새 데이터를 만들어 테이블을 처음 가져오면 데이터가 테이블 열에 채워집니다. 원본에서 데이터가 변경되거나 모델이 메모리에서 제거되면 처리 작업을 실행하여 데이터를 테이블에 다시 채워야 합니다.  
  
##  <a name="bkmk_working"></a> 테이블 및 열 작업  
 모델 디자이너에서는 새 모델 테이블을 직접 만들지 않습니다. 다른 데이터 원본에서 데이터를 가져오거나 복사할 때마다 새 탭이 자동으로 만들어집니다. 모델 디자이너의 각 탭에는 다음을 포함할 수 있는 데이터 테이블이 하나씩 들어 있습니다.  
  
-   관계형 데이터베이스의 단일 테이블이나 뷰 또는 Analysis Services 큐브와 같은 관계형이 아닌 다른 원본  
  
-   피드 또는 텍스트 파일에서 가져온 테이블 형식의 데이터 집합  
  
-   복사하여 테이블에 붙여넣은 관계형 데이터 및 테이블 형식(HTML) 데이터의 조합  
  
 데이터를 가져오면 데이터의 각 테이블이나 뷰, 시트 또는 파일이 모델 디자이너에 테이블로 추가됩니다. 다양한 원본의 데이터를 각각 별도의 탭에 추가하는 것이 일반적지만 **붙여넣기** 및 **추가하여 붙여넣기**를 사용하여 데이터를 단일 테이블로 결합할 수도 있습니다. 자세한 내용은 [데이터 복사 및 붙여넣기](../../analysis-services/tabular-models/ssas-import-data-copy-and-paste-data.md)합니다.  
  
 필요한 데이터를 모두 추가한 후 테이블 간의 추가 관계를 만들거나, 다른 테이블의 관련 값을 조회 또는 참조하거나, 새 계산 열을 추가하여 파생 값을 만들 수 있습니다.  
  
 매우 큰 데이터 집합을 작업하는 경우 특정 데이터가 표시되지 않도록 필터링할 수 있습니다. 다른 순서로 데이터를 정렬할 수도 있습니다. 모델 디자이너를 사용하면 필터, 정렬 및 숨기기 기능을 사용하여 전체 열 또는 특정 데이터를 표시하거나 표시하지 않을 수 있습니다.  
  
##  <a name="bkmk_related_tasks"></a> 관련 작업  
  
|항목|Description|  
|-----------|-----------------|  
|[테이블에 열 추가](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)|원본 열을 테이블 정의에 추가하는 방법을 설명합니다.|  
|[열 삭제](../../analysis-services/tabular-models/delete-a-column-ssas-tabular.md)|모델 디자이너 또는 테이블 속성 대화 상자를 사용하여 모델 테이블 열을 삭제하는 방법에 대해 설명합니다.|  
|[테이블, 열 또는 행 필터 매핑 변경](../../analysis-services/tabular-models/change-table-column-or-row-filter-mappings-ssas-tabular.md)|테이블 속성 편집 대화 상자에서 테이블 미리 보기 또는 SQL 쿼리 편집기를 사용하여 테이블, 열 또는 행 필터 매핑을 변경하는 방법을 설명합니다.|  
|[시간 인텔리전스에 사용할 날짜 테이블로 표시 지정](../../analysis-services/tabular-models/specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md)|날짜 테이블로 표시 대화 상자를 사용하여 날짜 테이블 및 고유 식별자 열을 지정하는 방법을 설명합니다. 날짜 테이블 및 고유 식별자 지정은 DAX 수식에서 시간 인텔리전스 기능을 사용할 경우에 필요합니다.|  
|[테이블 추가](../../analysis-services/tabular-models/add-a-table-ssas-tabular.md)|기존 데이터 원본 연결을 사용하여 데이터 원본의 테이블을 추가하는 방법을 설명합니다.|  
|[테이블 삭제](../../analysis-services/tabular-models/delete-a-table-ssas-tabular.md)|모델 작업 영역 데이터베이스에서 더 이상 필요하지 않은 테이블을 삭제하는 방법을 설명합니다.|  
|[테이블 또는 열 이름 바꾸기](../../analysis-services/tabular-models/rename-a-table-or-column-ssas-tabular.md)|모델에서 쉽게 식별할 수 있도록 테이블 또는 열의 이름을 바꾸는 방법을 설명합니다.|  
|[열 데이터 형식 설정](../../analysis-services/tabular-models/set-the-data-type-of-a-column-ssas-tabular.md)|열의 데이터 형식을 변경하는 방법을 설명합니다. 데이터 형식은 열의 데이터가 저장되고 표시되는 방법을 정의합니다.|  
|[열 숨기기 또는 고정](../../analysis-services/tabular-models/hide-or-freeze-columns-ssas-tabular.md)|표시 하지 않으려는 열을 숨기는 방법 및 영역의 (잠금) 특정 열을 동결 하 여 모델의 다른 영역으로 스크롤할 때 모델의 영역을 표시 유지 하는 방법을 설명 합니다.|  
|[계산 열](../../analysis-services/tabular-models/ssas-calculated-columns.md)|이 섹션의 항목에서는 계산 열을 사용하여 집계된 데이터를 모델에 추가하는 방법을 설명합니다.|  
|[데이터 필터링 및 정렬](http://msdn.microsoft.com/library/55ebd7a6-2458-4398-911f-fcfeb2413f1b)|이 섹션의 항목에서는 모델 디자이너의 컨트롤을 사용하여 데이터를 필터링하거나 정렬하는 방법을 설명합니다.|  
  
  
