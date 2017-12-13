---
title: "Analysis Services에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: instances of Analysis Services, connections
ms.assetid: 73ee8171-3379-4384-bfc8-071b3eebbc8f
caps.latest.revision: "46"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 683474e873b45eca2fc39d0b8f254da06d205cf2
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="connect-to-analysis-services"></a>Analysis Services에 연결
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]연결 문자열 속성을 설정 또는 서버를 오프 라인 상태로 전환 하기 전에 연결을 해제 하는 방법과 Analysis Services에서는 인증 방법을 지 원하는 연결에 사용 되는 클라이언트 라이브러리에 대 한 자세한 내용은이 섹션의 정보를 사용 합니다.  
  
## <a name="analysis-services-connections"></a>Analysis Services 연결  
 Analysis Services는 TCP를 네트워크 프로토콜로 사용하고 XMLA(XML for Analysis)를 통신 프로토콜로 사용합니다. 가장 낮은 수준에서 Analysis Services와 함께 제공되는 모든 클라이언트 라이브러리는 XMLA-over-TCP를 구현합니다. 원시 XMLA를 기반으로 응용 프로그램을 작성할 수 있지만 대부분의 응용 프로그램과 응용 프로그램 개발자는 클라이언트 라이브러리를 사용하여 개체 모델을 활용하고 개체 모델이 제공하는 코딩 효율성을 이용합니다. 클라이언트를 Analysis Services에 연결하려는 경우 스택 간에 TCP를 사용할 수 없으면 IIS를 중간 연결로 사용할 수 있습니다. IIS를 통해 HTTP 액세스를 사용할 때의 한 가지 이점은 연결 문자열에서 자격 증명을 전달하는 응용 프로그램에서 연결할 수 있다는 것입니다.  
  
 연결과 관련된 모든 논의에는 대개 인증이 포함됩니다. 다른 SQL Server 기능과 달리 Analysis Services는 Windows 자격 증명을 독점적으로 사용합니다. Analysis Services에 대한 백 엔드 연결에는 SQL Server 데이터베이스 인증, 클레임 인증, 양식 기반 인증 또는 다이제스트를 사용할 수 없습니다. 인증에 대한 자세한 내용이 이 섹션에서 제공됩니다.  
  
##  <a name="bkmk_clientApps"></a> 연결 태스크  
  
|링크|태스크 설명|  
|----------|----------------------|  
|[클라이언트 응용 프로그램에서 연결&#40;Analysis Services&#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md)|Analysis Services를 처음 접하는 경우 Analysis Services에서 가장 흔히 사용되는 도구와 응용 프로그램에 대해 알아보려면 이 항목을 읽으세요.|  
|[연결 문자열 속성&#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)|Analysis Services에는 다양한 서버 및 데이터베이스 속성이 포함되어 있으므로 인스턴스나 데이터베이스가 서버에서 구성된 방식과 관계없이 특정 응용 프로그램에 대한 연결을 사용자 지정할 수 있습니다.|  
|[Analysis Services에서 지원하는 인증 방법](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)|이 항목에서는 Analysis Services에서 사용하는 인증 방법을 간단하게 소개합니다.|  
|[Kerberos 제한 위임에 대해 Analysis Services 구성](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)|많은 비즈니스 인텔리전스 솔루션은 인증된 데이터만 각 사용자에게 반환되도록 하기 위해 가장을 필요로 합니다. 이 항목에서는 가장을 사용하기 위한 요구 사항을 알아봅니다. 또한 Kerberos 제한 위임에 대해 Analysis Services를 구성하기 위한 단계에 대해서도 설명합니다.|  
|[Analysis Services 인스턴스에 대한 SPN 등록](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)|Kerberos 인증에는 다중 서버 솔루션에서 사용자 ID를 가장하거나 위임하는 서비스에 대한 유효한 SPN(서비스 사용자 이름)이 필요합니다. Analysis Services에 대한 SPN 등록의 생성 및 단계를 알아보려면 이 항목의 정보를 사용하세요.|  
|[IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)|기본 인증 또는 도메인 경계 교차는 HTTP 액세스에 대해 Analysis Services를 구성하는 두 가지 중요한 이유입니다.|  
|[Analysis Services 연결에 사용되는 데이터 공급자](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md)|Analysis Services는 서버 작업 또는 Analysis Services 데이터에 액세스하기 위한 세 가지 클라이언트 라이브러리를 제공합니다. 이 항목에서는 ADOMD.NET, AMO(Analysis Services Management Objects) 및 Analysis Services OLE DB 공급자(MSOLAP)에 대해 간략하게 소개합니다.|  
|[Analysis Services 서버에서 사용자와 세션 연결 끊기](../../analysis-services/instances/disconnect-users-and-sessions-on-analysis-services-server.md)|이 항목에서는 서버를 오프라인으로 전환하거나 기준 성능 테스트를 수행하기 전에 기존 연결 및 세션을 해제하는 방법에 대해 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [설치 후 구성&#40;Analysis Services&#41;](../../analysis-services/instances/post-install-configuration-analysis-services.md)   
 [Analysis Services에서 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
  
  
