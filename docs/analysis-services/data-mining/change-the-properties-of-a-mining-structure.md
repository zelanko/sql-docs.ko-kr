---
title: "마이닝 구조 속성 변경 | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], properties
ms.assetid: 03b16897-2e36-42b8-9f7d-db1b9b898401
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 908bf89105dbcfc4c61a4018c92a8cee71237fb9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="change-the-properties-of-a-mining-structure"></a>마이닝 구조 속성 변경
  마이닝 구조에 대한 속성은 두 가지 종류가 있으며 이 두 가지 속성 모두 수정할 수 있습니다.  
  
-   마이닝 구조의 속성 중 전체 구조에 영향을 주는 속성  
  
-   구조의 개별 열에 대한 속성  
  
 일부 속성은 다른 속성 설정에 종속됩니다. 예를 들어 열의 데이터 형식을 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 로 설정하기 전에는 범주화 동작을 제어하는 속성(예: <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A>또는 **DiscretizationBucketCount**)을 설정할 수 없습니다.  
  
 마이닝 구조 속성에 대한 자세한 내용은 [마이닝 구조 열](../../analysis-services/data-mining/mining-structure-columns.md)을 참조하세요.  
  
### <a name="to-change-the-properties-of-a-mining-structure"></a>마이닝 구조의 속성을 변경하려면  
  
1.  데이터 마이닝 디자이너의 **마이닝 구조** 탭에서 마이닝 구조의 한 열이나 마이닝 구조를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
     화면 오른쪽에 **속성** 창이 열립니다. 이 창이 이미 열려 있는 경우도 있습니다.  
  
2.  **속성** 창에서 변경할 속성에 해당하는 값을 선택하고 새 값을 입력합니다.  
  
     디자이너에서 다른 요소를 선택하면 새 값이 적용됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 구조 태스크 및 방법](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
