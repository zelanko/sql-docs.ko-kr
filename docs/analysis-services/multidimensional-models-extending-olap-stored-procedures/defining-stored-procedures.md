---
title: 저장된 프로시저 정의 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6a251da65ced87835b6de50d71bd60658db17fd9
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="defining-stored-procedures"></a>저장 프로시저 정의
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  저장된 프로시저를 사용 하 여에서 외부 루틴을 호출 하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다. 저장 프로시저에서 호출할 외부 루틴을 C, C++, C#, Visual Basic 또는 Visual Basic .NET과 같은 CLR(공용 언어 런타임) 언어로 작성할 수 있습니다. 저장 프로시저는 한 번 만든 다음 다른 저장 프로시저, 계산 측정값 또는 클라이언트 응용 프로그램과 같은 다양한 컨텍스트에서 호출할 수 있습니다. 저장 프로시저를 사용하면 공통 코드를 한 번 개발한 다음 단일 위치에 저장하여 재사용할 수 있으므로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 개발 및 구현이 간편해집니다. 또한 MDX의 기본 기능에서 제공하지 않는 비즈니스 기능을 응용 프로그램에 추가할 수 있습니다.  
  
 이 섹션에서는 저장 프로시저를 이해하고 디자인하고 구현하는 데 필요한 정보를 제공합니다.  
  
|항목|Description|  
|-----------|-----------------|  
|[저장 프로시저 디자인](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/designing-stored-procedures.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 사용할 어셈블리를 디자인하는 방법을 설명합니다.|  
|[저장 프로시저 만들기](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 어셈블리를 만드는 방법을 설명합니다.|  
|[저장 프로시저 호출](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 어셈블리를 사용하는 방법에 대한 정보를 제공합니다.|  
|[저장 프로시저의 쿼리 컨텍스트 액세스](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/accessing-query-context-in-stored-procedures.md)|어셈블리를 사용하여 범위 및 컨텍스트 정보에 액세스하는 방법을 설명합니다.|  
|[저장 프로시저의 보안 설정](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 어셈블리의 보안을 구성하는 방법을 설명합니다.|  
|[저장 프로시저 디버깅](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 어셈블리를 디버깅하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델 어셈블리 관리](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
