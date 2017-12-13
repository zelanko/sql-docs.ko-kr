---
title: "Analysis Services 데이터 공급자 (AMO, ADOMD.NET, MSOLAP) 설치 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7aedabc-6af9-4698-a7a4-98f894001476
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 7cd7f4a950335557e3fb65d3d504f79af0801de0
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="install-analysis-services-data-providers-amo-adomdnet-msolap"></a>Analysis Services 데이터 공급자(AMO, ADOMD.NET, MSOLAP) 설치
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 은 ADOMD.Net, AMO 및 MSOLAP로 구성 된 Analysis Services 데이터 공급자의 버전 업데이트입니다.  
  
 대부분의 쿼리 기반 데이터 액세스 시나리오의 경우 클라이언트 시스템에 이미 설치된 기존 이전 버전의 데이터 공급자를 사용하여 SQL Server 2016 전용 기능을 사용하는 테이블 형식 모델을 포함하는 SQL Server 2016 Analysis Services 인스턴스의 테이블 형식 및 다차원 모델에 액세스할 수 있습니다. 일반 규칙으로 Excel, Reporting Services 또는 Tableau와 같은 쿼리를 생성하는 클라이언트 응용 프로그램은 Analysis Services 모델에 액세스할 때 최신 데이터 공급자를 요구하면 안 됩니다.  
  
 모델링 및 관리 도구는 적어도 데이터 공급자에 대한 버전 요구 사항을 기준으로 규칙에 대한 예외입니다. 이러한 도구에는 해당 서버에서 개체를 조작하기 위해 대상 서버에 대해 특별히 작성된 데이터 공급자가 있어야 합니다. 다행히 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 와(과) 함께 제공되는 도구는 자동으로 현재 버전의 서버를 준수하는 데이터 공급자를 포함합니다.  Visual Studio 2015용 SQL Server Data Tools에 대한 설치는 SQL Server 2016 Analysis Services용 데이터 공급자를 설치합니다. 마찬가지로 AMO와 ADOMD.Net 모두를 사용하는 SQL Server 2016 Management Studio는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]을(를) 대상으로 하는 두 데이터 공급자를 설치합니다.  
  
 데이터 공급자의 수동 설치를 호출하는 한 시나리오는 AMO(Analysis Services Management Objects)를 사용하는 사용자 지정 응용 프로그램 또는 스크립트입니다. 이 릴리스에는 Microsoft.AnalysisServices.dll 어셈블리의 일부인 새 네임스페이스(Microsoft.AnalysisServices.Core)에 서버 및 데이터베이스와 같은 주요 개체를 이동하는 다시 팩터링된 네임스페이스가 도입되었습니다. AMO를 사용하는 사용자 지정 코드 또는 스크립트가 있는 경우 코드를 다시 컴파일하고 AMO를 통해 Analysis Services의 SQL Server 2016 인스턴스에 직접 연결하는 모든 서버 및 클라이언트 워크스테이션에서 AMO를 수동으로 업데이트해야 합니다.  
  
## <a name="provider-list"></a>공급자 목록  
 다음 표에서는 각 공급자에 대해 설명합니다.  
  
||||  
|-|-|-|  
|공급자|Filename|버전|  
|AMO(Analysis Services Management Objects)|Microsoft.AnalysisServices.dll|13.0.0.0|  
|Analysis Services Core|Microsoft.AnalysisServices.Core.dll|13.0.0.0|  
|Analysis Services(ADOMD.NET)|Microsoft.AnalysisServices.AdomdClient.dll|13.0.0.0|  
|Analysis Services용 OLE DB 공급자(MSOLAP)|MSOLAP130.dll|13.0.0.0|  
  
## <a name="download-and-install-data-provider"></a>데이터 공급자 다운로드 및 설치  
  
1.  [SQL Server 2016에 대한 기능 팩 다운로드 페이지](http://go.microsoft.com/fwlink/?LinkID=398150)로 이동합니다.  
  
2.  **다운로드** 를 클릭하여 개별 구성 요소를 설치합니다.  
  
3.  64비트 컴퓨터의 경우 다음의 전체 또는 일부를 선택합니다(그렇지 않은 경우 해당하는 x86 선택).  
  
    -   ENU\x64\SQL_AS_ADOMD.msi  
  
    -   ENU\x64\SQL_AS_AMO.msi  
  
    -   ENU\x64\SQL_AS_OLEDB.msi  
  
4.  **다음** 을 클릭하여 파일을 다운로드합니다.  
  
5.  각 프로그램을 실행하여 공급자를 설치합니다. ADO.MD 및 AMO 어셈블리는 C:\Windows\assembly\GAC_MSIL에 설치됩니다. Analysis Services OLE DB 공급자는 C:\Program Files\Microsoft Analysis Services\AS OLEDB\130에 설치됩니다.  
  
## <a name="verify-installation"></a>설치 확인  
  
1.  파일 탐색기에서 C:\Windows\Assembly로 이동합니다.  
  
2.  Microsoft.AnalysisServices를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  **버전** 을 클릭하여 최신 빌드가 있는지 확인합니다.  
  
  
