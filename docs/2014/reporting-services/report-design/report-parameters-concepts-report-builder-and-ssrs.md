---
title: 보고서 매개 변수 개념 (보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: b0aa2159-4e49-4713-8824-5ef9a9edbc62
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 70bb740b9f5948d077f0336e7e7bc14ed9902941
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105083"
---
# <a name="report-parameters-concept-report-builder-and-ssrs"></a>보고서 매개 변수 개념(보고서 작성기 및 SSRS)
  보고서에 매개 변수를 추가하여 관련 보고서를 연결하거나 보고서 모양을 제어하거나 보고서 데이터를 필터링하거나 보고서 범위를 특정 사용자나 위치로 좁힐 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 보고서 매개 변수는 다음과 같은 방법으로 생성됩니다.  
  
-   쿼리 변수가 포함된 데이터 세트 쿼리를 정의할 때 자동으로 생성됩니다. 각 쿼리 변수의 경우 해당 데이터 세트 쿼리 매개 변수 및 보고서 매개 변수가 같은 이름으로 생성됩니다. 쿼리 매개 변수는 저장 프로시저의 입력 매개 변수 또는 쿼리 변수에 대한 참조일 수 있습니다.  
  
-   쿼리 매개 변수가 포함된 공유 데이터 세트에 참조를 추가할 때 자동으로 생성됩니다.  
  
-   보고서 데이터 창에서 보고서 매개 변수를 만들 때 수동으로 생성됩니다. 매개 변수는 보고서의 식에 포함할 수 있는 기본 제공 컬렉션 중 하나입니다. 보고서 정의 전반에서 값을 정의하는 데 식이 사용되기 때문에 매개 변수를 사용하여 보고서 모양을 제어하거나 관련 하위 보고서나 매개 변수를 사용하는 다른 보고서에 값을 전달할 수 있습니다.  
  
 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](report-parameters-report-builder-and-report-designer.md)를 참조하세요.  
  
 데이터가 보고서에 반환되기 전과 후에 매개 변수가 보고서 데이터를 필터링하는 데 자주 사용됩니다. 자세한 내용은 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)을 참조하세요.  
  
 보고서를 디자인할 때는 보고서 매개 변수가 보고서 정의에 저장되고, 보고서를 게시할 때는 보고서 매개 변수가 보고서 정의와 별개로 저장되고 관리됩니다. 보고서를 보고서 서버에 저장한 후 다음을 수행할 수 있습니다.  
  
-   보고서 정의로부터 독립적으로 보고서 서버에서 보고서 매개 변수 값을 직접 변경합니다.  
  
-   각 링크된 보고서가 보고서 서버에서 독립적으로 관리될 수 있는 별도의 매개 변수 값 집합이 포함된 보고서 정의에 대한 링크인 여러 링크된 보고서를 만듭니다.  
  
 보고서 스냅숏, 기록 또는 게시된 보고서에 대한 구독을 만들려는 경우 보고서 매개 변수가 보고서의 디자인 요구 사항에 미치는 영향을 이해해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 제작 개념&#40;보고서 작성기 및 SSRS&#41;](report-authoring-concepts-report-builder-and-ssrs.md)   
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [자습서: 보고서에 매개 변수 추가&#40;보고서 작성기&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)  
  
  
