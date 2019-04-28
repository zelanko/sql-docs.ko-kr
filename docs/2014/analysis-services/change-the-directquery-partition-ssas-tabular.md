---
title: DirectQuery 파티션 (SSAS 테이블 형식) 변경 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: f9df1e66-dd23-41b4-95eb-af110d10eda4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b247bd63087003b1c9205719a6d1cb0563390cc3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62681130"
---
# <a name="change-the-directquery-partition-ssas-tabular"></a>DirectQuery 파티션 변경(SSAS 테이블 형식)
  테이블의 한 파티션만 DirectQuery 파티션으로 지정할 수 있으므로 기본적으로 Analysis Services에서는 테이블에 첫 번째로 만들어진 파티션을 사용합니다. 모델 프로젝트 제작 중에 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 파티션 관리자 대화 상자를 사용하여 DirectQuery 파티션을 변경할 수 있습니다. 배포된 모델의 경우 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 사용하여 DirectQuery 파티션을 변경할 수 있습니다.  
  
### <a name="change-the-directquery-partition-for-a-tabular-model-project"></a>테이블 형식 모델 프로젝트에 대한 DirectQuery 파티션 변경  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]의 모델 디자이너에서 분할된 테이블이 포함된 테이블(탭)을 클릭합니다.  
  
2.  **테이블** 메뉴를 클릭한 다음 **파티션**을 클릭합니다.  
  
3.  **파티션 관리자**에서 현재 직접 쿼리 파티션인 파티션의 파티션 이름에는 **(DirectQuery)** 라는 접두사가 표시됩니다.  
  
     **파티션** 목록에서 다른 파티션을 선택하고 **DirectQuery로 설정**을 클릭합니다. **DirectQuery로 설정** 단추는 현재 DirectQuery 파티션이 선택된 경우에는 사용할 수 없으며 모델이 직접 쿼리 모드용으로 설정되지 않은 경우에는 표시되지 않습니다.  
  
4.  필요한 경우 처리 옵션을 변경하고 **확인**을 클릭합니다.  
  
### <a name="change-the-directquery-partition-for-a-deployed-tabular-model"></a>배포된 테이블 형식 모델에 대한 DirectQuery 파티션 변경  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 model 데이터베이스를 엽니다.  
  
2.  **테이블** 노드를 확장하고 분할된 테이블을 마우스 오른쪽 단추로 클릭한 다음 **파티션**을 선택합니다.  
  
     DirectQuery 모드에서 사용하도록 지정된 파티션은 파티션 이름에 (DirectQuery)라는 접두사가 포함되어 있습니다.  
  
3.  다른 파티션으로 변경하려면 **직접 쿼리** 도구 모음 아이콘을 클릭하여 **DirectQuery 파티션 설정** 대화 상자를 엽니다. 직접 쿼리용으로 설정되지 않은 모델에서는 DirectQuery 도구 모음 아이콘을 사용할 수 없습니다.  
  
4.  **파티션 이름** 드롭다운 목록에서 다른 파티션을 선택한 다음 필요한 경우 파티션에 대한 처리 옵션을 변경합니다.  
  
## <a name="see-also"></a>관련 항목  
 [파티션&#40;SSAS 테이블 형식&#41;](tabular-models/partitions-ssas-tabular.md)  
  
  
