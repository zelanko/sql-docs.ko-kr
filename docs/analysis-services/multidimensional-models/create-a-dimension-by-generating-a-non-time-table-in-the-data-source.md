---
title: "데이터 원본에 시간이 아닌 테이블을 생성 하 여 차원 만들기 | Microsoft Docs"
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
- data sources [Analysis Services], dimensions without data source
- dimensions [Analysis Services], standard
- dimensions [Analysis Services], creating without data source
- standard dimensions [Analysis Services]
ms.assetid: a37f7a46-7451-4582-ba19-2595196d97bc
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 20035f6d8fff0c5d45b4c807cf6202531156741d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-dimension-by-generating-a-non-time-table-in-the-data-source"></a>데이터 원본에 시간이 아닌 테이블을 생성하여 차원 만들기
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 차원 마법사를 사용하여 기존 데이터 원본 없이 차원을 만들 수 있습니다. 이렇게 하려면 마법사의 **생성 방법 선택** 페이지에서 **데이터 원본에 시간이 아닌 테이블 생성** 옵션을 선택합니다. 기본 데이터 원본에 새 차원 테이블을 만들려면 기본 데이터 원본에 개체를 만들 수 있는 권한이 있어야 합니다. 미리 정의된 데이터 원본 뷰 없이 차원을 정의하는 경우 완전히 새로 차원을 정의하거나 차원 템플릿을 사용할 수 있습니다.  
  
 차원 마법사에서는 일반적인 차원 유형을 작성할 수 있는 예제 차원 템플릿을 제공합니다. 다음 차원 유형 중에서 선택할 수 있습니다.  
  
-   계정  
  
-   Customer  
  
-   날짜  
  
-   Department  
  
-   Destination Currency  
  
-   Employee  
  
-   지리  
  
-   Internet Sales Order Details  
  
-   조직  
  
-   Product  
  
-   홍보 행사  
  
-   Reseller Sales Order Details  
  
-   Reseller  
  
-   Sales Channel  
  
-   Sales Reason  
  
-   Sales Summary Order Details  
  
-   Sales Territory  
  
-   시나리오  
  
-   Source Currency  
  
 각 표준 템플릿에서 지원하는 특성을 선택하여 차원에 포함할 수 있으며 데이터에 자주 사용되는 차원에 대해 고유한 템플릿 파일을 추가할 수도 있습니다. 차원 템플릿은 다음 폴더에 있습니다.  
  
 `C:\Program Files\Microsoft SQL Server\100\Tools\Templates\olap\1033\Dimension Templates`  
  
 차원 마법사를 완료한 후에는 차원 디자이너를 사용하여 차원의 특성과 계층을 추가, 제거 및 구성할 수 있습니다.  
  
 데이터 원본 없이 시간 차원 이외의 다른 차원을 만드는 경우 차원 마법사가 차원 유형을 지정하고 키 특성 및 느린 변경 차원을 식별하는 과정을 단계별로 안내합니다.  
  
## <a name="specify-dimension-type"></a>차원 유형 지정  
 차원 마법사의 **차원 유형 지정** 페이지에서 차원 유형을 지정할 수 있습니다. 템플릿을 기반으로 차원을 작성하는 경우 차원 유형이 자동으로 정의됩니다. 이 페이지에서는 지정된 차원 유형(사용 가능한 경우)의 표준 특성도 선택할 수 있습니다.  
  
 차원 유형에 해당하는 템플릿을 선택한 경우 이 페이지가 해당 차원 유형의 옵션으로 채워집니다. 템플릿을 선택하지 않았거나 해당하는 차원 유형이 없는 경우 기본 차원 유형은 **Regular**입니다. 차원 유형을 선택하지 않은 경우 생성할 차원에 가장 적합한 유형을 선택합니다. **차원 유형**에 적절한 유형이 나열되지 않은 경우 **Regular**를 사용합니다.  
  
 차원 유형을 선택하면 **차원 특성**아래에 해당 차원에 적용할 수 있는 특성 유형이 나열됩니다. 특성 유형을 선택하려면 특성 유형 옆에 있는 **포함** 확인란을 선택하고 **차원 특성**아래에 특성 이름을 입력합니다. 기본 이름은 **특성 유형**과 같습니다.  
  
## <a name="identify-key-attribute-and-changing-dimensions"></a>키 특성 및 변경 차원 식별  
 **차원 키 및 유형 지정** 페이지에서 차원의 키 특성으로 지정할 특성을 선택합니다. 일반적으로 키 특성은 주 차원 테이블의 기본 키 열에 해당하며 대개 차원의 리프 멤버를 인덱싱합니다.  
  
 템플릿을 선택했을 경우 템플릿에 키 특성이 정의되어 있으면 해당 특성이 기본 키 특성입니다. 템플릿을 선택했는데 템플릿에 키 특성이 정의되어 있지 않은 경우 목록의 첫 번째 특성이 기본값이 됩니다. 목록에는 **차원 유형 지정** 페이지에서 선택한 모든 특성이 포함되어 있습니다. **차원 유형 지정** 페이지에서 키 특성으로 선택한 특성 중 하나를 선택할 수 있습니다. 아무 특성도 선택하지 않은 경우에는 마법사에서 자동으로 키 특성을 만들고 차원 이름과 "ID"를 합쳐 이름을 지정합니다.  
  
 마지막으로 차원이 변경 차원인지 여부를 지정합니다. 변경 차원의 멤버는 시간에 따라 계층 구조 내의 여러 위치로 이동합니다. 마법사에서 추가 열을 생성하고 해당 열에 대응하는 특성을 생성합니다. 사용자는 이러한 열을 사용하여 변경에서 팩토링하는 것과 같은 방식으로 차원을 쿼리할 수 있습니다. 이후에 스키마 생성 마법사를 사용하여 만든 모든 패키지는 차원의 느린 변경 차원 특징에 기반하여 서로게이트 키를 관리합니다.  
  
 **변경 차원임** 확인란을 선택한 경우 차원 마법사에서 다음 표에 표시된 특성을 정의합니다.  
  
|Attribute|형식|  
|---------------|----------|  
|SCD 원래 ID|SCDOriginalID|  
|SCD 종료 날짜|SCDEndDate|  
|SCD 시작 날짜|SCDStartDate|  
|SCD 상태|SCDStatus|  
  
 이러한 느린 변경 차원 특성이 정의되어 있는 템플릿을 사용할 경우 기본적으로 **변경 차원임** 확인란이 선택되어 있습니다. 이 확인란의 선택을 취소하면 차원에서 느린 변경 차원 특성이 제거됩니다.  
  
 차원 디자이너를 사용하여 느린 변경 차원의 속성을 구성할 수 있습니다.  
  
## <a name="completing-the-dimension-wizard"></a>차원 마법사 완료  
 **마법사 완료** 페이지에서 새 차원의 이름을 입력하고 차원 구조를 확인합니다. **마침** 을 클릭한 후 스키마 생성 마법사를 시작하려면 **지금 스키마 생성**확인란을 선택합니다. 대부분의 경우 추가 개체를 만들려면 이 확인란을 선택하지 않아야 합니다. 이 확인란을 선택하지 않을 경우 나중에 차원 디자이너를 사용하여 스키마를 생성할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [시간 테이블을 생성하여 시간 차원 만들기](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [시간 테이블을 생성 하 여 시간 차원 만들기](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)  
  
  

