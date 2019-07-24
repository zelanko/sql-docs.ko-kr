---
title: 보고서 데이터 창
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 89cbdf8b0ae431a03a14c2a39d46edffa8920689
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267810"
---
# <a name="report-data-pane-in-sql-server-reporting-services-ssrs"></a>SSRS(SQL Server Reporting Services)의 보고서 데이터 창

  **보고서 데이터** 창을 사용하여 보고서의 현재 정의된 매개 변수, 데이터 원본, 데이터 세트, 필드 컬렉션 및 이미지를 볼 수 있습니다. 보고서 데이터 창은 보고서의 데이터를 나타내는 항목의 계층 뷰를 표시합니다. 최상위 노드는 기본 제공 필드, 매개 변수, 이미지 및 데이터 원본 참조를 나타냅니다. 각 노드를 확장하여 데이터 항목을 볼 수 있습니다. 예를 들어 데이터 원본 노드를 확장하면 해당 데이터 원본에 대해 정의된 데이터 세트가 표시됩니다. 데이터 세트를 확장하면 필드 컬렉션이 표시됩니다. 데이터를 보고서 페이지의 보고서 항목에 연결하려면 항목을 끌어서 보고서 디자인 화면에 놓습니다.  
  
## <a name="options"></a>옵션

 **기본 제공 필드**  
 보고서 이름이나 페이지 번호와 같이 보고서에서 일반적으로 사용되는 Reporting Services에서 제공하는 필드를 나타냅니다. 자세한 내용은 [식의 기본 제공 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)을 참조하세요.  
  
 **매개 변수**  
 각각 단일값 또는 다중값일 수 있는 보고서 매개 변수 컬렉션을 나타냅니다. 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)에 대해 자세히 알아봅니다.  
  
 **이미지**  
 보고서에 사용되는 이미지 집합을 나타냅니다. 자세한 내용은 [이미지&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)를 참조하세요.  
  
 **데이터 원본**  
 포함된 데이터 원본이나 공유 데이터 원본에 대한 단일 데이터 원본 참조를 나타냅니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 공유 데이터 원본은 솔루션 탐색기의 공유 데이터 원본 폴더에 표시됩니다. 데이터 원본은 Reporting Services에서 지원하는 데이터 원본 유형 중 하나를 지정합니다. 데이터 원본은 데이터 세트 컬렉션이 기반을 두는 부모 노드입니다. 자세한 내용은 [데이터 연결, 데이터 원본 및 연결 문자열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)을 참조하세요.  
  
 **데이터 세트**  
 단일 데이터 세트를 나타냅니다. 데이터 세트는 쿼리에 의해 지정된 필드 컬렉션의 부모 노드이며 계산 필드를 포함합니다. Reporting Services는 쿼리를 지정할 수 있도록 쿼리 디자이너를 지원합니다. 자세한 내용은 [보고서 데이터 세트&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md) 및 [쿼리 디자인 도구&#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md)을 참조하세요.  
  
## <a name="next-steps"></a>다음 단계

 - [데이터 세트 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)
 - [그룹화 창](../../reporting-services/tools/grouping-pane.md)