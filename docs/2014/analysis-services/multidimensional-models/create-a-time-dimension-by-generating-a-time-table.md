---
title: 시간 테이블을 생성 하 여 시간 차원 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time dimensions [Analysis Services]
- dimensions [Analysis Services], time
- time periods [Analysis Services]
- range-based time dimensions [Analysis Services]
- server time dimensions [Analysis Services]
- calendars [Analysis Services]
- table-based time dimensions [Analysis Services]
ms.assetid: 58303326-1361-4c0e-9f3d-642ce69c4f6a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b54bfbdb03f6f2220cf66cb988456b2e6e6a0070
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66076286"
---
# <a name="create-a-time-dimension-by-generating-a-time-table"></a>시간 테이블을 생성하여 시간 차원 만들기
  에서는의 차원 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 마법사를 사용 하 여 원본 데이터베이스에서 사용할 수 있는 시간 테이블이 없을 때 시간 차원을 만들 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 이렇게 하려면 **생성 방법 선택** 페이지에서 다음 옵션 중 하나를 선택하세요.  
  
-   **데이터 원본에 시간 테이블 생성** 기본 데이터 원본에 개체를 만들 수 있는 권한이 있으면 이 옵션을 선택합니다. 그러면 마법사가 시간 테이블을 생성하고 이 시간 테이블을 데이터 원본에 저장한 다음 이 시간 테이블을 기반으로 시간 차원을 만듭니다.  
  
-   **서버에 시간 테이블 생성** 기본 데이터 원본에 개체를 만들 수 있는 권한이 없으면 이 옵션을 선택합니다. 그러면 마법사가 데이터 원본이 아니라 서버에서 테이블을 생성하고 저장합니다. 서버의 시간 테이블을 기반으로 만든 차원을 *서버 시간 차원*이라고 하는데, 마법사는 이 테이블을 기반으로 서버 시간 차원을 만듭니다.  
  
 시간 차원을 만들 때는 기간을 지정하고 차원의 시작 날짜와 종료 날짜도 지정합니다. 마법사는 지정된 기간을 사용하여 시간 특성을 생성합니다. 사용자가 차원을 처리할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 지정된 날짜와 기간을 지원하는 데 필요한 데이터를 생성하고 저장합니다. 마법사는 시간 차원에 대해 생성된 특성을 사용하여 차원에 적합한 계층을 권장합니다. 계층은 다양한 기간 간의 관계를 반영하고 다양한 달력을 고려합니다. 예를 들어 표준 달력 계층에서는 주가 월이 아닌 년으로 균일하게 나뉘기 때문에 주 수준이 연도 수준 아래에는 나타나지만 월 수준 아래에는 나타나지 않습니다. 반면에 제조 또는 보고 달력 계층에서는 주가 월로 균등하게 나뉘므로 주 수준이 월 수준 아래에 나타납니다.  
  
## <a name="define-time-periods"></a>기간 정의  
 마법사의 **기간 정의** 페이지를 사용하여 차원에 포함할 날짜 범위를 지정합니다. 예를 들어 데이터에서 가장 빠른 연도의 1월 1일에 시작하고 이후의 트랜잭션을 허용하도록 현재 연도에서 1~2년 지나 종료되는 범위를 선택할 수도 있습니다. 범위 밖의 트랜잭션은 차원에 대한 `UnknownMemberVisible` 속성 설정에 따라 차원에서 알 수 없는 멤버로 나타나거나 아예 나타나지 않습니다. 데이터에 사용되는 주의 첫 번째 요일을 변경할 수도 있습니다. 기본값은 일요일입니다.  
  
 마법사가 년, 반기, 사분기, 삼분기, 월, 10일, 주, 날짜와 같이 데이터에 적용되는 계층을 만들 때 사용할 기간을 선택합니다. 최소한 "날짜" 기간은 항상 선택해야 합니다. 날짜 특성은 차원의 키 특성이므로 이 특성이 없으면 차원이 제대로 작동할 수 없습니다.  
  
 **시간 멤버 이름의 언어**옆에서 차원 멤버에 레이블을 지정하는 데 사용할 언어를 선택합니다.  
  
 날짜 범위를 기반으로 하는 시간 차원을 만든 후 차원 디자이너를 사용하여 시간 특성을 추가하거나 제거할 수 있습니다. 날짜 특성은 차원의 키 특성이므로 차원에서 제거할 수 없습니다. 사용자가 볼 수 없도록 날짜 특성을 숨기려면 날짜 특성의 `AttributeHierarchyVisible` 속성을 `False`로 변경합니다.  
  
## <a name="select-calendars"></a>달력 선택  
 1월 1일에 시작하고 12월 31일에 끝나는 표준(그레고리력) 12개월 달력은 시간 차원을 만들 때 항상 포함됩니다. 마법사의 **달력 선택** 페이지에서 차원 계층의 기반으로 사용할 추가 달력을 지정할 수 있습니다. 달력 종류에 대한 설명은 [날짜 유형 차원 만들기](database-dimensions-create-a-date-type-dimension.md)를 참조하세요.  
  
 마법사의 **기간 정의** 페이지에서 어떤 기간을 선택했느냐에 따라 달력 선택 항목을 기준으로 차원에 생성되는 특성이 결정됩니다. 예를 들어 마법사의 **기간 정의** 페이지에서 **연도** 와 **분기** 기간을 선택하고 **달력 선택** 페이지에서 **회계 달력** 을 선택하면 회계 달력에 대해 FiscalYear, FiscalQuarter 및 FiscalQuarterOfYear 특성이 만들어집니다.  
  
 또한 마법사는 달력에 대해 생성된 특성으로 구성된 달력별 계층을 만듭니다. 모든 달력에서 계층의 각 수준은 위 수준으로 롤업됩니다. 예를 들어 표준 12개월 달력에서 마법사는 년과 주 또는 년과 월 계층을 만듭니다. 그러나 표준 달력에서 주가 월 내에 균등하게 포함되지 않으므로 년, 월 및 주 계층은 없습니다. 반면에 보고 달력 또는 제조 달력의 주는 월로 균일하게 나뉘므로 이러한 달력에서 주는 월로 롤업됩니다.  
  
## <a name="completing-the-dimension-wizard"></a>차원 마법사 완료  
 **마법사 완료** 페이지에서 마법사에 의해 생성된 특성 및 계층을 검토한 후 시간 차원 이름을 지정합니다. **마침** 을 클릭하여 마법사를 완료하고 차원을 만듭니다. 차원을 완료한 후 차원 디자이너를 사용하여 차원을 변경할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [다차원 모델의 데이터 원본 뷰](data-source-views-in-multidimensional-models.md)   
 [날짜 유형 차원 만들기](database-dimensions-create-a-date-type-dimension.md)   
 [데이터베이스 차원 속성](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)   
 [차원 관계](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [기존 테이블을 사용 하 여 차원 만들기](create-a-dimension-by-using-an-existing-table.md)   
 [데이터 원본에 시간이 아닌 테이블을 생성하여 차원 만들기](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  
