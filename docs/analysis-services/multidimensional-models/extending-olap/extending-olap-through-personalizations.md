---
title: "개별화를 통해 OLAP 확장 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Services, extensibility
ms.assetid: 348e49fc-4390-43c1-9b6c-61b386ff4373
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4a676978e37f257293b863786c3bcfae103ed4c4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="extending-olap-through-personalizations"></a>개별화를 통해 OLAP 확장
  Analysis Services MDX (Multidimensional Expressions) 및 데이터 마이닝 DMX (Extensions) 언어와 함께 사용 하기 위해 다양 한 내장 함수를 제공 합니다. 이러한 함수를 사용하여 표준 통계 계산을 비롯하여 계층에서의 멤버 이동에 이르는 모든 작업을 수행할 수 있습니다. 그러나 복잡하고 강력한 다른 제품에서도 그렇듯이 제품의 기능을 더 확장할 필요성은 언제나 있기 마련입니다.  
  
 따라서 표준 기능이 충분하지 않을 때마다 업무 요구 사항을 완전히 충족시키기 위해 Analysis Services에서는 서비스 인스턴스에 어셈블리 및 개인 설정 확장 프로그램을 추가하는 기능을 제공합니다.  
  
## <a name="assemblies"></a>어셈블리  
 어셈블리를 사용하면 MDX와 DMX의 비즈니스 기능을 확장할 수 있습니다. 원하는 기능을 작성하여 DLL(동적 연결 라이브러리)과 같은 라이브러리에 추가한 후 이 라이브러리를 Analysis Services 인스턴스 또는 Analysis Services 데이터베이스에 어셈블리로 추가하면 됩니다. 그런 다음 MDX 및 DMX 식, 프로시저, 계산, 동작 및 클라이언트 응용 프로그램에서 라이브러리의 공용 메서드를 사용자 정의 함수로 사용할 수 있습니다.  
  
## <a name="personalized-extensions"></a>개인 설정 확장 프로그램  
 SQL Server Analysis Services 개인 설정 확장 프로그램은 플러그 인 아키텍처 구현 개념의 토대입니다. Analysis Services 개인 설정 확장 프로그램은 기존 관리 어셈블리 아키텍처를 간단하고 유용하게 수정하는 한 방법이며, Analysis Services <xref:Microsoft.AnalysisServices.AdomdServer> 개체 모델, MDX(Multidimensional Expression) 구문 및 스키마 행 집합을 통해 노출됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델 어셈블리 관리](../../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Analysis Services 개인 설정 확장 프로그램](../../../analysis-services/multidimensional-models/extending-olap/analysis-services-personalization-extensions.md)  
  
  

