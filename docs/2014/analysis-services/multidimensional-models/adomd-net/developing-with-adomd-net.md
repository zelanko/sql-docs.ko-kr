---
title: ADOMD.NET과 함께 개발 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ADOMD.NET
ms.assetid: abaf33aa-db55-43bf-8f30-15547559be1d
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1dfdd10ae488633812b61e2a0220f7c22e65e575
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093632"
---
# <a name="developing-with-adomdnet"></a>ADOMD.NET를 사용하여 개발
  ADOMD.NET은는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 데이터 공급자와 통신 하도록 디자인 된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다. TCP/IP 또는 HTTP 연결을 사용하여 XML for Analysis 사양에 맞는 SOAP 요청 및 응답을 송수신하는 XML for Analysis 프로토콜을 통해 분석 데이터 원본과 통신합니다. 명령은 MDX(Multidimensional Expressions), DMX(Data Mining Extensions), ASSL(Analysis Services Scripting Language) 또는 제한된 SQL 구문을 통해 전송될 수 있으며 결과가 반환되지 않을 수도 있습니다. ADOMD.NET 개체 모델을 사용하여 분석 데이터, KPI(핵심 성과 지표) 및 마이닝 모델을 쿼리 및 조작할 수 있습니다. ADOMD.NET을 사용하면 OLE DB 호환 스키마 행 집합을 검색하거나 ADOMD.NET 개체 모델을 사용하여 메타데이터를 보고 작업할 수도 있습니다.  
  
 ADOMD.NET 데이터 공급자로 표시 됩니다는 `Microsoft.AnalysisServices.AdomdClient` 네임 스페이스입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[ADOMD.NET 클라이언트 프로그래밍](../../multidimensional-models-adomd-net-client/adomd-net-client-programming.md)|ADOMD.NET 클라이언트 개체를 사용하여 분석 데이터 원본에서 데이터 및 메타데이터를 검색하는 방법에 대해 설명합니다.|  
|[ADOMD.NET 서버 프로그래밍](../../multidimensional-models-adomd-net-server/adomd-net-server-programming.md)|ADOMD.NET 서버 개체를 사용하여 저장 프로시저 및 사용자 정의 함수를 만드는 방법에 대해 설명합니다.|  
|[ADOMD.NET 재배포](redistributing-adomd-net.md)|ADOMD.NET을 재배포하는 과정에 대해 설명합니다.|  
|<xref:Microsoft.AnalysisServices.AdomdClient>|`Microsoft.AnalysisServices.AdomdClient` 네임스페이스에 포함된 개체에 대해 자세히 설명합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Multidimensional Expression &#40;MDX&#41; 참조](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [Data Mining Extensions &#40;DMX&#41; 참조](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Analysis Services 스키마 행 집합](../../schema-rowsets/analysis-services-schema-rowsets.md)   
 [개발 analysis Services Scripting Language &#40;ASSL&#41;](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [다차원 모델 데이터 액세스 &#40;Analysis Services-다차원 데이터&#41;](../mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)  
  
  
