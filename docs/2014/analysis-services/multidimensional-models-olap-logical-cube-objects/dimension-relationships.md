---
title: 차원 관계 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- relationships [Analysis Services]
- member groups [Analysis Services]
- regular dimensions [Analysis Services]
- many-to-many relationships [Analysis Services]
- cubes [Analysis Services], relationships
- reference dimensions
- dimensions [Analysis Services], relationships
- fact dimensions [Analysis Services]
- relationships [Analysis Services], dimensions
ms.assetid: de54c059-cb0f-4f66-bd70-8605af05ec4f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1fe1521f2eebaa4413b49c315f17a6b1b6a5914
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887935"
---
# <a name="dimension-relationships"></a>차원 관계
  차원 용도는 큐브 차원과 큐브에 있는 측정값 그룹 간의 관계를 정의합니다. 큐브 차원은 특정 큐브에 사용되는 데이터베이스 차원의 인스턴스입니다. 큐브에는 측정값 그룹에 직접 관련되어 있지 않지만 다른 차원 또는 측정값 그룹을 통해 측정값 그룹에 간접적으로 관련될 수 있는 큐브 차원이 있을 수 있습니다. 큐브에 데이터베이스 차원이 나 측정값 그룹을 추가 하면에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 큐브의 데이터 원본 뷰에 있는 차원 테이블과 팩트 테이블 간 관계를 검사 하 고 다음을 검사 하 여 차원 용도를 결정 하려고 합니다. 차원의 특성 간 관계입니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 감지할 수 있는 관계에 대해 차원 용도 설정을 자동으로 지정합니다.  
  
 차원과 측정값 그룹 간 관계는 관계에 참여하는 차원 및 팩트 테이블과 특정 측정값 그룹에서 차원 세분성을 지정하는 세분성 특성으로 구성됩니다.  
  
## <a name="regular-dimension-relationships"></a>일반 차원 관계  
 큐브 차원과 측정값 그룹 간 일반 차원 관계는 차원의 키 열이 팩트 테이블에 직접 조인되어 있을 때 존재하게 됩니다. 이 직접적인 관계는 기본 관계형 데이터베이스의 기본 키-외래 키 관계를 기반으로 하지만 데이터 원본 뷰에 정의 된 논리적 관계를 기반으로 할 수도 있습니다. 일반 차원 관계는 전형적인 별모양 스키마 디자인에서 차원 테이블과 팩트 테이블 간 관계를 나타냅니다. 일반 관계에 대 한 자세한 내용은 [일반 관계 및 일반 관계 속성 정의](../multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md)를 참조 하세요.  
  
## <a name="reference-dimension-relationships"></a>참조 차원 관계  
 큐브 차원과 측정값 그룹 간 참조 차원 관계는 다음 그림에 표시된 것처럼 차원의 키 열이 다른 차원 테이블의 키를 통해 팩트 테이블에 간접적으로 조인될 때 존재하게 됩니다.  
  
 ![논리적 다이어그램, 참조 된 차원 관계](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-refdimension1.gif "논리적 다이어그램, 참조 된 차원 관계")  
  
 참조 차원 관계는 눈송이 스키마 디자인에서 차원 테이블과 팩트 테이블 간 관계를 나타냅니다. 차원 테이블이 눈송이 스키마에 연결되어 있으면 여러 테이블의 열을 사용하여 단일 차원을 정의하거나 별도의 차원 테이블을 기반으로 별도의 차원을 정의한 후 참조 차원 관계 설정을 사용하여 차원 간에 연결을 정의할 수 있습니다. 다음 그림은 눈송이 스키마에서 **Internetsales**라는 팩트 테이블 한 개와 **Customer** 및 **Geography**라는 두 개의 차원 테이블을 보여 줍니다.  
  
 ![논리적 스키마, 참조 된 차원 관계](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-refdim-schema1.gif "논리적 스키마, 참조 된 차원 관계")  
  
 **Customer** 테이블을 차원 기본 테이블로 사용 하 고 **Geography** 테이블을 관련 테이블로 포함 하는 차원을 만들 수 있습니다. 그런 다음 차원과 InternetSales 측정값 그룹 간에 일반 관계가 정의됩니다.  
  
 또는 InternetSales 측정값 그룹과 관련 된 두 개의 차원, 즉 **Customer** 테이블 기반의 차원과 **Geography** 테이블 기반의 차원을 만들 수 있습니다. 그런 후 Customer 차원을 사용하는 참조 차원 관계를 통해 Geography 차원을 InternetSales 측정값 그룹에 연관지을 수 있습니다. 이 경우 InternetSales 측정값 그룹의 팩트를 Geography 차원에 따라 구분하면 팩트는 고객 및 지리별로 차원이 구분됩니다. 해당 큐브에 Reseller Sales라는 두 번째 측정값 그룹이 포함되면 Reseller Sales와 Geography 간에 관계가 없으므로 Reseller Sales 측정값 그룹의 팩트를 Geography 차원에 따라 구분할 수 없습니다.  
  
 다음 그림과 같이 함께 연결할 수 있는 참조 차원 수에는 제한이 없습니다.  
  
 ![논리적 다이어그램, 참조 된 차원 관계](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-refdimension2.gif "논리적 다이어그램, 참조 된 차원 관계")  
  
 참조 관계에 대 한 자세한 내용은 참조 [관계 및 참조 관계 속성 정의](../multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)를 참조 하세요.  
  
