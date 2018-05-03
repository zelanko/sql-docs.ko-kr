---
title: 기존 테이블을 사용 하 여 차원 만들기 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ebf7fb99def766b3635743a31fa2cfa37fcbc228
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-dimension-by-using-an-existing-table"></a>기존 테이블을 사용하여 차원 만들기
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 차원 마법사를 사용하여 기존 테이블에서 차원을 만들 수 있습니다. 이렇게 하려면 마법사의 **생성 방법 선택** 페이지에서 **기존 테이블 사용** 옵션을 선택하십시오. 이 옵션을 선택할 경우 마법사는 기존 데이터 원본 뷰에 있는 차원 테이블, 차원 테이블 열, 차원 테이블 열 간의 관계를 기반으로 하여 차원 구조를 만듭니다. 마법사는 원본 테이블과 관련 테이블의 데이터를 샘플링한 다음 이 데이터를 사용하여 차원 테이블 열을 기반으로 하는 특성 열을 정의하고 특성의 계층( *사용자 정의* 계층이라고 함)을 정의합니다. 차원 마법사를 사용하여 차원을 만든 후에는 차원 디자이너를 사용하여 차원의 특성과 계층을 추가, 제거 및 구성할 수 있습니다.  
  
 기존 테이블을 사용하여 차원을 만드는 경우 차원 마법사는 다음 단계로 이루어집니다.  
  
-   원본 정보 지정  
  
-   관련 테이블 선택  
  
-   차원 특성 선택  
  
-   계정 인텔리전스 정의  
  
> [!NOTE]  
>  이 항목에 제시된 정보에 해당하는 단계별 지침은 [차원 마법사를 사용하여 차원 만들기](../../analysis-services/multidimensional-models/create-a-dimension-using-the-dimension-wizard.md)를 참조하세요.  
  
## <a name="specifying-the-source-information"></a>원본 정보 지정  
 원본 정보는 **원본 정보 지정** 페이지에서 지정합니다. 먼저 차원의 기반이 될 테이블을 포함하는 데이터 원본 뷰를 선택합니다. 그런 다음 정의하려는 차원의 주 차원 테이블을 지정합니다. 주 차원 테이블은 팩트 테이블에 직접 연결되는 테이블입니다. 예를 들어 Products 차원에 대해 주 테이블로 Product 테이블을 지정하거나 Employees 차원에 대해 Employee 테이블을 지정합니다. 데이터 원본 뷰의 기본 키를 기반으로 하는 키 열이 자동으로 선택됩니다. 필요에 따라 키 열을 변경할 수도 있습니다. 키 열은 차원의 멤버를 결정합니다. 예를 들어 ProductKey를 Product 차원의 키 열로 정의할 수 있습니다.  
  
 필요에 따라 멤버 이름이 포함된 열을 정의할 수 있습니다. 기본적으로 사용자에게 표시되는 멤버 이름은 키 열의 값입니다. ProductID나 EmployeeID와 같은 키 열의 값은 대개 사용자에게 의미가 없는 고유한 시스템 생성 키입니다. 사용자에게 표시되는 이름을 차원에 있는 다른 열의 해당 값으로 변경하면 사용자에게 보다 의미 있는 정보를 제공할 수도 있습니다. 예를 들어 제품 이름이나 직원 이름을 포함하는 멤버 이름 열을 정의할 수 있습니다. 멤버 이름을 변경할 경우 보다 설명적인 이름이 사용자에게 표시되지만 같은 이름을 공유하는 멤버를 정확하게 구별하기 위해 쿼리에서는 계속 키 열 값이 사용됩니다. 키 열에 대해 복합 키를 지정하는 경우 키 특성에 대한 멤버 값을 제공하는 열도 지정해야 합니다. 특성 속성을 구성하는 방법은 [차원 특성 속성 참조](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)를 참조하세요.  
  
## <a name="selecting-related-tables"></a>관련 테이블 선택  
  
> [!NOTE]  
>  주 차원 테이블에 데이터 원본 뷰에서 정의된 다른 차원 테이블에 대한 관계가 없으면 마법사에서 이 단계를 건너 뜁니다.  
  
 눈송이 차원을 작성하는 경우 **관련 테이블 선택** 페이지에서 추가 특성을 정의할 관련 테이블을 지정합니다. 예를 들어 고객 지리 테이블을 정의할 고객 차원을 작성하는 경우 지리 테이블을 관련 테이블로 정의할 수 있습니다.  
  
## <a name="selecting-dimension-attributes"></a>차원 특성 선택  
 차원 테이블을 선택한 후 **차원 특성 선택** 페이지를 사용하여 차원에 포함시킬 특성을 차원 테이블에서 선택합니다. 모든 차원 테이블의 기본 열을 모두 잠재적인 차원 특성으로 사용할 수 있습니다. 검색하려면 차원 키 특성을 선택하고 설정해야 합니다.  
  
 기본적으로 특성 유형은 **Regular**로 설정됩니다. 그러나 데이터를 보다 잘 나타내는 다른 특성 유형에 특정 특성을 매핑할 수도 있습니다. 예를 들어 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] DW 예제 데이터베이스의 dbo.DimAccount 테이블에는 계정 번호를 제공하는 AccountCodeAlternateKey 열이 있습니다. 이 특성에 대한 유형을 **Regular** 로 설정하는 대신 이 특성을 **Account Number** 유형에 매핑할 수도 있습니다.  
  
