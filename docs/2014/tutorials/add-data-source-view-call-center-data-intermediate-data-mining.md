---
title: 추가 데이터 원본 뷰의 콜 센터 데이터 (중급 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a448e7e4-dbd1-4d31-90bc-4d4a1c23b352
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5da7978db04b0fdf6e1d4f7740857fc5c0cf90ed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62823303"
---
# <a name="adding-a-data-source-view-for-call-center-data-intermediate-data-mining-tutorial"></a>콜 센터 데이터의 데이터 원본 뷰 추가(중급 데이터 마이닝 자습서)
  이 태스크에서는 콜 센터 데이터에 액세스하는 데 사용할 데이터 원본 뷰를 추가합니다. 탐색을 위한 초기 신경망 모델과 권장하는 데 사용할 로지스틱 회귀 모델 모두를 작성하는 데 동일한 데이터가 사용됩니다.  
  
 또한 데이터 원본 뷰 디자이너를 사용하여 요일에 대한 열을 추가합니다. 이는 원본 데이터가 콜 센터 데이터를 날짜별로 추적하더라도 해당 요일이 평일 또는 주중인지 여부에 따라 호출량 및 서비스 품질 측면 모두에 경험적으로 되풀이되는 패턴이 있기 때문입니다.  
  
## <a name="procedures"></a>절차  
  
#### <a name="to-add-a-data-source-view"></a>데이터 원본 뷰를 추가하려면  
  
1.  **솔루션 탐색기**에서 **데이터 원본 뷰**를 마우스 오른쪽 단추로 클릭하고 **새 데이터 원본 뷰**를 선택합니다.  
  
     데이터 원본 뷰 마법사가 열립니다.  
  
2.  **데이터 원본 뷰 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  에 **데이터 원본 선택** 페이지의 **관계형 데이터 원본**를 선택는 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 데이터 원본. 이 데이터 원본을 없는 경우 [Basic Data Mining Tutorial](../../2014/tutorials/basic-data-mining-tutorial.md)합니다. **다음**을 클릭합니다.  
  
4.  에 **테이블 및 뷰 선택** 페이지에서 다음 표에서 선택한 데이터 원본 뷰에 추가 하려면 오른쪽 화살표를 클릭 합니다.  
  
    -   **FactCallCenter (dbo)**  
  
    -   **DimDate**  
  
5.  **다음**을 클릭합니다.  
  
6.  에 **마법사 완료** 페이지에서 데이터 원본 뷰 이름이 기본적으로 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]입니다. 이름을 **CallCenter**를 클릭 하 고 **마침**합니다.  
  
     데이터 원본 뷰 디자이너가 열리면서 표시 합니다 **CallCenter** 데이터 원본 뷰.  
  
7.  데이터 원본 뷰 창 안쪽을 마우스 오른쪽 단추로 누르고 **테이블 추가/제거**합니다. 테이블을 선택 **DimDate** 누릅니다 **확인**합니다.  
  
     간의 관계를 자동으로 추가 해야 합니다 `DateKey` 각 테이블의 열입니다. 이 관계를 사용 하 여 열을 얻어 **EnglishDayNameOfWeek**에서 **DimDate** 테이블 모델에서 사용 합니다.  
  
8.  데이터 원본 뷰 디자이너에서 테이블을 마우스 오른쪽 단추로 클릭 **FactCallCenter**, 선택한 **새 명명 된 계산**합니다.  
  
     에 **명명 된 계산 만들기** 대화 상자에서 다음 값을 입력 합니다.  
  
    |||  
    |-|-|  
    |**열 이름**|DayOfWeek|  
    |**설명**|DimDate 테이블에서 요일을 얻음|  
    |**식**|`(SELECT EnglishDayNameOfWeek AS DayOfWeek FROM DimDate where FactCallCenter.DateKey = DimDate.DateKey)`|  
  
     식은 데이터를 만듭니다 있는지 확인 하려면를 마우스 오른쪽 단추로 클릭할 테이블 **FactCallCenter**를 선택한 후 **데이터 탐색**합니다.  
  
