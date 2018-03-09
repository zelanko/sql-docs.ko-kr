---
title: "쓰기 가능한 파티션을 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- storage [Analysis Services], partitions
- write-enabled partitions [Analysis Services]
- partitions [Analysis Services], write-enabled
- partitions [Analysis Services], storage
- writeback [Analysis Services], partitions
- storing data [Analysis Services], partitions
ms.assetid: 46e7683f-03ce-4af2-bd99-a5203733d723
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 82cafa346d2347afa9022a61d9ffce018d9d0dd8
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="partitions---write-enabled-partitions"></a>파티션-쓰기 가능 파티션
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
큐브의 데이터는 일반적으로 읽기 전용입니다. 그러나 특정 시나리오에 대해 파티션을 쓰기 가능으로 설정할 수 있습니다. 쓰기 가능 파티션을 사용하면 비즈니스 사용자가 셀 값을 변경하고 큐브 데이터에 대한 이러한 변경의 효과를 분석하여 여러 시나리오를 조사해 볼 수 있습니다. 파티션을 쓰기 가능하도록 설정하면 클라이언트 응용 프로그램에서 파티션의 데이터에 변경 내용을 기록할 수 있습니다. 쓰기 저장(writeback) 데이터라고 하는 이러한 변경 내용은 별도의 테이블에 저장되며 측정값 그룹의 기존 데이터를 덮어쓰지 않습니다. 그러나 큐브 데이터의 일부인 것처럼 쿼리 결과에 포함됩니다.  
  
 전체 큐브나 큐브의 특정 파티션만 쓰기 가능으로 설정할 수 있습니다. 쓰기 가능 차원은 각기 다르지만 서로 보완됩니다. 쓰기 가능 파티션을 사용하면 사용자가 파티션 셀을 업데이트할 수 있고 쓰기 가능 차원을 사용하면 사용자가 차원 멤버를 업데이트할 수 있습니다. 이러한 두 기능을 조합하여 사용할 수도 있습니다. 예를 들어 쓰기 가능 큐브나 쓰기 가능 파티션에 쓰기 가능 차원이 포함되지 않아도 됩니다. **관련된 항목:**[쓰기 가능한 차원](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)합니다.  
  
> [!NOTE]  
>  데이터 원본이 Microsoft Access 데이터베이스인 큐브를 쓰기 가능하도록 설정하려면 큐브, 해당 파티션 또는 해당 차원에 대한 데이터 원본 정의에 Microsoft OLE DB Provider for ODBC Drivers를 사용하지 마십시오. 대신 Jet 4.0 OLE를 포함하는 Jet 서비스 팩의 모든 버전이나 Microsoft Jet 4.0 OLE DB Provider를 사용할 수 있습니다. 자세한 내용은 Microsoft 기술 자료 문서를 참조 하십시오. [Microsoft Jet 4.0 데이터베이스 엔진용 최신 서비스 팩을 구하는 방법](http://support.microsoft.com/?kbid=239114)합니다.  
  
 큐브 수 쓰기 가능 모든 해당 측정값이 사용 하는 경우에는 **Sum** 집계 함수입니다. 연결된 측정값 그룹과 로컬 큐브는 쓰기 가능하도록 설정할 수 없습니다.  
  
## <a name="writeback-storage"></a>쓰기 저장(writeback) 저장소  
 비즈니스 사용자의 변경 내용은 현재 표시된 값과 다른 값으로 쓰기 저장 테이블에 저장됩니다. 예를 들어, 최종 사용자가 셀 값 90에서 100 값으로 변경한 경우 **+ 10** 수행한 비즈니스 사용자에 대 한 정보와 변경 시간과 함께 쓰기 저장 테이블에 저장 됩니다. 누적된 변경 내용의 최종 결과가 클라이언트 응용 프로그램에 표시됩니다. 큐브의 원래 값은 유지되고 변경 내용에 대한 감사 내역이 쓰기 저장 테이블에 기록됩니다.  
  
 리프 셀과 리프가 아닌 셀에 대한 변경 내용은 다르게 처리됩니다. 리프 셀은 측정값 그룹에서 참조하는 모든 차원의 측정값과 리프 멤버와의 교집합을 나타냅니다. 리프 셀의 값은 팩트 테이블에서 직접 가져오며 드릴다운으로 더 나눌 수 없습니다. 큐브나 파티션이 쓰기 가능이면 리프 셀을 변경할 수 있습니다. 리프가 아닌 셀은 리프가 아닌 셀을 구성하는 리프 셀 간에 변경 내용을 배포할 수 있는 방법을 클라이언트 응용 프로그램에서 제공하는 경우에만 변경할 수 있습니다. 이러한 프로세스를 할당이라고 하며 MDX(Multidimensional Expressions)의 UPDATE CUBE 문을 통해 관리합니다. 비즈니스 인텔리전스 개발자는 UPDATE CUBE 문을 사용하여 할당 기능을 포함시킬 수 있습니다. 자세한 내용은 참조 [UPDATE CUBE 문을 &#40; Mdx&#41; ](../../mdx/mdx-data-manipulation-update-cube.md).  
  
> [!IMPORTANT]  
>  업데이트된 셀이 겹치지 않을 경우 **Update Isolation Level** 연결 문자열 속성을 사용하여 UPDATE CUBE의 성능을 향상시킬 수 있습니다. 자세한 내용은 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>을 참조하세요.  
  
 클라이언트 응용 프로그램에서 리프가 아닌 셀에 변경 내용을 배포하는지 여부에 관계없이 쿼리를 평가할 때마다 쓰기 저장 테이블의 변경 내용이 리프 셀은 물론 리프가 아닌 셀에도 적용되므로 비즈니스 사용자가 큐브 전체에서 변경 결과를 볼 수 있습니다.  
  
 비즈니스 사용자가 적용한 변경 내용은 다음과 같이 작업할 수 있는 별도의 쓰기 저장 테이블에 보관됩니다.  
  
-   변경 내용을 큐브에 영구적으로 적용하기 위해 테이블을 파티션으로 변환할 수 있습니다. 이렇게 하면 측정값 그룹이 읽기 전용으로 설정됩니다. 변환할 변경 내용을 선택하기 위한 필터 식을 지정할 수 있습니다.  
  
-   테이블을 무시하여 파티션을 원래 상태로 되돌릴 수 있습니다. 이렇게 하면 파티션이 읽기 전용으로 설정됩니다.  
  
## <a name="security"></a>보안  
 큐브 셀에 대한 읽기/쓰기 권한이 있는 역할에 속하는 비즈니스 사용자만 큐브의 쓰기 저장 테이블에 변경 내용을 기록할 수 있습니다. 각 역할에 대해 업데이트할 수 있는 큐브 셀과 업데이트할 수 없는 큐브 셀을 제어할 수 있습니다. 자세한 내용은 참조 [큐브 또는 모델 사용 권한 &#40; 부여 Analysis Services &#41; ](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
## <a name="see-also"></a>관련 항목:  
 [쓰기 가능 차원](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)   
 [집계 및 집계 디자인](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)   
 [파티션 &#40; Analysis Services-다차원 데이터 &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [쓰기 가능 차원](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
