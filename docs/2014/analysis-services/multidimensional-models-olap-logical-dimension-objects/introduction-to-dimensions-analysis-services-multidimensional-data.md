---
title: 차원 소개 (다차원 데이터) (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], about dimensions
- storage [Analysis Services], dimensions
- dimensions [Analysis Services], examples
- storing data [Analysis Services], dimensions
- storage [Analysis Services]
ms.assetid: ab170fdd-4144-42db-9497-690b9189fc25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2dce25d6638c5ec921ec22601ed73d03a2ccb215
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887866"
---
# <a name="introduction-to-dimensions-analysis-services---multidimensional-data"></a>차원 소개(Analysis Services - 다차원 데이터)
  모든 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 차원은 데이터 원본 뷰에서 테이블이 나 뷰의 열을 기반으로 하는 특성 그룹입니다. 차원은 큐브와 독립적으로 존재하며 여러 큐브에서 사용되거나 단일 큐브에서 여러 번 사용되고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 간에 연결될 수 있습니다. 큐브와 독립적으로 존재하는 차원을 데이터베이스 차원이라고 하며 큐브 내의 데이터베이스 차원 인스턴스를 큐브 차원이라고 합니다.  
  
## <a name="dimension-based-on-a-star-schema-design"></a>별모양 스키마 디자인을 기반으로 하는 차원  
 차원의 구조는 기본 차원 테이블의 구조에 의해 크게 좌우됩니다. 가장 간단한 구조를 별모양 스키마라고 하는데 이러한 구조에서 각 차원은 기본 키 - 외래 키 관계에 따라 팩트 테이블에 직접 연결되어 있는 단일 차원 테이블을 기반으로 합니다.  
  
 다음 다이어그램에서는 FactResellerSales 팩트 테이블이 두 개의 [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] 차원 테이블 ( **재판매인** 및 shpromotion)과 관련 된 예제 데이터베이스의 하위 섹션을 보여줍니다. **FactResellerSales** 팩트 테이블의 **ResellerKey** 열은 Sh재판매인 차원 테이블의 **ResellerKey** 기본 키 열에 대 한 외래 키 관계를 정의 합니다. 마찬가지로 **FactResellerSales** 팩트 테이블의 **PromotionKey** 열은 Shpromotion 차원 테이블의 **PromotionKey** 기본 키 열에 대 한 외래 키 관계 를 정의 합니다.  
  
 ![팩트 차원 관계에 대 한 논리적 스키마](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/dimfactrelationship.gif "팩트 차원 관계에 대 한 논리적 스키마")  
  
## <a name="dimension-based-on-a-snowflake-schema-design"></a>눈송이 스키마 디자인을 기반으로 하는 차원  
 차원을 정의하는 데는 여러 테이블의 정보가 필요하기 때문에 좀 더 복잡한 구조가 요구되기도 합니다. 눈송이 스키마라고 하는 이 구조에서 각 차원은 기본 키 - 외래 키 관계로 서로 간에 및 팩트 테이블에 연결되어 있는 여러 테이블의 열 특성을 기반으로 합니다. 예를 들어 다음 다이어그램에서는 **AdventureWorksDW** 샘플 프로젝트의 Product 차원을 완벽 하 게 설명 하는 데 필요한 테이블을 보여 줍니다.  
  
 ![AdventureWorksAS Product 차원에 대 한 테이블](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/dimproduct.gif "AdventureWorksAS Product 차원에 대 한 테이블")  
  
 제품을 완벽하게 설명하려면 해당 제품의 범주와 하위 범주가 Product 차원에 포함되어야 합니다. 그러나이 정보는이에 대 한 주 테이블에 직접 상주 하지 않습니다. 나이의 외래 키 관계를 사용 하는 경우에는가 나이 **하위**범주 테이블에 대 한 외래 키 관계를 사용 하 여 제품 범주에 대 한 정보를 포함할 수 있습니다. Product 차원의 하위 범주입니다.  
  
## <a name="snowflake-schema-versus-reference-relationship"></a>눈송이 스키마 및 참조 관계 비교  
 일부 경우에 눈송이 스키마를 사용하여 여러 테이블을 통해 차원의 특성을 정의하는 방법이나 별도의 두 차원을 정의하고 이 두 차원 간에 참조 차원 관계를 정의하는 방법 중에서 한 가지를 선택할 수 있습니다. 다음 다이어그램에서는 이러한 시나리오를 보여 줍니다.  
  
 ![참조 되는 샘플 차원에 대 한 논리 스키마](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/dimindirect.gif "참조 되는 샘플 차원에 대 한 논리 스키마")  
  
 위의 다이어그램에서 **FactResellerSales** 팩트 테이블은 shgeography 차원 테이블과 외래 키 관계가 없습니다. 그러나 **FactResellerSales** 팩트 테이블은 sh재판매인 차원 테이블과 외래 키 관계에 있습니다 . 그러면이 테이블에는 shgeography 차원 테이블과 외래 키 관계가 있습니다. 각 대리점에 대 한 지리 정보를 포함 하는 재판매인 차원을 정의 하려면이 특성을 지 수 **지리** 및 범위 **재판매인** 차원 테이블에서 검색 해야 합니다. 그러나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 별도의 두 차원을 만든 후 두 차원 간에 참조 차원 관계를 정의하여 측정값 그룹 내에서 두 차원을 연결하는 방식으로 동일한 결과를 얻을 수 있습니다. 참조 차원 관계에 대 한 자세한 내용은 [차원 관계](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)를 참조 하세요.  
  
 이 시나리오에서 참조 차원 관계 사용의 이점은 추가 스토리지 공간 없이 단일 지리 차원을 만든 후 해당 지리 차원을 기반으로 여러 개의 큐브 차원을 만들 수 있다는 점입니다. 예를 들어 지리 큐브 차원 중 하나를 대리점 차원에 연결하고 또 다른 지리 큐브 차원을 고객 차원에 연결할 수 있습니다. **관련 항목:** [차원 관계](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md), [참조 관계 및 참조 관계 속성 정의](../multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)  
  
## <a name="processing-a-dimension"></a>차원 처리  
 차원을 만든 후에는 차원을 처리해야만 해당 차원의 특성 멤버 및 계층을 볼 수 있습니다. 차원의 구조가 변경되거나 해당 기본 테이블의 정보가 업데이트되면 차원을 다시 처리해야만 변경 내용을 볼 수 있습니다. 구조 변경 후에 차원을 처리할 때 차원을 포함하는 큐브도 처리해야 하며 그렇지 않으면 큐브를 볼 수 없습니다.  
  
## <a name="security"></a>보안  
 계층, 수준 및 멤버를 포함한 차원의 모든 하위 개체는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 역할을 통해 보안이 설정됩니다. 차원 보안은 해당 차원을 사용하는 데이터베이스의 모든 큐브에 적용될 수도 있고 특정 큐브에만 적용될 수도 있습니다. 차원 보안에 대 한 자세한 내용은 [차원 &#40;에 대 한 권한 부여 Analysis Services&#41;](../multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md)를 참조 하세요.  
  
## <a name="see-also"></a>관련 항목  
 [차원 저장소](../multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)   
 [차원 번역](../multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [쓰기 가능 차원](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
