---
title: ADOMD.NET과 함께 개발 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 794692334fdee4d3cbc87fc9ccf1c2313dcc1262
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34025053"
---
# <a name="developing-with-adomdnet"></a>ADOMD.NET를 사용하여 개발
  ADOMD.NET은는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 데이터 공급자와 통신 하도록 디자인 된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다. TCP/IP 또는 HTTP 연결을 사용하여 XML for Analysis 사양에 맞는 SOAP 요청 및 응답을 송수신하는 XML for Analysis 프로토콜을 통해 분석 데이터 원본과 통신합니다. 명령은 MDX(Multidimensional Expressions), DMX(Data Mining Extensions), ASSL(Analysis Services Scripting Language) 또는 제한된 SQL 구문을 통해 전송될 수 있으며 결과가 반환되지 않을 수도 있습니다. ADOMD.NET 개체 모델을 사용하여 분석 데이터, KPI(핵심 성과 지표) 및 마이닝 모델을 쿼리 및 조작할 수 있습니다. ADOMD.NET을 사용하면 OLE DB 호환 스키마 행 집합을 검색하거나 ADOMD.NET 개체 모델을 사용하여 메타데이터를 보고 작업할 수도 있습니다.  
  
 ADOMD.NET 데이터 공급자는 **Microsoft.AnalysisServices.AdomdClient** 네임스페이스로 표현됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[ADOMD.NET 클라이언트 프로그래밍](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)|ADOMD.NET 클라이언트 개체를 사용하여 분석 데이터 원본에서 데이터 및 메타데이터를 검색하는 방법에 대해 설명합니다.|  
|[ADOMD.NET 서버 프로그래밍](../../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)|ADOMD.NET 서버 개체를 사용하여 저장 프로시저 및 사용자 정의 함수를 만드는 방법에 대해 설명합니다.|  
|[ADOMD.NET 재배포](../../../analysis-services/multidimensional-models/adomd-net/redistributing-adomd-net.md)|ADOMD.NET을 재배포하는 과정에 대해 설명합니다.|  
|<xref:Microsoft.AnalysisServices.AdomdClient>|**Microsoft.AnalysisServices.AdomdClient** 네임스페이스에 포함된 개체에 대해 자세히 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 식 & #40; Mdx& #41; 참조](../../../mdx/multidimensional-expressions-mdx-reference.md)   
 [Data Mining Extensions & #40; DMX & #41; 참조](../../../dmx/data-mining-extensions-dmx-reference.md)   
 [Analysis Services 스키마 행 집합](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [개발 analysis Services Scripting Language &#40;ASSL&#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [다차원 모델 데이터 액세스 &#40;Analysis Services-다차원 데이터&#41;](../../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)  
  
  
