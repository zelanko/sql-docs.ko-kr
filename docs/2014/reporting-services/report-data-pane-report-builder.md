---
title: 보고서 데이터 창 (보고서 작성기) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10435"
helpviewer_keywords:
- Report Data pane
ms.assetid: 1492aa39-aeb1-4509-ab97-b9edd0901b7e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b5ba45fa4070a025101d9bf2c06bc69f8aa5d8b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62697801"
---
# <a name="report-data-pane-report-builder"></a>보고서 데이터 창(보고서 작성기)
  **보고서 데이터** 창을 사용하여 보고서의 현재 정의된 매개 변수, 데이터 원본, 데이터 집합, 필드 컬렉션 및 이미지를 볼 수 있습니다. 보고서 데이터는 보고서의 데이터를 나타내는 항목의 계층 뷰를 표시합니다. 최상위 노드는 기본 제공 필드, 매개 변수, 이미지 및 데이터 원본 참조를 나타냅니다. 각 노드를 확장하여 데이터 항목을 볼 수 있습니다. 예를 들어 데이터 원본 노드를 확장하면 해당 데이터 원본에 대해 정의된 데이터 세트가 표시됩니다. 데이터 세트를 확장하면 필드 컬렉션이 표시됩니다. 항목을 보고서 디자인 화면이나 그룹화 창으로 끌어 데이터를 보고서 페이지의 선택된 보고서 항목에 연결합니다. 자세한 내용은 [보고서 디자인 뷰&#40;보고서 작성기&#41;](report-builder/report-design-view-report-builder.md)를 참조하세요.  
  
## <a name="options"></a>변수  
 **기본 제공 필드**  
 보고서 이름이나 페이지 번호를 비롯하여 보고서에서 일반적으로 사용되는 필드를 나타냅니다. 자세한 내용은 [식의 기본 제공 컬렉션&#40;보고서 작성기 및 SSRS&#41;](report-design/built-in-collections-in-expressions-report-builder.md)을 참조하세요.  
  
 **매개 변수**  
 각각 단일값 또는 다중값일 수 있는 보고서 매개 변수 컬렉션을 나타냅니다. 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](report-design/report-parameters-report-builder-and-report-designer.md)를 참조하세요.  
  
 **이미지**  
 보고서에 사용되는 이미지 집합을 나타냅니다. 자세한 내용은 [이미지&#40;보고서 작성기 및 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)를 참조하세요.  
  
 **데이터 원본**  
 포함된 데이터 원본 또는 공유 데이터 원본에 대한 참조를 나타냅니다. 데이터 원본은 보고서의 데이터 원본을 나타냅니다. 데이터 원본은 이를 사용하는 데이터 집합 컬렉션의 부모 노드입니다. 자세한 내용은 [보고서에 데이터 추가 &#40;보고서 작성기 및 SSRS&#41; ](report-data/report-datasets-ssrs.md) 하 고 [데이터 연결, 데이터 원본 및 보고서 작성기에서 연결 문자열](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
 **데이터 집합**  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 데이터베이스에서 데이터를 검색하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리처럼 하나의 명령을 실행하여 데이터 원본에서 검색되는 데이터를 나타냅니다. 데이터 집합은 쿼리로 지정되는 필드 컬렉션의 부모 노드이며 계산된 필드를 포함합니다. 보고서 작성기에서는 쿼리를 지정하는 데 유용한 쿼리 디자이너를 지원합니다. 자세한 내용은 [보고서에 데이터 추가 &#40;보고서 작성기 및 SSRS&#41;](report-data/report-datasets-ssrs.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [대화 상자, 창 및 마법사에 대한 보고서 작성기 도움말](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [그룹화 창&#40;보고서 작성기&#41;](report-design/grouping-pane-report-builder.md)   
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
