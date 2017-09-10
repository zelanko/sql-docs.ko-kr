---
title: "날짜 유형 차원 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time dimensions [Analysis Services]
- dimensions [Analysis Services], time
- adding time intelligence
- server time dimensions [Analysis Services]
- calendars [Analysis Services]
- time intelligence [Analysis Services]
ms.assetid: 6d692856-4b01-4dca-a650-f97ac220c114
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 52470e4818d24aeb2288d41f60114f040e669cd6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="database-dimensions---create-a-date-type-dimension"></a>데이터베이스 차원-날짜 유형 차원 만들기
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 시간 차원은 년, 반기, 분기, 월, 일 등의 기간을 나타내는 특성이 포함된 차원 유형입니다. 분석 및 보고와 관련하여 시간 차원의 기간은 시간을 기준으로 세분화됩니다. 특성은 계층으로 구성되며 시간 차원 세분성은 주로 기록 데이터에 대한 비즈니스 및 보고 요구 사항에 따라 결정됩니다. 예를 들어 비즈니스 인텔리전스 응용 프로그램의 재무 데이터와 영업 데이터에는 대부분 월별 또는 분기별 세분성이 사용됩니다.  
  
 일반적으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 큐브는 시간 차원을 한 형식이나 다른 형식으로 포함합니다. 데이터의 세분성과 보고 요구 사항에 따라 큐브는 둘 이상의 시간 차원이나 동일한 시간 차원의 여러 계층을 포함할 수 있습니다. 그러나 모든 큐브에 시간 차원이 필요한 것은 아닙니다. 작업 기준 차원에서의 비용 계산은 시간이 아닌 작업을 기준으로 하기 때문에 작업 기준 비용 계산과 같은 일부 OLAP 응용 프로그램에는 시간 차원이 필요하지 않습니다.  
  
## <a name="dimension-structure"></a>차원 구조  
 시간 차원에 대한 차원 구조는 기본 데이터 원본에 기간 정보가 저장되는 방법에 따라 다릅니다. 이러한 차이에 따라 시간 차원에는 다음과 같은 두 가지 기본 유형이 있습니다.  
  
 시간 차원  
 시간 차원은 차원 테이블이 차원에 대한 특성을 제공한다는 점에서 다른 차원과 유사합니다. 주 차원 테이블의 각 열은 특정 기간에 대한 특성을 정의합니다.  
  
 다른 차원과 마찬가지로 팩트 테이블은 시간 차원에 대한 차원 테이블과 외래 키 관계에 있습니다. 시간 차원에 대한 키 특성은 주 차원 테이블에 나타나는 날짜 등의 가장 낮은 수준의 정보 또는 정수 키를 기준으로 합니다.  
  
 서버 시간 차원  
 시간 관련 특성을 바인딩할 차원 테이블이 없으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 기간에 따라 서버 시간 차원을 정의하도록 할 수 있습니다. 서버 시간 차원에서 나타낼 계층, 수준 및 멤버를 정의하려면 차원을 만들 때 표준 기간을 선택합니다.  
  
 서버 시간 차원의 특성에는 특수한 시간-특성 바인딩이 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 Year, Month 또는 Day와 같이 날짜와 관련된 특성 유형을 사용하여 시간 차원에서 특성의 멤버를 정의합니다.  
  
 큐브에 서버 시간 차원을 포함한 후 큐브 마법사의 **차원 용도 정의** 페이지에서 관계를 지정하여 측정값 그룹과 서버 시간 차원 간의 관계를 설정합니다.  
  
### <a name="calendars"></a>달력  
 시간 차원이나 서버 시간 차원에서 기간 특성은 계층으로 그룹화됩니다. 이러한 계층을 일반적으로 달력이라고 합니다.  
  
 비즈니스 인텔리전스 응용 프로그램의 경우 여러 개의 달력을 정의해야 하는 경우가 많습니다. 예를 들어 인사과에서 1월 1일로 시작하여 12월 31일로 끝나는 12개월 양력 달력인 *표준* 달력을 사용하여 직원 기록을 추적할 수 있습니다. 이와 동시에 인사과에서는 조직에서 사용하는 회계 연도를 정의하는 12개월 달력인 *회계* 달력을 사용하여 지출을 추적할 수 있습니다.  
  
 이와 같이 다양한 달력을 차원 디자이너에서 직접 구성할 수 있습니다. 그러나 시간 차원이나 서버 시간 차원을 만들 때 차원 마법사가 제공하는 여러 계층 템플릿을 사용하면 다양한 유형의 달력이 자동으로 생성됩니다. 다음 표에서는 차원 마법사가 생성할 수 있는 다양한 달력을 설명합니다.  
  
