---
title: 예측 구조 및 모델 만들기 (중급 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5f55cbf6-0db4-4cb4-a0f5-e27441873d4f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6e631a8983705d4f58e4b193823c9a255284f346
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63204815"
---
# <a name="creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial"></a>예측 구조 및 모델 만들기(중급 데이터 마이닝 자습서)
  다음으로 데이터 마이닝 마법사를 사용하여 방금 만든 데이터 원본 뷰를 기반으로 하는 새 마이닝 구조와 마이닝 모델을 만듭니다. 이 태스크에서는 마이닝 모델에 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시계열 알고리즘을 사용하도록 지정합니다.  
  
### <a name="to-create-a-forecasting-mining-structure"></a>예측 마이닝 구조를 만들려면  
  
1.  의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]솔루션 탐색기에서 **마이닝 구조** 를 마우스 오른쪽 단추로 클릭 하 고 **새 마이닝 구조**를 선택 합니다.  
  
2.  
  **데이터 마이닝 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  **정의 방법 선택** 페이지에서 **기존 관계형 데이터베이스 또는 데이터 웨어하우스** 를 선택 했는지 확인 하 고 **다음**을 클릭 합니다.  
  
4.  **데이터 마이닝 구조 만들기** 페이지에서 **사용 하려는 데이터 마이닝 기술**에 대해 **Microsoft 시계열**을 선택 하 고 **다음**을 클릭 합니다.  
  
5.  **데이터 원본 뷰 선택** 페이지의 **사용 가능한 데이터 원본 뷰**에서 **salesbyregion**을 선택 합니다.  
  
6.  **다음**을 클릭합니다.  
  
7.  **테이블 유형 지정** 페이지에서 vTimeSeries 테이블의 **사례** 열에 있는 확인란이 선택 되어 있는지 확인 한 후 **다음**을 클릭 합니다.  
  
8.  **학습 데이터 지정** 페이지에서 modelregion 및 ReportingDate 열에 대 한 **키** 열의 확인란을 선택 합니다.  
  
     데이터 원본 뷰를 만들 때 이 열을 논리적 기본 키로 지정했으므로 ReportingDate를 기본적으로 선택해야 합니다. ModelRegion을 두 번째 키로 추가하면 알고리즘에 이 필드에 나열된 모델 및 지역의 각 조합에 대해 별도의 시계열을 만들도록 지시하는 것과 같습니다.  
  
9. 수량, 열에 대 한 **입력** 및 **예측 가능한** 열의 확인란을 선택 하 고 **다음**을 클릭 합니다.  
  
     **예측**가능을 선택 하 여이 열의 데이터에 대 한 예측을 만들려고 함을 알 수 있습니다. 그러나 이전 데이터에 대한 예측을 기반으로 하므로 열을 입력으로 추가해야 합니다.  
  
10. **열 내용 및 데이터 형식 지정**페이지에서 선택 사항을 검토 합니다.  
  
     ModelRegion 열은 **키** 열로 지정 되 고 ReportingDate 열은 **key Time** 열로 자동으로 지정 됩니다. 각 키 유형 중 하나만 지정할 수 있습니다.  
  
11. **다음**을 클릭합니다.  
  
12. **마법사 완료** 페이지에서 **마이닝 구조 이름**에을 입력 `Forecasting`합니다.  
  
    > [!NOTE]  
    >  드릴스루를 사용하는 옵션은 시계열 모델에 사용할 수 없습니다.  
  
13. **마이닝 모델 이름**에를 입력 `Forecasting`한 다음 **마침**을 클릭 합니다.  
  
     데이터 마이닝 디자이너가 열리고 방금 만든 `Forecasting` 마이닝 구조가 표시 됩니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [&#40;중급 데이터 마이닝 자습서&#41;예측 구조 수정](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 디자이너](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft Time Series 알고리즘](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
