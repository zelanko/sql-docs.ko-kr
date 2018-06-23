---
title: 예측 구조 및 모델 (중급 데이터 마이닝 자습서) 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5f55cbf6-0db4-4cb4-a0f5-e27441873d4f
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 47d6e75a691c53fe1658fb5f79ee2bde8e9c2d01
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312271"
---
# <a name="creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial"></a>예측 구조 및 모델 만들기(중급 데이터 마이닝 자습서)
  다음으로 데이터 마이닝 마법사를 사용하여 방금 만든 데이터 원본 뷰를 기반으로 하는 새 마이닝 구조와 마이닝 모델을 만듭니다. 이 태스크에서는 마이닝 모델에 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시계열 알고리즘을 사용하도록 지정합니다.  
  
### <a name="to-create-a-forecasting-mining-structure"></a>예측 마이닝 구조를 만들려면  
  
1.  솔루션 탐색기에서 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 마우스 오른쪽 단추로 클릭 **Mining Structures** 선택 **새 마이닝 구조**합니다.  
  
2.  **데이터 마이닝 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  에 **정의 방법 선택** 페이지에서 **기존 관계형 데이터베이스 또는 데이터 웨어하우스에서** 을 선택한 다음 클릭 **다음**합니다.  
  
4.  에 **데이터 마이닝 구조 만들기** 페이지의 **사용할 데이터 마이닝 기술을 사용 하 시겠습니까?** 선택, **Microsoft 시계열**, 클릭 하 고  **다음**합니다.  
  
5.  에 **데이터 원본 뷰 선택** 페이지의 **사용 가능한 데이터 원본 뷰**선택, **SalesByRegion**합니다.  
  
6.  **다음**을 클릭합니다.  
  
7.  에 **테이블 유형 지정** 페이지에서 확인란은 **대/소문자** vTimeSeries 테이블에 대 한 열을 선택한 다음 클릭 **다음**합니다.  
  
8.  에 **학습 데이터 지정** 페이지에 있는 확인란을 선택 합니다는 **키** ModelRegion 및 ReportingDate 열에 대 한 열입니다.  
  
     데이터 원본 뷰를 만들 때 이 열을 논리적 기본 키로 지정했으므로 ReportingDate를 기본적으로 선택해야 합니다. ModelRegion을 두 번째 키로 추가하면 알고리즘에 이 필드에 나열된 모델 및 지역의 각 조합에 대해 별도의 시계열을 만들도록 지시하는 것과 같습니다.  
  
9. 에 있는 확인란을 선택는 **입력** 및 **예측 가능** 수량, 열 및 클릭 한 다음에 대 한 열 **다음**합니다.  
  
     선택 하 여 **예측 가능**,이 열에 있는 데이터에 예측을 만들 것인지를 나타냅니다. 그러나 이전 데이터에 대한 예측을 기반으로 하므로 열을 입력으로 추가해야 합니다.  
  
10. 페이지에서 **지정 열 내용 및 데이터 형식**, 선택 내용을 검토 합니다.  
  
     ModelRegion 열으로 지정 되는 **키** ReportingDate 열 및 열으로 자동으로 지정는 **Key Time** 열입니다. 각 키 유형 중 하나만 지정할 수 있습니다.  
  
11. **다음**을 클릭합니다.  
  
12. 에 **마법사 완료** 페이지에 대 한 **마이닝 구조 이름**, 형식 `Forecasting`합니다.  
  
    > [!NOTE]  
    >  드릴스루를 사용하는 옵션은 시계열 모델에 사용할 수 없습니다.  
  
13. **마이닝 모델 이름**, 형식 `Forecasting`, 클릭 하 고 **마침**합니다.  
  
     데이터 마이닝 디자이너가 열리고 표시 하는 `Forecasting` 방금 만든 마이닝 구조입니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [예측 구조 수정 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 디자이너](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft 시계열 알고리즘](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  