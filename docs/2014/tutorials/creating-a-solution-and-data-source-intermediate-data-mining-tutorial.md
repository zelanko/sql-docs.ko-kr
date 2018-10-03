---
title: 솔루션 및 데이터 원본 (중급 데이터 마이닝 자습서) 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0488b231-1045-4169-aabb-c1005d86ca30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1ad99c202d858bbdf5de47a21fe26070328e2de2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119633"
---
# <a name="creating-a-solution-and-data-source-intermediate-data-mining-tutorial"></a>솔루션 및 데이터 원본 만들기(중급 데이터 마이닝 자습서)
  데이터 마이닝을 사용 하려면 먼저 만들어야에서 프로젝트 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 템플릿을 사용 하 여 **Analysis Services 다차원 및 데이터 마이닝 프로젝트**합니다. 템플릿을 열면 데이터 원본, 마이닝 구조 및 마이닝 모델뿐 아니라 마이닝 구조에서 다차원 데이터를 사용하는 경우 큐브도 포함하여 데이터 마이닝에 필요할 수 있는 모든 스키마가 디자이너로 로드됩니다.  
  
 프로젝트를 만들면 솔루션이 배포될 때까지 솔루션이 로컬 파일로 저장됩니다. 솔루션을 배포할 때 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 찾습니다 합니다 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버 프로젝트 속성에 지정 된 만들고 새 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트와 동일한 이름 가진 데이터베이스입니다. 기본적으로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 사용 하는 **localhost** 새 프로젝트에 대 한 인스턴스. 명명된 인스턴스를 사용하거나 기본 인스턴스에 대해 다른 이름을 지정한 경우에는 프로젝트의 배포 데이터베이스 속성을 데이터 마이닝 개체를 만들려는 위치로 변경해야 합니다.  
  
 에 대 한 자세한 내용은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트를 참조 하세요 [Analysis Services 프로젝트 만들기 &#40;SSDT&#41;](../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)합니다.  
  
### <a name="to-create-a-new-analysis-services-project-for-this-tutorial"></a>이 자습서에 사용할 새 Analysis Services 프로젝트를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 엽니다.  
  
2.  **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다.  
  
3.  **설치된 템플릿** 창에서 **Analysis Services 다차원 및 데이터 마이닝 프로젝트** 를 선택합니다.  
  
4.  **이름** 상자에서 새 프로젝트의 이름을 **DM Intermediate**로 지정합니다.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-instance-where-data-mining-objects-are-stored-optional"></a>데이터 마이닝 개체가 저장되는 인스턴스를 변경하려면(선택 사항)  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에 **프로젝트** 메뉴에서 클릭 **속성**합니다.  
  
2.  **속성 페이지** 창의 왼쪽에서 **배포**를 클릭합니다.  
  
3.  **서버** 이름이 **localhost**인지 확인합니다. 다른 인스턴스를 사용할 경우에는 해당 인스턴스의 이름을 입력합니다. 명명된 된 인스턴스를 사용 하는 경우 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 컴퓨터 이름 및 인스턴스 이름을 입력 합니다. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-deployment-properties-for-a-project-optional"></a>프로젝트의 배포 속성을 변경하려면(선택 사항)  
  
1.  솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
     -- 또는 --  
  
     [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에 **프로젝트** 메뉴에서 **속성**합니다.  
  
2.  **속성 페이지** 창의 왼쪽에서 **배포**를 클릭합니다.  
  
     **옵션** 창에서 **배포 모드**를 선택하고 옵션을 **모두 배포** 로 설정하여 덮어쓰거나 **변경 내용만 배포** 로 설정하여 개체를 업데이트하거나 개체를 추가합니다.  
  
## <a name="creating-a-data-source"></a>데이터 원본 만들기  
 기본 데이터 마이닝 자습서에서 만든를 *데이터 원본* 에 대 한 연결 정보를 저장 하는 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 데이터베이스. 동일한 단계를 수행하여 이 솔루션에 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 데이터 원본을 만듭니다.  
  
#### <a name="to-create-a-data-source"></a>데이터 원본을 만들려면  
  
-   [데이터 원본 만들기 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
 단일 데이터 원본으로 여러 데이터 원본 뷰를 지원할 수 있으며 각 데이터 원본 뷰에 여러 테이블을 포함할 수 있습니다. 그러나 배포 때문에 데이터 원본 및 데이터 원본 뷰가 됩니다 하 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 사용자가 만든 테이블만 각 데이터 원본 뷰에 포함 해야 하는 모범 사례로 데이터 마이닝 모델과 함께 데이터베이스 각 데이터 마이닝 모델 또는 모델 그룹에 대 한 필수 이며  
  
 다음 단원에서는 각 새 시나리오를 지원하기 위해 데이터 원본 뷰를 추가합니다. 시장 바구니 및 시퀀스 클러스터링 단원에서만 동일한 데이터 원본 뷰를 사용하고 각 시나리오에서 다른 데이터 원본 뷰를 사용하므로 두 단원은 서로 독립적이며 별도로 완료할 수 있습니다.  
  
|시나리오|데이터 원본 뷰에 포함된 데이터|  
|--------------|-------------------------------------------|  
|[2 단원: 예측 시나리오 구축 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)|단일 뷰로 수집된 여러 지역의 자전거 모델에 대한 월별 판매 보고서|  
|[3 단원: 시장 바구니 시나리오 구축 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)|고객 주문 목록이 포함된 테이블 및 각 고객의 개별 구매가 표시된 중첩 테이블|  
|[4 단원: 시퀀스 클러스터링 시나리오 구축 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)|항목이 구매된 순서를 표시하는 식별자를 추가하여 시장 바구니 분석에 사용되는 동일한 데이터|  
|[5 단원: 신경망 및 로지스틱 회귀 모델 작성 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)|콜 센터에서 받은 일부 예비 성과 추적 데이터가 포함된 단일 테이블|  
  
## <a name="next-lesson"></a>다음 단원  
 [2 단원: 예측 시나리오 구축 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 프로젝트](../../2014/analysis-services/data-mining/data-mining-projects.md)   
 [다차원 모델의 데이터 원본 뷰](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
