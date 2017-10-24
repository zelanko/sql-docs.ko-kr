---
title: "저장된 프로시저 디자인 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- stored procedures [Analysis Services], designing
- dependent assemblies [Analysis Services]
- assemblies [Analysis Services]
ms.assetid: af4e7bd5-041b-4a40-9942-0ef6a3af46c6
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7ce4810cec6ebfe861150aa24fea322682dc0e8c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="designing-stored-procedures"></a>저장 프로시저 디자인
  저장 프로시저에서 관리 개체 모델 AMO(Analysis Management Objects) 및 클라이언트 기반 개체 모델 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ADO MD(ActiveX  Data Objects Multidimensional)를 모두 사용할 수 있습니다.  
  
 저장 프로시저는 호출할 MDX(Multidimensional Expressions) 수준에 표시되는 범위(서버 또는 데이터베이스)에 있어야 합니다. 그러나 저장 프로시저를 호출한 후에는 범위가 저장 프로시저의 부모 동작으로 제한되지 않습니다. 저장 프로시저는 저장 프로시저를 호출한 사용자 프로세스의 보안 제한 사항이나 저장 프로시저가 작동 중인 트랜잭션의 제한 사항을 위반하지 않는 한 서버의 모든 범위에서 변경 또는 수정 작업을 수행할 수 있습니다.  
  
 서버 범위 프로시저는 서버의 모든 컨텍스트에서 사용할 수 있습니다. 데이터베이스 범위 저장 프로시저는 저장 프로시저가 정의된 데이터베이스의 컨텍스트에만 표시됩니다.  
  
 다른 MDX 함수와 마찬가지로 저장 프로시저가 먼저 해결되어야 MDX 세션이 계속될 수 있습니다. 저장 프로시저는 실행되는 동안 MDX 세션을 잠급니다. 사용자 상호 작용을 보류하는 MDX 세션을 중지해야 할 특별한 이유가 없다면 MDX 세션을 유지하여 대화 상자와 같은 사용자 상호 작용을 사용하지 않는 것이 좋습니다.  
  
## <a name="dependent-assemblies"></a>종속 어셈블리  
 모든 종속 어셈블리는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 로드되어 CLR(공용 언어 런타임)에서 참조할 수 있어야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 종속 어셈블리를 주 어셈블리와 같은 폴더에 저장하므로 CLR에서 이러한 어셈블리의 함수에 대한 모든 함수 참조가 자동으로 해결됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델 어셈블리 관리](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [저장 프로시저 정의](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  

