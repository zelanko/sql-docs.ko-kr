---
title: 데이터 집합 속성 대화 상자, 매개 변수 (보고서 작성기) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10023"
ms.assetid: 3a0672ad-c969-455b-b952-585164ce1dda
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3b4d473958e17fd67c1685e206fc02a5f5feca60
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56298011"
---
# <a name="dataset-properties-dialog-box-parameters-report-builder"></a>데이터 집합 속성 대화 상자, 매개 변수(보고서 작성기)
  선택 **매개 변수** 에 **데이터 집합 속성** 대화 상자를 추가, 변경 및 쿼리 매개 변수를 삭제 합니다.  
  
 포함된 데이터 집합의 경우 옵션은 보고서 정의의 데이터 집합에 적용됩니다.  
  
 공유 데이터 집합의 경우 옵션은 보고서 서버에 있는 공유 데이터 집합 정의에 적용됩니다.  
  
 자세한 내용은 [포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **추가**  
 목록에 새 매개 변수를 추가합니다.  
  
 **Delete**  
 선택한 매개 변수를 목록에서 제거합니다.  
  
 **위쪽 화살표**  
 선택한 매개 변수를 목록에서 위쪽으로 이동합니다.  
  
 **아래쪽 화살표**  
 선택한 매개 변수를 목록에서 아래쪽으로 이동합니다.  
  
 **매개 변수 이름**  
 **데이터 집합 속성** 대화 상자의 **쿼리** 탭에서 데이터 집합에 추가한 쿼리 매개 변수의 이름을 입력합니다.  
  
 **매개 변수 값**  
 포함된 데이터 집합에만 해당됩니다.  
  
 쿼리 매개 변수의 값을 입력합니다. 이 값은 정적 값 또는 보고서 내의 개체를 참조하는 식일 수 있지만 보고서 항목이나 필드는 참조할 수 없습니다. 기본적으로 **값** 에는 보고서 매개 변수를 가리키는 식이 포함됩니다.  
  
 **기본값**  
 공유 데이터 집합에만 해당됩니다.  
  
 기본값을 지정하려면 확인란을 선택합니다.  
  
 기본값을 입력합니다. 이 값은 정적 값이거나 보고서 내의 개체를 참조하는 식일 수 있습니다. 식은 보고서 항목, 보고서 매개 변수 또는 필드를 참조할 수 없습니다.  
  
 빈 기본값을 지정하려면 입력란을 비워 둡니다.  
  
 null을 지정하려면 Null 허용 옵션을 선택합니다.  
  
 **읽기 전용**  
 공유 데이터 집합에만 해당됩니다.  
  
 공유 데이터 집합 정의에서 이 매개 변수를 읽기 전용으로 표시하려면 이 옵션을 선택합니다. 그러면 공유 데이터 집합을 보고서에 추가할 때 매개 변수가 속성에 나타나지 않습니다. 공유 데이터 집합을 보고서 서버에서 캐시할 때 값을 변경할 수 없습니다.  
  
 **Null 허용**  
 공유 데이터 집합에만 해당됩니다.  
  
 null 값을 허용하려면 이 옵션을 선택합니다.  
  
 **쿼리에서 생략**  
 공유 데이터 집합에만 해당됩니다.  
  
 보고서 매개 변수에 대한 참조가 쿼리에 있지 않고 공유 데이터 집합 필터의 식에 있는 경우 이 옵션을 선택합니다. 이 옵션을 선택하는 경우 쿼리 실행 시 이 매개 변수에 대한 기본값을 지정할 필요가 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [대화 상자, 창 및 마법사에 대한 보고서 작성기 도움말](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [데이터 집합 속성 대화 상자, 쿼리 &#40;보고서 작성기&#41;](report-data/dataset-properties-dialog-box-query-report-builder.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [자습서: 보고서 매개 변수를 추가 &#40;보고서 작성기&#41;](tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](report-design/report-parameters-report-builder-and-report-designer.md)   
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [쿼리 디자이너&#40;보고서 작성기&#41;](../../2014/reporting-services/query-designers-report-builder.md)   
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [공유 데이터 집합 또는 포함된 데이터 집합 만들기&#40;보고서 작성기 및 SSRS&#41;](report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
  
