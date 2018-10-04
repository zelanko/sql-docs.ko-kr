---
title: AMO 클래스 소개 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Management Objects]
- classes [AMO]
ms.assetid: d3c066bc-f812-4d53-9e96-9e306f2fc580
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ead51a0fadc54f0b68c550bda2a775a64a79b11a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218733"
---
# <a name="introducing-amo-classes"></a>AMO 클래스 소개
  AMO(Analysis Management Objects)는 클라이언트 응용 프로그램에서 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 의 인스턴스를 관리하기 위해 설계된 클래스 라이브러리입니다. AMO 클래스는 데이터베이스, 차원, 큐브, 마이닝 구조 및 모델, 역할 및 권한, 예외 등의 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체를 관리하는 데 사용되는 클래스입니다.  
  
 다음 그림에서는 이 항목에 설명된 클래스의 관계를 보여 줍니다.  
  
 ![AMO 개념 항목에서 검토 된 클래스](../../../analysis-services/dev-guide/media/amo-reviewedclasses.gif "AMO 개념 항목에서 검토 된 클래스")  
  
 AMO 라이브러리는 특정 태스크를 수행하기 위해 논리적으로 관련된 개체 그룹이라고 생각할 수 있습니다. AMO 클래스는 다음과 같이 분류될 수 있습니다. 이 섹션에서는 다음 항목을 다룹니다.  
  
|항목|Description|  
|-----------|-----------------|  
|[AMO 기본 클래스](amo-fundamental-classes.md)|다른 클래스 집합을 사용하는 데 필요한 클래스를 설명합니다.|  
|[AMO OLAP 클래스](amo-olap-classes.md)|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 OLAP 개체를 관리하는 데 사용되는 클래스를 설명합니다.|  
|[AMO 데이터 마이닝 클래스](amo-data-mining-classes.md)|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 데이터 마이닝 개체를 관리하는 데 사용되는 클래스를 설명합니다.|  
|[AMO 보안 클래스](amo-security-classes.md)|다른 개체에 대한 액세스를 제어하고 보안을 유지하는 데 사용되는 클래스를 설명합니다.|  
|[AMO 기타 클래스 및 메서드](amo-other-classes-and-methods.md)|OLAP 또는 데이터 마이닝 관리자의 일상 업무에 도움이 되는 클래스와 메서드를 설명합니다.|  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.AnalysisServices>   
 [논리적 아키텍처 &#40;Analysis Services-다차원 데이터&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [데이터베이스 개체 &#40;Analysis Services-다차원 데이터&#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [Analysis Management Objects를 사용 하 여 개발 &#40;AMO&#41;](developing-with-analysis-management-objects-amo.md)  
  
  
