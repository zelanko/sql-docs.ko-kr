---
title: "저장된 프로시저 정의 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- stored procedures [Analysis Services]
- OLAP [Analysis Services], stored procedures
- external routines [Analysis Services]
- stored procedures [Analysis Services], about stored procedures
ms.assetid: f9c57d91-f60f-4f0e-8f7f-d87f4ba97b7c
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b70d20ea8ad3cc108076261b692129bf72ccb6ef
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="defining-stored-procedures"></a>저장 프로시저 정의
  저장된 프로시저를 사용 하 여에서 외부 루틴을 호출 하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다. 저장 프로시저에서 호출할 외부 루틴을 C, C++, C#, Visual Basic 또는 Visual Basic .NET과 같은 CLR(공용 언어 런타임) 언어로 작성할 수 있습니다. 저장 프로시저는 한 번 만든 다음 다른 저장 프로시저, 계산 측정값 또는 클라이언트 응용 프로그램과 같은 다양한 컨텍스트에서 호출할 수 있습니다. 저장 프로시저를 사용하면 공통 코드를 한 번 개발한 다음 단일 위치에 저장하여 재사용할 수 있으므로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 개발 및 구현이 간편해집니다. 또한 MDX의 기본 기능에서 제공하지 않는 비즈니스 기능을 응용 프로그램에 추가할 수 있습니다.  
  
 이 섹션에서는 저장 프로시저를 이해하고 디자인하고 구현하는 데 필요한 정보를 제공합니다.  
  
|항목|Description|  
|-----------|-----------------|  
|[저장된 프로시저 디자인](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/designing-stored-procedures.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 사용할 어셈블리를 디자인하는 방법을 설명합니다.|  
|[저장된 프로시저 만들기](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 어셈블리를 만드는 방법을 설명합니다.|  
|[저장된 프로시저 호출](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 어셈블리를 사용하는 방법에 대한 정보를 제공합니다.|  
|[저장된 프로시저의 쿼리 컨텍스트 액세스](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/accessing-query-context-in-stored-procedures.md)|어셈블리를 사용하여 범위 및 컨텍스트 정보에 액세스하는 방법을 설명합니다.|  
|[저장된 프로시저에 대 한 보안을 설정합니다.](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 어셈블리의 보안을 구성하는 방법을 설명합니다.|  
|[저장된 프로시저를 디버깅](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 어셈블리를 디버깅하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델 어셈블리 관리](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
