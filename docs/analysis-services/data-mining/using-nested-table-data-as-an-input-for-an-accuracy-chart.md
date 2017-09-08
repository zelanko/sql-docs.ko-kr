---
title: "정확도 차트에 대 한 입력으로 중첩된 테이블 데이터를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Mining Accuracy Chart [Analysis Services], nested tables
- Mining Accuracy Chart [Analysis Services], input tables
- nested tables
- adding nested tables
ms.assetid: 162e0686-ada3-4dd3-9151-9589926e6613
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6ebe50e260a7de9520c75e534548d342fa3b2b68
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="using-nested-table-data-as-an-input-for-an-accuracy-chart"></a>정확도 차트에 대한 입력으로 중첩 테이블 데이터 사용
  외부 데이터를 사용하여 마이닝 모델의 정확도를 테스트할 때 마이닝 모델에 중첩 테이블이 포함되어 있으면 외부 데이터에도 사례 테이블 및 연결된 중첩 테이블이 포함되어 있어야 합니다.  
  
 이 항목에서는 모델 테스트에 사용되는 중첩 테이블에 대한 작업을 수행하는 방법과 모델 및 외부 데이터의 중첩 테이블 및 사례 테이블을 매핑하는 방법과 중첩 테이블에 필터를 적용하는 방법에 대해 설명합니다.  
  
 중첩 테이블에 대한 작업을 수행할 때 다음 팁에 유의해야 합니다.  
  
-   **마이닝 모델 테스트 사례 사용** 또는 **마이닝 구조 테스트 사례 사용**옵션을 선택한 경우에는 사례 테이블이나 중첩 테이블을 지정할 필요가 없습니다. 이 옵션을 사용하면 테스트 데이터의 정의가 마이닝 구조에 저장되므로 정확도 차트를 만들 때 테스트 데이터가 자동으로 선택됩니다.  
  
-   데이터 원본의 사례 테이블과 중첩 테이블 간에 관계가 이미 설정되어 있는 경우 마이닝 구조의 열이 입력 테이블에 있는 동일한 이름의 열에 자동으로 매핑됩니다.  
  
-   사례 테이블을 지정하기 전에는 중첩 테이블을 선택할 수 없습니다. 또한 마이닝 모델에서 사례 테이블 및 중첩 테이블 구조를 사용하기 전에는 중첩 테이블을 입력으로 지정할 수 없습니다.  
  
### <a name="use-a-nested-table-as-input-to-an-accuracy-chart"></a>정확도 차트에 대한 입력으로 중첩 테이블 사용  
  
1.  마이닝 구조를 두 번 클릭하여 데이터 마이닝 디자이너에서 엽니다.  
  
2.  **마이닝 정확도 차트** 탭을 선택한 다음 **입력 선택** 탭을 선택합니다.  
  
3.  **정확도 차트에 사용할 데이터 집합을 선택하십시오**에서 **다른 데이터 집합 지정**옵션을 선택합니다.  
  
4.  찾아보기 단추 **(…)** 를 클릭하여 현재 서버의 데이터 원본 뷰 목록에서 외부 데이터 집합을 선택합니다.  
  
5.  **사례 테이블 선택**을 클릭합니다. **테이블 선택** 대화 상자에서 사례 데이터가 포함된 데이터 원본 뷰의 테이블을 선택한 다음 **확인**을 클릭합니다.  
  
6.  **중첩 테이블 선택**을 클릭합니다. **테이블 선택** 대화 상자에서 중첩 데이터가 포함된 테이블을 선택한 다음 **확인**을 클릭합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     중첩 테이블과 사례 테이블 간의 관계를 수정해야 하는 경우 **조인 수정** 을 클릭하여 **관계 만들기** 대화 상자를 엽니다.  
  
## <a name="see-also"></a>관련 항목:  
 [모델 테스트 데이터 선택 및 매핑](../../analysis-services/data-mining/choose-and-map-model-testing-data.md)   
 [모델 테스트 데이터에 필터 적용](../../analysis-services/data-mining/apply-filters-to-model-testing-data.md)  
  
  
