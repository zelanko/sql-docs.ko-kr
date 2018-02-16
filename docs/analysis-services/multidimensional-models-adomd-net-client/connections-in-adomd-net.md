---
title: "ADOMD.NET에서 연결 설정 | Microsoft Docs"
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- opening connections
- closing connections
- connections [ADOMD.NET]
- ADOMD.NET, connections
ms.assetid: 7b9610f5-6641-42cc-af4e-bd35771913d1
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 36325fc2b6c7dd9ed948b0e5ccf70d41f5df1b9f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="connections-in-adomdnet"></a>ADOMD.NET에서 연결
  ADOMD.NET을 사용 하 여는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체와 같은 분석 데이터 원본 연결을 열려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스. 연결이 더 이상 필요하지 않으면 명시적으로 연결을 닫아야 합니다.  
  
## <a name="opening-a-connection"></a>연결 열기  
 ADOMD.NET에서 연결을 열려면 먼저 연결 문자열을 유효한 분석 데이터 원본 및 데이터베이스로 지정해야 합니다. 그런 다음 해당 데이터 원본에 대한 연결을 명시적으로 열어야 합니다.  
  
### <a name="specifying-a-multidimensional-data-source"></a>다차원 데이터 원본 지정  
 분석 데이터 원본 및 데이터베이스를 지정하려면 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 개체의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 속성을 설정합니다. <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 속성에 지정된 연결 문자열은 OLE DB 호환 문자열입니다. ADOMD.NET에서는 지정된 연결 문자열을 사용하여 서버에 연결하는 방법을 결정합니다.  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 속성은 기존 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체에서 설정되거나 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체의 인스턴스가 만들어지는 동안 설정될 수 있습니다. 다음 코드에서는 ADOMD 연결을 만들 때 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 속성을 설정하는 방법을 보여 줍니다.  
  
```vb  
Dim advwrksConnection As New AdomdConnection("Data Source=localhost;Catalog=AdventureWorksAS")  
System.Diagnostics.Debug.Writeline(advwrksConnection.ConnectionString)  
```  
  
```csharp  
AdomdConnection advwrksConnection = new AdomdConnection("Data Source=localhost;Catalog=AdventureWorksAS");  
System.Diagnostics.Debug.Writeline(advwrksConnection.ConnectionString);  
```  
  
### <a name="opening-a-connection-to-the-data-source"></a>데이터 원본에 대한 연결 열기  
 연결 문자열을 지정한 후에는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> 메서드를 사용하여 연결을 열어야 합니다. <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체를 열 때 연결에 대해 다양한 보안 수준을 설정할 수 있습니다. 값에 따라 연결에 사용 되는 보안 수준을 **ProtectionLevel** 연결 문자열 설정 합니다. ADOMD.NET에서 보안 연결을 여는 방법에 대 한 자세한 내용은 참조 [Establishing Secure Connections in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections.md)합니다.  
  
## <a name="working-with-a-connection"></a>연결 사용  
 각각의 열린 연결은 상태 저장 작업을 지원하는 세션에 존재합니다. 둘 이상의 열린 연결에서 한 세션을 공유할 수 있습니다. 세션을 공유하면 둘 이상의 클라이언트가 같은 컨텍스트를 공유할 수 있습니다. 자세한 내용은 참조 [ADOMD.NET에서 연결 및 세션 작업](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-working-with-connections-and-sessions.md)합니다.  
  
 열린 연결을 사용하여 메타데이터와 데이터를 검색하고 명령을 실행할 수 있습니다. 자세한 내용은 참조 [분석 데이터 원본에서 메타 데이터 가져오기](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md), [분석 데이터 원본에서 데이터 검색](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md), 및 [실행 명령에 대해는 분석 데이터 소스](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md)합니다.  
  
 연결이 열려 있으면 커밋된 읽기 트랜잭션 내에서 데이터와 메타데이터를 검색하고 명령을 실행할 수 있습니다. 데이터를 읽는 동안 더티 읽기를 방지하기 위해 공유 잠금이 유지되지만 트랜잭션이 끝나기 전에 데이터가 변경되어 반복되지 않은 읽기나 팬텀 데이터가 생성될 수도 있습니다. 자세한 내용은 참조 [ADOMD.NET에서 트랜잭션 수행](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-performing-transactions.md)합니다.  
  
## <a name="closing-a-connection"></a>연결 닫기  
 연결이 더 이상 필요하지 않으면 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체를 명시적으로 닫는 것이 좋습니다. 사용할 연결을 명시적으로 닫으려면는 **닫습니다** 및 **Dispose** 의 메서드는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체입니다.  
  
 연결을 명시적으로 닫지 않았으나 연결이 범위를 벗어날 수 있는 경우 서버 리소스를 신속하게 해제하지 못하여 높은 동시성을 요구하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 클라이언트 응용 프로그램에서 새 연결을 효율적으로 열지 못할 수도 있습니다. 연결을 명시적으로 닫지 않은 경우 연결을 만든 방법에 따라 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체에 사용된 세션이 활성 상태로 유지될 수 있습니다.  
  
 세션에 대 한 자세한 내용은 참조 [ADOMD.NET에서 연결 및 세션 작업](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-working-with-connections-and-sessions.md)합니다.  
  
> [!IMPORTANT]  
>  에 **Finalize** 모든 구현 클래스, 호출 하지 않으면는 **닫기** 또는 **Dispose** 의 메서드는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 개체 또는 다른 관리 되는 개체입니다. 종료자에서 구현된 클래스가 직접 소유하는 관리되지 않는 리소스만 해제해야 합니다. 구현 된 클래스는 관리 되지 않는 리소스가 없는 경우 포함 되지 않습니다는 **Finalize** 클래스 정의에서 메서드.  
  
## <a name="see-also"></a>관련 항목:  
 [ADOMD.NET 클라이언트 프로그래밍](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