## <a name="fact-dimension-relationships"></a>팩트 차원 관계  
 중복 제거 차원이라고 통칭되는 팩트 차원은 차원 테이블의 특성 열이 아닌 팩트 테이블의 특성 열에서 생성되는 표준 차원입니다. 중복을 줄이기 위해 유용한 차원 데이터가 팩트 테이블에 저장되는 경우가 있습니다. 예를 들어 다음 다이어그램에서는 예제 데이터베이스의 **FactResellerSales** 팩트 테이블 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 을 보여 줍니다.  
  
 ![팩트 테이블의 열은 차원을 지원할 수 있습니다] . (https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-factdim.gif "팩트 테이블의 열은 차원을 지원할 수 있습니다") .  
  
 테이블에는 대리점에서 발주하는 주문 행뿐만 아니라 주문 자체에 대한 특성 정보도 포함됩니다. 이전 다이어그램에서 원으로 지정 된 특성은 차원에서 특성으로 사용할 수 있는 **FactResellerSales** 테이블의 정보를 식별 합니다. 이 경우 대리점에서 발주하는 구매 주문 번호와 운송업체 추적 번호의 두 가지 정보가 CustomerPONumber 및 CarrierTrackingNumber 특성 열로 표시됩니다. 이 정보는 흥미로운 내용입니다. 예를 들어 사용자는 단일 추적 번호로 배송 되는 모든 주문에 대 한 총 제품 비용과 같은 집계 된 정보를 확인 하는 데 관심이 있습니다. 그러나 차원 없이는 이러한 두 가지 특성에 대한 차원 데이터를 구성하고 집계할 수 없습니다.  
  
 이론상으로는 FactResellerSales 테이블과 동일한 키 정보를 사용하는 차원 테이블을 만들어 CarrierTrackingNumber와 CustomerPONumber라는 두 가지 다른 특성 열을 이 차원 테이블로 이동할 수 있습니다. 그러나 이렇게 하면 단 두 가지 특성을 별개의 차원으로 표시하기 위해 데이터의 중요 부분이 중복되고 데이터 웨어하우스가 불필요하게 더 복잡해집니다.  
  
> [!NOTE]  
>  팩트 차원은 종종 드릴스루 동작을 지원하는 데 사용됩니다. 동작에 대한 자세한 내용은 [동작&#40;Analysis Services - 다차원 데이터&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md)을 참조하세요.  
  
> [!NOTE]  
>  팩트 관계에서 참조하는 측정값 그룹을 업데이트할 때마다 팩트 차원을 증분 업데이트해야 합니다. 팩트 차원이 ROLAP 차원이면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 처리 엔진에서 모든 캐시를 삭제하고 측정값 그룹을 증분 처리합니다.  
  
 팩트 관계에 대 한 자세한 내용은 [팩트 관계 정의 및 팩트 관계 속성](../multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)을 참조 하세요.  
  
## <a name="many-to-many-dimension-relationships"></a>다 대 다 차원 관계  
 대부분의 차원에서 각 팩트는 하나의 차원 멤버에만 조인되고 단일 차원 멤버는 여러 팩트와 연결될 수 있습니다. 관계형 데이터베이스 용어에서 이 관계를 일 대 다 관계라고 합니다. 그러나 단일 팩트를 여러 차원 멤버에 조인하는 것이 유용한 경우가 종종 있습니다. 예를 들어 은행 고객이 당좌 예금 계정, 저축 예금 계정, 신용 카드 계정 및 투자 계정 등의 여러 계정을 가질 수 있으며 한 계정에 공동 예금주나 여러 예금주가 있을 수도 있습니다. 따라서 이러한 관계로 구성된 Customer 차원에는 단일 계정 트랜잭션과 관련된 여러 멤버가 포함됩니다.  
  
 ![논리적 스키마/다 대 다 차원 관계](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-many-dimension1.gif "논리적 스키마/다 대 다 차원 관계")  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 차원과 팩트 테이블 간에 다 대 다 관계를 정의할 수 있습니다.  
  
> [!NOTE]  
>  다 대 다 차원 관계를 지원하려면 위의 다이어그램과 같이 데이터 원본 뷰에서 관련된 모든 테이블 간에 외래 키 관계를 설정해야 합니다. 그렇지 않으면 차원 디자이너의 **차원 용도** 탭에서 관계를 설정할 때 올바른 중간 측정값 그룹을 선택할 수 없게 됩니다.  
  
 다 대 다 관계에 대 한 자세한 내용은 [다 대 다 관계 정의 및 다 대 다 관계 속성](../multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)을 참조 하세요.  
  
## <a name="see-also"></a>관련 항목  
 [차원&#40;Analysis Services - 다차원 데이터&#41;](../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