|달력|Description|  
|--------------|-----------------|  
|표준 달력|1월 1일로 시작하여 12월 31일로 끝나는 12개월 일반 달력입니다.<br /><br /> 차원 마법사를 사용하여 시간 차원을 만드는지 서버 시간 차원을 만드는지 여부에 관계없이 차원에 대한 기간을 나타내는 특성을 정의하면 마법사가 표준 달력에 대한 계층을 생성합니다. 차원 마법사를 사용하여 서버 시간 차원을 만들 경우 표준 달력의 시작 날짜를 1월 1일이 아닌 다른 날짜로 조정할 수 있습니다.|  
|회계 달력|12개월 회계 달력입니다. 이 달력을 선택할 경우 조직에서 사용하는 회계 연도의 시작 월과 일을 지정해야 합니다.<br /><br /> 참고: 이 달력은 차원 마법사를 사용하여 서버 시간 차원을 만드는 경우에만 사용할 수 있습니다.|  
|보고/마케팅 달력|각각 4주로 이루어진 두 달과 5주로 이루어진 한 달이 3개월(분기)마다 반복되는 12개월 보고 달력입니다. 이 달력을 선택할 경우 시작 월과 일을 지정해야 하며 4-4-5, 4-5-4 또는 5-4-4주와 같은 3개월 패턴을 결정해야 합니다. 여기서 각 숫자는 해당 월의 주 수를 나타냅니다.<br /><br /> 참고: 이 달력은 차원 마법사를 사용하여 서버 시간 차원을 만드는 경우에만 사용할 수 있습니다.|  
|제조 달력|각각 4주로 이루어진 13개 기간을 사용하는 달력으로 3개 기간의 3분기와 4개 기간의 1분기로 나뉩니다. 이 달력을 선택할 경우 조직에서 사용하는 제조 연도의 시작 주(1에서 4 사이)와 월을 지정하고 4개 기간을 포함하는 분기도 식별해야 합니다.<br /><br /> 참고: 이 달력은 차원 마법사를 사용하여 서버 시간 차원을 만드는 경우에만 사용할 수 있습니다.|  
|ISO 8601 달력|ISO(International Organization for Standardization) 날짜와 시간 표현 표준 달력(8601)입니다. 이 달력에는 주(7일) 숫자가 있습니다. ISO 8601 달력의 새해는 일반 달력의 새해보다 며칠 전이나 후에 시작될 수 있습니다. 이 달력의 첫 번째 주는 목요일이 포함된 일반 달력의 첫 번째 주입니다. 따라서 이 주의 첫 번째 요일인 일요일이 실제로 이전 연도에 포함될 수 있습니다.<br /><br /> 참고: 이 달력은 차원 마법사를 사용하여 서버 시간 차원을 만드는 경우에만 사용할 수 있습니다.|  
  
 서버 시간 차원을 만들고 해당 차원에 사용할 기간과 달력을 지정하면 차원 마법사가 지정된 각 달력에 적합한 기간에 대한 특성을 추가합니다. 예를 들어 "년"을 기간으로 사용하는 서버 시간 차원을 만들고 회계 달력과 보고 달력을 모두 포함하는 경우 마법사에서는 차원에 표준 Years 특성과 함께 FiscalYear 및 ReportingYears 특성을 추가합니다. 서버 시간 차원에는 선택한 기간의 조합에 대한 특성도 있습니다. 예를 들어 일과 주를 포함하는 차원의 경우 DayOfWeek 특성이 있습니다. 차원 마법사는 한 달력 유형에 속하는 특성을 조합하여 달력 계층을 만듭니다. 예를 들어 회계 달력 계층에는 회계 연도, 회계 반기, 회계 사분기, 회계 월 및 회계 일자 등의 수준이 포함될 수 있습니다.  
  
## <a name="adding-time-intelligence-with-the-business-intelligence-wizard"></a>비즈니스 인텔리전스 마법사로 시간 인텔리전스 추가  
 시간 차원을 정의하고 큐브에 추가한 후 비즈니스 인텔리전스 마법사를 사용하여 월간 누계, 기간별 누계 및 이동 평균 측정값 등의 시간 인텔리전스 기능을 추가할 수 있습니다. 자세한 내용은 [비즈니스 인텔리전스 마법사를 사용하여 시간 인텔리전스 계산 정의](../../analysis-services/multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md)를 참조하세요.  
  
> [!NOTE]  
>  서버 시간 차원에 시간 인텔리전스를 추가하는 데는 비즈니스 인텔리전스 마법사를 사용할 수 없습니다. 비즈니스 인텔리전스 마법사는 계층을 추가하여 시간 인텔리전스를 지원하며 이 계층은 시간 차원 테이블의 열에 바인딩되어야 합니다. 서버 시간 차원에는 해당 시간 차원 테이블이 없으므로 이러한 추가 계층을 지원할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [시간 테이블을 생성하여 시간 차원 만들기](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [비즈니스 인텔리전스 마법사 F1 도움말](http://msdn.microsoft.com/library/155ac80c-63ae-47aa-9e86-9396e3d920eb)   
 [차원 유형](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
