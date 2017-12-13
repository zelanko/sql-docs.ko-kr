---
title: "데이터 원본 뷰 (Analysis Services)에서 속성을 변경 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- friendly names [Analysis Services]
- names [Analysis Services], data source views
- viewing tables
- displaying tables
- data source views [Analysis Services], tables
- tables [Analysis Services], data source views
ms.assetid: 4ccdabea-9c4d-460d-ba78-d23068143696
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b8d8d731552fe099d161d6b87bca87ceecd709a9
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="change-properties-in-a-data-source-view-analysis-services"></a>데이터 원본 뷰에서 속성 변경(Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]명명 된 계산, 데이터 원본 뷰 마법사를 사용 하 고 테이블, 뷰, 추가 데이터 원본 뷰를 정의 및 데이터 원본에 명명 된 쿼리를 한 후 관련 된 속성을 변경 하는 것이 좋습니다.  
  
-   데이터 원본 뷰 일치 조건  
  
-   고급 데이터 원본 뷰 옵션  
  
-   개체 이름  
  
-   개체 메타데이터  
  
 수정할 수 없는 데이터 원본에서 검색된 개체 메타데이터를 볼 수도 있습니다.  
  
## <a name="viewing-or-changing-data-source-view-properties"></a>데이터 원본 뷰 속성 보기 또는 변경  
 데이터 원본 뷰에 대한 설명을 제외한 데이터 원본 뷰 속성은 처음에 데이터 원본 뷰를 정의할 때 데이터 원본 뷰 마법사에서 설정합니다. 다음 표에서는 데이터 원본 뷰의 속성을 보여 주고 설명합니다.  
  
> [!NOTE]  
>  속성 창에는 DSV 개체와 함께 .dsv 파일 속성이 표시됩니다. 개체의 속성을 보려면 솔루션 탐색기에서 개체를 두 번 클릭합니다. 속성은 다음 표에서 참조하는 속성을 반영하도록 업데이트됩니다.  
  
|속성|Description|  
|--------------|-----------------|  
|데이터 원본|속성을 보고 있는 데이터 원본 뷰 내의 데이터 원본을 지정합니다.|  
|Description|데이터 원본 뷰에 대한 설명을 지정합니다.|  
|이름|솔루션 탐색기나 Analysis Services 데이터베이스에 표시되는 데이터 원본 뷰의 이름을 지정합니다. 여기서 또는 솔루션 탐색기에서 데이터 원본 뷰 이름을 변경할 수 있습니다.|  
|NameMatchingCriteria|데이터 원본의 이름 일치 조건입니다. 데이터 원본 뷰 마법사에서 기본 키 - 외래 키 관계가 감지된 경우 기본값은 (없음)입니다. 데이터 원본 뷰 마법사에서 이 속성을 설정했는지에 관계없이 여기서 값을 지정할 수 있습니다. 데이터베이스 관계가 있으며 이름 일치 조건을 지정하면 기존 테이블과 새로 추가한 테이블 간의 관계를 유추하기 위해 둘 다 사용됩니다.|  
|RetrieveRelationships|데이터베이스에서 관계가 검색되는지 여부를 지정합니다. 기본값은 True입니다.|  
|SchemaRestriction|데이터 원본에서 검색된 스키마에 대한 제한(있는 경우)을 지정합니다. 기본적으로 스키마 제한은 없습니다.|  
  
## <a name="viewing-or-changing-datatable-properties"></a>DataTable 속성 보기 또는 변경  
 **DataTable** 속성은 데이터 원본 뷰의 테이블, 뷰 및 명명된 쿼리의 속성입니다. 이러한 속성은 데이터 원본 뷰에 이러한 개체를 추가할 때 설정됩니다. 다음 표에서는 데이터 원본 뷰의 **DataTable** 개체 속성을 보여 주고 설명합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|AllowChangesDuringGeneration|스키마 생성 마법사에 다시 생성 중 데이터 원본 뷰를 덮어쓸 권한이 있는지 여부를 지정합니다. 이 속성은 스키마 생성 마법사에서 처음 생성한 테이블에만 있습니다. 자세한 내용은 [증분 생성 이해](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)를 참조하세요.|  
