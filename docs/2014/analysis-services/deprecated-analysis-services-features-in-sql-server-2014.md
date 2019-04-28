---
title: SQL Server 2014에서에서 사용 되지 않는 Analysis Services 기능 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, backward compatibility
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
- deprecated features [Analysis Services]
ms.assetid: 2c96ecfe-a170-41d0-bee3-74503f880197
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 620e74b3854b5cc590ffb84e2b8b70b33d0bfcd3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62732233"
---
# <a name="deprecated-analysis-services-features-in-sql-server-2014"></a>SQL Server 2014에서 사용 되지 않는 Analysis Services 기능
  이 항목에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 계속 제공되지만 더 이상 사용되지 않는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]기능에 대해 설명합니다. 이러한 기능은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 이후 릴리스에서 제거될 예정입니다. 새 애플리케이션에는 이러한 기능을 사용하면 안 됩니다.  
  
## <a name="features-not-supported-in-the-next-version-of-sql-server"></a>다음 버전의 SQL Server에서 지원되지 않는 기능  
 아래의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 기능은 다음 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 지원되지 않습니다. 새 개발 작업에서는 이러한 기능을 사용하지 말고, 현재 이러한 기능을 사용하는 애플리케이션은 가능한 한 빨리 수정하십시오.  
  
|범주|사용되지 않는 기능|대체 기능|  
|--------------|------------------------|-----------------|  
|MDX 함수|CalculationPassValue 함수|없음 계산 패스는 OLAP 엔진에서 관리됩니다. 이 함수는 더 이상 필요하지 않습니다.|  
|MDX 함수|CalculationCurrentPass 함수|없음 계산 패스는 OLAP 엔진에서 관리됩니다. 이 함수는 더 이상 필요하지 않습니다.|  
|MDX(Multidimensional Expressions)|NON_EMPTY_BEHAVIOR 쿼리 최적화 프로그램 힌트는 기본적으로 설정됩니다.|향후 릴리스에서는 NON_EMPTY_BEHAVIOR 쿼리 최적화 프로그램 힌트가 기본적으로 해제됩니다. 이 MDX 최적화 힌트를 올바르게 사용하지 않으면 잘못된 결과가 생성될 수 있습니다.|  
|기타|CELL_EVALUATION_LIST 기본 셀 속성|원래는 셀에 적용되는 계산된 수식 목록을 제공했습니다. 이 버전의 Analysis Services에서는 목록이 비어 있습니다.  계산 순서는 이제 MDX 스크립트에서 지정됩니다. 자세한 내용은 [이해 패스 순서 및 계산 순서 &#40;MDX&#41;](multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md)|  
|개체|COM 어셈블리|COM 어셈블리는 보안 위험을 내포할 수 있습니다. 이후 버전에서는 COM 어셈블리에 대한 지원이 제거될 예정입니다.|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>이후 버전의 SQL Server에서 지원되지 않는 기능  
 아래의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 기능은 다음 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 지원되지만 이후 버전에서는 제거될 예정입니다. 어떤 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 제거될지는 결정되지 않았습니다.  
  
|범주|사용되지 않는 기능|대체 기능|  
|--------------|------------------------|-----------------|  
|다차원 모델|원격 파티션|없음 대신 로컬 파티션을 사용합니다. 참조 [로컬 파티션 만들기 및 관리 &#40;Analysis Services&#41; ](multidimensional-models/create-and-manage-a-local-partition-analysis-services.md) 에 대 한 자세한 내용은 합니다.|  
|다차원 모델|원격으로 연결된 측정값 그룹|원격으로 연결된 측정값 그룹은 원격 서버에서 데이터 원본을 사용하여 연결된 측정값 그룹입니다. 연결된 측정값 그룹에 대해 원격 데이터 원본을 사용하는 기능은 현재 사용 중단될 예정입니다.<br /><br /> 이 기능을 대체할 기능은 없습니다. 대신 로컬로 연결된 측정값 그룹을 사용하는 것이 좋습니다. 자세한 내용은 [Linked Measure Groups](multidimensional-models/linked-measure-groups.md) 을 참조하세요.|  
|다차원 모델|차원 쓰기(writeback)|없음 쓰기 기능이 필요한 경우 파티션 쓰기를 사용합니다. 참조 [Set Partition Writeback](multidimensional-models/set-partition-writeback.md) 자세한 내용은 합니다.|  
|다차원 모델|연결된 차원|없음 다른 모델의 차원에 연결하는 대신 차원을 추가 모델에 복사해 보십시오.|  
|MDX|Non_Empty_Behavior 속성|없음 계산 멤버를 만들 때 이 속성을 잘못 설정하면 잘못된 결과가 반환될 수 있는 가능성이 높아집니다. 최근 OLAP 엔진의 최적화로 스파스 데이터 집합에 대한 연산이 향상되어 이 속성의 관련성이 줄어들었습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 이전 버전과의 호환성](analysis-services-backward-compatibility.md)   
 [SQL Server 2014에서에서 지원 되지 않는 Analysis Services 기능](discontinued-analysis-services-functionality-in-sql-server-2014.md)  
  
  
