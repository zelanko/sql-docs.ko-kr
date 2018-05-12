---
title: ADOMD.NET 클라이언트 프로그래밍 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fbef1da93d4edd44cedbf89ef52133a22b5bb6d9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="adomdnet-client-programming"></a>ADOMD.NET 클라이언트 프로그래밍
  ADOMD.NET 클라이언트 구성 요소 내에 있는 **Microsoft.AnalysisServices.AdomdClient** 네임 스페이스 (microsoft.analysisservices.adomdclient.dll). 이러한 클라이언트 구성 요소가 클라이언트에 대 한 기능 및 중간 계층 응용 프로그램을 쉽게 쿼리 데이터와 메타 데이터는 분석 데이터 저장소에서 제공와 같은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="using-the-adomdnet-client-objects"></a>ADOMD.NET 클라이언트 개체 사용  
 분석 데이터 원본을 쿼리할 경우 일반적인 일련의 태스크를 수행해야 합니다. 다음 표에서는 쿼리 수행과 같이 ADOMD.NET 클라이언트 개체를 사용할 때 필요한 일반적인 태스크를 보여 줍니다.  
  
|태스크|Description|  
|----------|-----------------|  
|[ADOMD.NET에서 연결 설정](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)|ADOMD.NET에서 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스와 같은 분석 데이터 원본에 대한 연결을 설정합니다. <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체를 사용하여 분석 데이터 원본에 대해 명령을 실행하고 데이터 및 메타데이터를 검색할 수 있습니다.|  
|[분석 데이터 원본에서 메타데이터 검색](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)|연결이 설정된 후에는 다양한 개체를 사용하여 내부 데이터 원본에 대한 정보를 검색할 수 있습니다. 응용 프로그램에서 이 기능을 사용하여 연결된 데이터 원본을 적용할 수 있습니다.|  
|[분석 데이터 원본에 대한 명령 실행](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md)|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 개체는 내부 분석 데이터 원본에 대한 명령을 실행하는 데 필요한 인터페이스를 제공합니다.|  
|[분석 데이터 원본에서 데이터 검색](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)|데이터를 검색할 수 없습니다 및 중 하나를 사용 하 여 구문 분석 명령을 실행 한 후의 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, 또는 **System.XmlReader** 개체입니다.|  
|[ADOMD.NET에서 트랜잭션 수행](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-performing-transactions.md)|이 표의 이전 행에 나열된 모든 동작은 커밋된 읽기 트랜잭션 내에서 발생할 수 있습니다. 데이터를 읽는 동안 더티 읽기를 방지하기 위해 공유 잠금이 유지되지만 트랜잭션이 끝나기 전에 데이터가 변경되어 반복되지 않은 읽기나 팬텀 데이터가 생성될 수도 있습니다. <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 개체는 ADOMD.NET에서 트랜잭션 기능을 제공합니다.|  
  
 ADOMD.NET 개체 계층 구조와의 상호 작용은 일반적으로 다음 표에 설명된 최상위 레이어에 있는 하나 이상의 개체에서 시작됩니다.  
  
|수행할 작업|사용 개체|  
|--------|---------------------|  
|분석 데이터 원본에 연결|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체는 데이터 원본 및 데이터 원본 메타데이터 모두에 대한 연결을 나타냅니다. 예를 들어에 연결할 수는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (.cub) 로컬 큐브 파일을 선택한 다음 검사는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Cubes%2A> 분석 데이터 원본에 있는 큐브에 대 한 메타 데이터를 가져올 속성입니다. 이 개체의 구현을 나타냅니다는 **IDbConnection** 인터페이스, 모든.NET Framework 데이터 공급자에 필요한 인터페이스입니다.|  
|데이터 원본의 데이터 마이닝 기능 검색|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체는 여러 마이닝 컬렉션을 노출합니다.<br /><br /><br /><br /> <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelCollection>에는 데이터 원본의 모든 마이닝 모델 목록이 들어 있습니다.<br /><br /><br /><br /> <xref:Microsoft.AnalysisServices.AdomdClient.MiningServiceCollection>은 사용 가능한 마이닝 알고리즘에 대한 정보를 제공합니다.<br /><br /><br /><br /> <xref:Microsoft.AnalysisServices.AdomdClient.MiningStructureCollection>은 서버의 마이닝 구조에 대한 정보를 표시합니다.|  
|데이터 원본 쿼리|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 개체는 서버로 전송될 쿼리 또는 문을 나타냅니다. 데이터 원본에 연결된 후에는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 개체를 사용하여 MDX(Multidimensional Expressions) 또는 데이터 마이닝 DMX(Data Mining Extensions)와 같은 지원되는 언어로 문을 실행할 수 있습니다. <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 개체를 사용하여 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 또는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 개체 형식으로 결과를 반환할 수도 있습니다.|  
|빠르고 효율적인 방법으로 데이터 검색|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 개체의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader%2A> 또는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 메서드를 호출하여 만들 수 있습니다. 이 개체를 구현 하는 **지** 에서 인터페이스는 **System.Data** .NET Framework 클래스 라이브러리의 네임 스페이스입니다.|  
|많은 양의 메타데이터를 사용하여 분석 데이터 검색|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet><br /> <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>은 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A>의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A> 또는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 메서드를 호출하여 만들 수 있습니다. <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>에서 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>이 반환되면 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>에 들어 있는 분석 데이터를 검사할 수 있습니다.|  
|사용 가능한 차원, 측정값, 명명된 집합 등의 큐브에 대한 메타데이터 검색|<xref:Microsoft.AnalysisServices.AdomdClient.CubeDef><br /> <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef>는 큐브에 대한 메타데이터를 나타냅니다. <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef>는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>을 통해 참조됩니다.|  
|데이터를 사용 하 여 검색 된 **System.Data.IDbDataAdapter** 인터페이스|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter><br /> <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter>는 기존 .NET Framework 클라이언트 응용 프로그램에 대한 읽기 전용 지원을 제공합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [ADOMD.NET 서버 프로그래밍](../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)   
 [ADOMD.NET을 사용 하 여 개발](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)  
  
  
