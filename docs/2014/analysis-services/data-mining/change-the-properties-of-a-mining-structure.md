---
title: 마이닝 구조의 속성 변경 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], properties
ms.assetid: 03b16897-2e36-42b8-9f7d-db1b9b898401
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 083133e43355f6f394c18654a23aa5366e3d5731
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187690"
---
# <a name="change-the-properties-of-a-mining-structure"></a>마이닝 구조 속성 변경
  마이닝 구조에 대한 속성은 두 가지 종류가 있으며 이 두 가지 속성 모두 수정할 수 있습니다.  
  
-   마이닝 구조의 속성 중 전체 구조에 영향을 주는 속성  
  
-   구조의 개별 열에 대한 속성  
  
 일부 속성은 다른 속성 설정에 종속됩니다. 예를 들어 열의 데이터 형식을 `Discretized`로 설정하기 전에는 범주화 동작을 제어하는 속성(예: <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 또는 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A>)을 설정할 수 없습니다.  
  
 마이닝 구조 속성에 대한 자세한 내용은 [마이닝 구조 열](mining-structure-columns.md)을 참조하세요.  
  
### <a name="to-change-the-properties-of-a-mining-structure"></a>마이닝 구조의 속성을 변경하려면  
  
1.  데이터 마이닝 디자이너의 **마이닝 구조** 탭에서 마이닝 구조의 한 열이나 마이닝 구조를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
     화면 오른쪽에 **속성** 창이 열립니다. 이 창이 이미 열려 있는 경우도 있습니다.  
  
2.  **속성** 창에서 변경할 속성에 해당하는 값을 선택하고 새 값을 입력합니다.  
  
     디자이너에서 다른 요소를 선택하면 새 값이 적용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 구조 태스크 및 방법](mining-structure-tasks-and-how-tos.md)  
  
  