9. 데이터가 사용 가능한지 검토하는 데에 1분 정도 소요되며, 이를 통해 데이터 마이닝에 해당 데이터가 어떻게 사용되는지 알 수 있습니다.  
  
|열 이름|포함|  
|-----------------|--------------|  
|FactCallCenterID|데이터를 데이터 웨어하우스로 가져올 때 만든 임의 키입니다.<br /><br /> 이 열은 고유 레코드를 식별하며 데이터 마이닝 모델에 대한 사례 키로 사용해야 합니다.|  
|DateKey|콜 센터 운영 날짜로, 정수로 표시됩니다. 정수 날짜 키는 데이터 웨어하우스에서 종종 사용되지만, 날짜 값으로 그룹화하려는 경우 날짜/시간 형식으로 날짜를 구할 수도 있습니다.<br /><br /> 공급업체에서 각 운영일의 각 교대조에 대해 별도의 보고서를 제공하기 때문에 날짜는 고유하지 않습니다.|  
|WageType|날짜가 평일인지, 아니면 주말 또는 공휴일인지를 나타냅니다.<br /><br /> 차이가 고객 서비스 품질에서 주중 및 주말에이 열을 입력으로 사용 가능 합니다.|  
|Shift|통화를 기록한 교대조를 나타냅니다. 이 콜 센터는 영업일을 4 개의 교대 합니다. AM, PM1, PM2, 및 자정입니다.<br /><br /> 교대조가 고객 서비스 품질에 영향을 줄 수 있으므로 이를 입력으로 사용합니다.|  
|LevelOneOperators|근무 중인 첫 번째 수준의 전화 상담원 수를 나타냅니다.<br /><br /> 콜 센터 직원은 첫 번째 수준부터 시작하므로 이러한 직원은 덜 숙련되어 있습니다.|  
|LevelTwoOperators|근무 중인 두 번째 수준의 전화 상담원 수를 나타냅니다.<br /><br /> 직원이 두 번째 수준의 전화 상담원이 되기 위해서는 특정 서비스 시간을 기록해야 합니다.|  
|TotalOperators|교대조 동안 근무하는 총 전화 상담원 수입니다.|  
|Calls|교대조 동안 받은 호출 수입니다.|  
|AutomaticResponses|자동 호출 처리 시스템인 IVR(Interactive Voice Response)을 통해 완전히 처리된 호출 수입니다.|  
|Orders|호출 결과로 발생한 주문 수입니다.|  
|IssuesRaised|호출로 인해 생성된 후속 작업이 필요한 문제 수입니다.|  
|AverageTimePerIssue|들어오는 호출에 응답하는 데 필요한 평균 시간입니다.|  
|ServiceGrade|서비스의 전체적인 품질을 나타내는 메트릭으로 측정 한 값을 *중단 율* 전체 교대조에 대 한 합니다. 중단율이 높을수록 고객이 불만을 느끼며 잠재 주문 기회를 놓칠 가능성이 높습니다.|  
  
 데이터는 단일 날짜 열을 기반으로 하는 네 개의 다른 열에 참고: `WageType`, **DayOfWeek**를 `Shift`, 및 `DateKey`합니다. 일반적으로 데이터 마이닝에서는 동일한 데이터로부터 파생된 여러 열을 사용하는 것이 바람직하지 않습니다. 이는 값들이 서로 너무 강한 상관 관계를 갖고 있으며 기타 패턴을 명확하게 나타내지 못할 수 있기 때문입니다.  
  
 하지만 사용 하지 것입니다 `DateKey` 모델에서 너무 많은 고유 값이 들어 있으므로. 간에 직접 관계가 없습니다 `Shift` 하 고 **DayOfWeek**, 및 `WageType` 및 **DayOfWeek** 부분적 으로만 관련 됩니다. 공선성에 대해 염려되는 경우 사용 가능한 전체 열을 사용하여 구조를 만든 다음 각 모델의 서로 다른 열을 무시하고 그 영향을 시험할 수 있습니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [신경망 구조 및 모델 만들기 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [다차원 모델의 데이터 원본 뷰](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
