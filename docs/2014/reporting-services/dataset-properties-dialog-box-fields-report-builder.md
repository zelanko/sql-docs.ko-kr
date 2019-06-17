---
title: 데이터 집합 속성 대화 상자, 필드 (보고서 작성기) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10021"
ms.assetid: 75c7e54a-3d20-4c9a-88da-ab36dce2ce42
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 375d8eda6f0863dbe3852f1a88ea2e58ecc85b80
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109428"
---
# <a name="dataset-properties-dialog-box-fields-report-builder"></a>데이터 세트 속성 대화 상자, 필드(보고서 작성기)
  **데이터 집합 속성** 대화 상자에서 **필드** 를 선택하여 보고서 데이터 집합의 필드 컬렉션을 변경할 수 있습니다. 필드 목록은 자동으로 채워지지만 **필드** 를 사용하여 쿼리와 계산 필드를 추가, 편집 및 삭제할 수도 있습니다.  
  
 계산 필드는 포함된 데이터 세트에서만 지원됩니다. 자세한 내용은 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)이라는 데이터 집합이 들어 있습니다.  
  
## <a name="options"></a>변수  
 **추가**  
 데이터 세트에 새 쿼리나 계산 필드를 추가합니다.  
  
 **Delete**  
 선택한 필드를 데이터 세트에서 삭제합니다.  
  
 **필드 이름**  
 필드의 이름을 입력합니다. 필드는 데이터 세트 내에서 고유해야 합니다. 데이터 세트의 기존 필드 각각에 대해서는 이름이 미리 지정됩니다.  
  
 **필드 원본**  
 필드의 값을 입력합니다.  
  
 계산 필드의 경우 필드 원본은 데이터 세트 쿼리 또는 사용자가 만든 식으로 검색된 기존 필드의 이름이어야 합니다. 예를 들어 Sales라는 쿼리 필드의 값에 10을 곱한 값을 표시하는 필드를 만들려면 `=10 * Fields!Sales.Value`식을 사용합니다.  
  
 쿼리 필드의 경우 필드 원본은 데이터 세트 쿼리로 검색된 기존 필드의 이름이어야 합니다.  
  
 **식 (fx)**  
 새 계산 필드의 식을 추가하거나 변경합니다. 이 단추는 **추가** 를 클릭하고 **계산 필드**를 선택했을 때만 나타납니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [공유 데이터 집합 또는 포함된 데이터 집합 만들기&#40;보고서 작성기 및 SSRS&#41;](report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [대화 상자, 창 및 마법사에 대한 보고서 작성기 도움말](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [데이터 집합 속성 대화 상자, 옵션 &#40;보고서 작성기&#41;](report-data/dataset-properties-dialog-box-options-report-builder.md)   
 [데이터 집합 속성 대화 상자, 필터 &#40;보고서 작성기&#41;](../../2014/reporting-services/dataset-properties-dialog-box-filters-report-builder.md)   
 [데이터 집합 속성 대화 상자, 매개 변수 &#40;보고서 작성기&#41;](../../2014/reporting-services/dataset-properties-dialog-box-parameters-report-builder.md)   
 [데이터 집합 속성 대화 상자, 쿼리 &#40;보고서 작성기&#41;](report-data/dataset-properties-dialog-box-query-report-builder.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
  