|DataSource|개체의 데이터 원본을 지정합니다. 이 속성은 편집할 수 없습니다.|  
|Description|테이블, 뷰 또는 명명된 쿼리에 대한 설명을 지정합니다. 기본 데이터베이스 테이블이나 뷰에 확장 속성으로 저장된 설명이 있으면 이 값도 표시됩니다. 이 속성은 편집할 수 있습니다.|  
|FriendlyName|사용자가 보다 쉽게 이해할 수 있거나 주제 영역에 더 적합한 테이블 또는 뷰 이름을 지정합니다. 기본적으로 테이블이나 뷰의 **FriendlyName** 속성은 해당 테이블이나 뷰의 **Name** 속성과 동일합니다. **FriendlyName** 속성은 테이블이나 뷰를 기반으로 개체를 정의할 때 OLAP 및 데이터 마이닝 개체에 사용됩니다. 이 속성은 편집할 수 있습니다.|  
|이름|기본 테이블이나 뷰의 이름 또는 명명된 쿼리의 이름을 지정합니다. **Name** 속성은 명명된 쿼리를 기반으로 개체를 정의할 때 OLAP 및 데이터 마이닝 개체에 사용됩니다. 이 속성은 명명된 쿼리에 대해서만 편집할 수 있습니다.|  
|QueryDefinition|명명된 쿼리 정의를 지정합니다. 이 속성은 명명된 쿼리에만 해당되며 직접 편집할 수 없습니다. 이 속성을 편집하려면 명명된 쿼리 자체를 편집합니다.|  
|스키마|테이블, 뷰 또는 명명된 쿼리에 해당하는 데이터베이스 스키마를 지정합니다. 이 속성은 편집할 수 없습니다.|  
|TableType|테이블, 뷰 또는 명명된 쿼리에 대한 테이블 유형을 지정합니다. 이 속성은 편집할 수 없습니다.|  
  
## <a name="viewing-or-changing-datacolumn-properties"></a>DataColumn 속성 보기 또는 변경  
 **DataColumn** 속성은 데이터 원본 뷰의 테이블, 뷰 및 명명된 쿼리의 열 속성입니다. 이러한 속성은 명명된 계산에서 정의하는 대로 또는 기본 테이블이나 뷰, 명명된 쿼리에서 이러한 개체를 데이터 원본 뷰에 추가할 때 설정됩니다. 다음 표에서는 데이터 원본 뷰의 **DataColumn** 개체 속성을 보여 주고 설명합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|AllowNull|기본 테이블의 열, 값 또는 명명된 쿼리를 기반으로 열의 Null 허용 여부 속성을 지정합니다. 이 속성은 편집할 수 없습니다.|  
|DataType|기본 테이블의 열, 값 또는 명명된 쿼리를 기반으로 열의 데이터 형식 속성을 지정합니다. 이 속성은 직접 편집할 수 없습니다. 그러나 테이블이나 뷰에서 열의 데이터 형식을 변경해야 하는 경우 원하는 데이터 형식으로 열을 변환하는 명명된 쿼리로 테이블을 바꿉니다.|  
|DateTimeMode|**DateTime** 열의 날짜 직렬화 형식을 지정합니다. 기본값은 **UnspecifiedLocal**입니다. 이 속성은 편집할 수 있습니다.|  
|Description|열에 대한 설명을 지정합니다. 기본 데이터베이스 열에 확장 속성으로 저장된 설명이 있으면 이 값도 표시됩니다. 이 속성은 편집할 수 있습니다.|  
|FriendlyName|사용자가 보다 쉽게 이해할 수 있거나 주제 영역에 더 적합한 테이블 또는 뷰의 열 이름을 지정합니다. 기본적으로 테이블이나 뷰의 열에 대한 **FriendlyName** 속성은 해당 열의 **Name** 속성과 동일합니다. **FriendlyName** 속성은 테이블이나 뷰의 열을 기반으로 특성을 정의할 때 OLAP 및 데이터 마이닝 개체에 사용됩니다. 이 속성은 편집할 수 있습니다.|  
|길이|기본 테이블이나 뷰의 열 데이터를 기반으로 열의 최대 길이를 지정합니다.|  
|이름|기본 열의 이름 또는 명명된 계산의 이름을 지정합니다. **Name** 속성은 명명된 계산을 기반으로 특성을 정의할 때 OLAP 및 데이터 마이닝 개체에 사용됩니다. 이 속성은 명명된 계산에 대해서만 편집할 수 있습니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델의 데이터 원본 뷰](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [데이터 원본 뷰 디자이너에서의 다이어그램 작업&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  
