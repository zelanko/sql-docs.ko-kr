---
title: 계산 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- calculations [Analysis Services]
- OLAP objects [Analysis Services], calculations
- MDX [Analysis Services], calculations
- calculations [Analysis Services], about calculations
- cubes [Analysis Services], calculations
ms.assetid: 6be84916-fd05-4efc-ab98-6adbbad80154
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ce999e5a301fc6c6a9fd50f241e6863e0ad2cca9
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59241781"
---
# <a name="calculations"></a>새 명명된 집합
  MDX (Multidimensional Expressions) 식 또는 스크립트에 있는 큐브에 계산된 멤버, 명명된 된 집합 또는 범위 할당을 정의 하는 데 사용 되는 계산은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다. 계산을 사용하면 큐브의 데이터가 아니라 큐브의 다른 부분, 다른 큐브 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 외부의 정보까지도 참조할 수 있는 식에 의해 정의된 개체를 추가할 수 있습니다. 또한 계산을 사용하면 큐브의 기능을 확장하여 비즈니스 인텔리전스 응용 프로그램의 융통성과 성능을 높일 수 있습니다. 스크립팅 계산에 대 한 자세한 내용은 참조 하세요. [Introduction to MDX Scripting in Microsoft SQL Server 2005](https://go.microsoft.com/fwlink/?LinkId=81892)합니다. MDX 쿼리 및 계산과 관련 된 성능 문제에 대 한 자세한 내용은 참조는 [SQL Server 2005 Analysis Services 성능 가이드](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide)합니다.  
  
## <a name="calculated-members"></a>계산 멤버  
 계산 멤버는 계산 멤버를 정의할 때 지정한 MDX(Multidimensional Expressions) 식을 사용하여 런타임에 값이 계산되는 멤버입니다.  계산 멤버는 다른 멤버와 마찬가지로 비즈니스 인텔리전스 응용 프로그램에서 사용할 수 있습니다. 계산 멤버는 정의만 큐브에 저장되기 때문에 큐브 크기를 늘리지 않습니다. 값은 쿼리에 응답해야 할 때 메모리에서 계산됩니다.  
  
 측정값 차원을 비롯하여 모든 차원에서 계산 멤버를 정의할 수 있습니다. 측정값 차원에서 생성한 계산 멤버를 계산 측정값이라고 합니다.  
  
 대개 계산 멤버는 큐브에 이미 있는 데이터를 기반으로 하지만 데이터를 산술 연산자, 숫자 및 함수와 결합하여 복잡한 식을 만들 수 있습니다. 또한 LookupCube와 같은 MDX 함수를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 다른 큐브에 있는 데이터에 액세스할 수 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 표준 Visual Studio 함수 라이브러리도 제공하므로 저장 프로시저를 사용하여 현재 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 이외의 원본에서 데이터를 검색할 수 있습니다. 저장된 프로시저에 대 한 자세한 내용은 참조 하세요. [저장 프로시저 정의](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)합니다.  
  
 예를 들어 해운 회사의 중역이 분량 단위당 수익을 기준으로 수익성이 더 좋은 수송 화물 유형을 결정하려는 경우에는  Cargo, Fleet 및 Time 차원과 Price_to_Ship, Cost_to_Ship, Volume_in_Cubic_Meters 측정값이 포함된 Shipments 큐브를 사용합니다. 그러나 이 큐브에는 수익성에 대한 측정값이 없습니다. 다음 식에서 기존 측정값을 결합하여 큐브에 Profit_per_Cubic_Meter라는 측정값으로 계산 멤버를 만들 수 있습니다.  
  
```  
([Measures].[Price_to_Ship] - [Measures].[Cost_to_Ship]) /  
[Measures].[Volume_in_Cubic_Meters]  
```  
  
 계산 멤버를 만든 후 다음에 Shipments 큐브를 찾아볼 때는 다른 측정값들과 함께 Profit_per_Cubic_Meter가 나타납니다.  
  
 계산된 멤버를 만들려면 사용 합니다 **계산**큐브 디자이너의 탭 합니다. 자세한 내용은 참조 하세요. [계산 멤버 만들기](../multidimensional-models/create-calculated-members.md)  
  
## <a name="named-sets"></a>명명된 집합  
 명명된 집합은 집합을 한 개 반환하는 CREATE SET MDX 문 식입니다. MDX 식의 큐브 정의의 일부로 저장 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다. 명명된 집합은 MDX(Multidimensional Expressions) 쿼리에서 재사용하기 위한 용도로 생성됩니다. 명명된 집합을 통해 업무용 사용자는 쿼리를 단순화하고 자주 사용되는 복잡한 집합 식 대신 집합 이름을 사용할 수 있습니다. **관련된 항목:** [명명된 집합 만들기](../multidimensional-models/create-named-sets.md)  
  
## <a name="script-commands"></a>스크립트 명령  
 스크립트 명령은 큐브 정의의 일부로 포함되는 MDX 스크립트입니다. 스크립트 명령을 사용하면 큐브의 일부에만 적용하도록 계산의 범위를 지정하는 등 MDX가 지원하는 거의 모든 동작을 큐브에 수행할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], MDX 스크립트는 전체 큐브 또는 큐브의 특정 지점에서 전체 스크립트의 실행에서 특정 섹션에 적용할 수 있습니다. 기본 스크립트 명령인 CALCULATE 문은 기본 범위를 기반으로 큐브의 셀을 집계된 데이터로 채웁니다.  
  
 기본 범위는 전체 큐브지만 하위 큐브라고 하는 더 제한된 범위를 정의하고 이러한 특정 큐브 공간에만 MDX 스크립트를 적용할 수 있습니다. SCOPE 문은 범위가 종료되거나 다시 정의될 때까지 계산 스크립트 내의 모든 후속 MDX 식 및 문의 범위를 정의합니다. 그런 다음 현재 범위에 MDX 식을 적용하기 위해 THIS 문이 사용됩니다. BACK_COLOR 문을 사용하여 디버깅 시 도움이 되도록 현재 범위의 셀에 대한 배경 셀 색을 지정할 수 있습니다.  
  
 예를 들어 스크립트 명령을 사용하여 이전 기간의 판매량 가중치를 기준으로 시간 및 판매 지역에 걸쳐 직원에게 판매량을 할당할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [다차원 모델의 계산](../multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
