---
title: "테이블 또는 열 (SSAS 테이블 형식) 이름 바꾸기 | Microsoft Docs"
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.bidtoolset.renametableorcolumn.f1
ms.assetid: 88061a39-c5aa-403d-a52b-7fdb365fc235
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: edfd1fe4e353f74f9729325b40865905a1907dc2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="rename-a-table-or-column-ssas-tabular"></a>테이블 또는 열 이름 바꾸기(SSAS 테이블 형식)
  가져오기 프로세스 동안 **테이블 가져오기 마법사** 의 **테이블 및 뷰 선택** 페이지에서 **이름**을 입력하여 테이블 이름을 변경할 수 있습니다. **테이블 가져오기 마법사** 의 **SQL 쿼리 지정**페이지에서 쿼리를 지정하여 데이터를 가져오는 경우 테이블 및 열 이름을 변경할 수도 있습니다.  
  
 데이터를 모델에 추가하면 모델 디자이너 아래의 테이블 탭에 테이블의 이름 또는 제목이 나타납니다. 테이블의 이름을 보다 적절한 이름으로 변경할 수 있습니다. 모델에 데이터를 추가한 후 열의 이름을 바꿀 수도 있습니다. 이 옵션은 특히 여러 원본에서 데이터를 가져왔을 때 서로 다른 테이블의 열에 쉽게 구분할 수 있는 이름을 지정하려는 경우에 중요합니다.  
  
### <a name="to-rename-a-table"></a>테이블의 이름을 바꾸려면  
  
1.  모델 디자이너에서 이름을 바꾸려는 테이블이 포함된 탭을 마우스 오른쪽 단추로 클릭한 다음 **이름 바꾸기**를 클릭합니다.  
  
2.  새 이름을 입력합니다.  
  
    > [!NOTE]  
    >  **테이블 속성 편집** 대화 상자를 사용하여 연결 정보 및 열 매핑을 비롯한 테이블의 다른 속성을 편집할 수 있습니다. 그러나 이 대화 상자에서 이름을 변경할 수는 없습니다.  
  
### <a name="to-rename-a-column"></a>열 이름을 바꾸려면  
  
1.  모델 디자이너에서 이름을 바꾸려는 열의 머리글을 두 번 클릭하거나 머리글을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **열 이름 바꾸기** 를 선택합니다.  
  
2.  새 이름을 입력합니다.  
  
## <a name="naming-requirements-for-columns-and-tables"></a>열 및 테이블의 명명 요구 사항  
 다음 단어 및 문자는 테이블 또는 열 이름으로 사용할 수 없습니다.  
  
-   선행 또는 후행 공백  
  
-   제어 문자  
  
-   Analysis Services 개체 이름에 유효하지 않은 문자: .,;':/\\*|?&%$!+=()[]{}<>  
  
-   MDX(Multidimensional Expressions) 및 DMX(Data Mining Extensions) 함수 이름과 연산자를 비롯한 Analysis Services의 예약된 키워드  
  
## <a name="effect-of-renaming-on-existing-tables-columns-and-calculations"></a>기존 테이블, 열 및 계산 이름을 바꿀 경우의 영향  
 테이블의 이름을 변경할 때마다 여러 열이나 측정값이 포함될 수 있는 기본 테이블 개체의 이름을 변경하게 됩니다. 테이블에 있는 모든 열과 테이블을 사용 하는 모든 관계는 해당 정의의 새 이름을 사용 하도록 업데이트 되어야 합니다. 대부분의 경우에 이러한 업데이트가 자동으로 수행 합니다.
  
 이름이 바뀐된 테이블의 열을 사용 하는 하거나 이름이 바꾼된 테이블을 사용 하는 모든 계산도 업데이트 되어야 하 고 해당 계산에서 파생 된 데이터가 새로 고쳐지고 다시 계산 되어야 합니다. 영향을 받는 테이블과 계산의 수에 따라서는 이러한 작업을 완료하는 데 시간이 걸릴 수 있습니다. 따라서 가져오기 프로세스를 진행하는 동안 또는 복잡한 관계와 계산을 만들기 전에 테이블 이름을 바꾸는 것이 가장 좋습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 및 열](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [파워 피벗에서 가져오기](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)   
 [Analysis Services에서 가져오기](../../analysis-services/tabular-models/import-from-analysis-services-ssas-tabular.md)  
  
  