> [!NOTE]  
>  차원을 만들 때 차원 유형과 표준 특성 유형을 설정하지 않은 경우 차원을 만든 후 비즈니스 인텔리전스 마법사를 사용하여 이러한 값을 설정하십시오. 자세한 내용은 [차원에 차원 인텔리전스 추가](../../analysis-services/multidimensional-models/bi-wizard-add-dimension-intelligence-to-a-dimension.md) 또는 계정 유형 차원의 경우 [차원에 계정 인텔리전스 추가](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md)를 참조하세요.  
  
 지정된 특성 유형에 따라 자동으로 차원 유형이 설정됩니다. 마법사에서 지정한 특성 유형은 특성의 **Type** 속성을 설정합니다. 차원 및 차원 특성에 대한 **Type** 속성 설정은 서버 및 클라이언트 응용 프로그램에 차원 내용에 대한 정보를 제공합니다. 경우에 따라 이 **Type** 속성 설정은 클라이언트 응용 프로그램에 대한 지침만 제공하며 선택적입니다. 일부 경우에는 계정, 시간 또는 통화 차원에 대한 **Type** 속성 설정이 특정 서버 기반 동작을 결정하며 특정 큐브 동작을 구현하는 데 필요할 수도 있습니다.  
  
 차원 및 특성 유형에 대한 자세한 내용은 [차원 유형](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md), [특성 유형 구성](../../analysis-services/multidimensional-models/attribute-properties-configure-attribute-types.md)을 참조하세요.  
  
## <a name="defining-account-intelligence"></a>계정 인텔리전스 정의  
  
> [!NOTE]  
>  차원 마법사의 **차원 특성 선택** 페이지에서 **계정 유형** 차원 특성을 정의한 경우에만 이 단계가 표시됩니다.  
  
 **계정 인텔리전스 정의** 페이지를 사용하여 계정 유형 차원을 만듭니다. 계정 유형 차원을 만드는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 지원하는 표준 계정 유형을 차원의 계정 유형 특성 멤버에 매핑해야 합니다. 서버에서는 이러한 매핑을 사용하여 각 유형의 계정 데이터에 대해 별개의 집계 함수와 별칭을 제공합니다.  
  
 이러한 계정 유형을 매핑하기 위해 마법사에서 다음 열을 포함하는 테이블을 제공합니다.  
  
-   **원본 테이블 계정 유형** 열 데이터 원본 테이블의 계정 유형이 나열됩니다.  
  
-   **기본 제공 계정 유형** 열에 서버에서 지원하는 해당 표준 계정 유형이 나열됩니다. 원본 데이터에서 표준 이름을 사용하는 경우 자동으로 원본 유형이 서버 유형에 매핑되며 **기본 제공 계정 유형** 열이 이 정보로 채워집니다. 서버에서 계정 유형을 매핑하지 않거나 매핑을 변경하려는 경우 **기본 제공 계정 유형** 열의 목록에서 다른 유형을 선택합니다.  
  
> [!NOTE]  
>  마법사에서 계정 차원을 만들 때 계정 유형이 매핑되어 있지 않은 경우 차원을 만든 후 비즈니스 인텔리전스 마법사를 사용하여 이러한 매핑을 구성하십시오. 자세한 내용은 [차원에 계정 인텔리전스 추가](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md)를 참조하세요.  
  
## <a name="completing-the-wizard"></a>마법사 완료  
 마법사에서 차원 테이블을 검색하여 관계를 찾은 다음 눈송이 차원의 키 특성 간 특성 관계를 자동으로 만듭니다.  
  
 또한 차원에 부모-자식 관계가 있는지도 자동으로 찾습니다. 부모-자식 관계는 부모 특성이 차원의 키 특성 멤버를 참조할 때 존재합니다. 이 관계는 차원의 리프 멤버 간 집계 경로와 계층 관계를 정의합니다. 부모-자식 계층에 대한 자세한 내용은 [부모-자식 계층의 특성](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)을 참조하세요.  
  
 **마법사 완료** 페이지에서 새 차원의 이름을 입력하고 차원 구조를 검토하여 마법사를 완료합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 원본에 시간이 아닌 테이블을 생성 하 여 차원 만들기](../../analysis-services/multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)   
 [시간 테이블을 생성 하 여 시간 차원 만들기](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [차원 특성 속성 참조](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)   
 [시간 테이블을 생성 하 여 시간 차원 만들기](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [데이터 원본에 시간이 아닌 테이블을 생성 하 여 차원 만들기](../../analysis-services/multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  
