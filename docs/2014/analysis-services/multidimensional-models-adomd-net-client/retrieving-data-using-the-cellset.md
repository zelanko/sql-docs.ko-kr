---
title: CellSet을 사용 하 여 데이터를 검색 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- CellSet object
- retrieving data
- data retrieval [ADOMD.NET], CellSet object
ms.assetid: 77e4ee58-882d-4012-91a3-0565f18a4882
caps.latest.revision: 41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 69e53cab56cf22d6627fd8039e6a46735d934ca7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37178900"
---
# <a name="retrieving-data-using-the-cellset"></a>CellSet을 사용하여 데이터 검색
  <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 개체에서는 분석 데이터 검색에 필요한 상호 작용 기능과 유연성을 제공합니다. <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 개체는 데이터의 원래 차원을 유지하는 기록 데이터 및 메타데이터의 메모리 내 캐시입니다. 또한 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 개체는 연결된 상태뿐 아니라 연결이 끊어진 상태에서도 이동할 수 있습니다. 연결이 끊어진 상태에서도 이동할 수 있으므로 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 개체는 순서에 상관 없이 데이터와 메타데이터를 보는 데 사용할 수 있으며 가장 종합적인 데이터 검색 개체 모델을 제공합니다. 이에 반해 연결이 끊어진 상태에서 이동하는 기능 때문에 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 개체는 오버헤드가 많아서 가장 느리게 채워지는 ADOMD.NET 데이터 검색 개체 모델입니다.  
  
## <a name="retrieving-data-in-a-connected-state"></a>연결된 상태에서 데이터 검색  
 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 개체를 사용하여 데이터를 검색하려면 다음 단계를 수행하십시오.  
  
1.  **개체의 새 인스턴스를 만듭니다.**  
  
     <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 개체의 새 인스턴스를 만들기 위해 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 개체의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A> 또는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 메서드를 호출합니다.  
  
2.  **메타 데이터를 식별 합니다.**  
  
     ADOMD.NET에서는 데이터뿐 아니라 셀 집합의 메타데이터도 검색합니다. 명령을 통해 쿼리가 실행되고 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>이 반환되면 다양한 개체를 통해 메타데이터를 검색할 수 있습니다. 이 메타데이터는 클라이언트 응용 프로그램에서 셀 집합 데이터를 표시하고 상호 작용을 수행하는 데 필요합니다. 예를 들어, 많은 클라이언트 응용 프로그램에서 셀 집합에 있는 지정된 위치의 자식 위치를 드릴다운하거나 계층적으로 표시하는 기능을 제공합니다.  
  
     ADOMD.NET에서 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Axes%2A> 개체의 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.FilterAxis%2A> 및 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 속성은 반환된 셀 집합에서 각각 쿼리 및 slicer 축의 메타데이터를 나타냅니다. 두 속성은 모두 <xref:Microsoft.AnalysisServices.AdomdClient.Axis> 개체에 대한 참조를 반환하며, 이러한 참조에는 각 축에 표시되는 위치가 포함됩니다.  
  
     각 <xref:Microsoft.AnalysisServices.AdomdClient.Axis> 개체에는 해당 축에 사용할 수 있는 튜플 집합을 나타내는 <xref:Microsoft.AnalysisServices.AdomdClient.Position> 개체의 컬렉션이 포함됩니다. 각 <xref:Microsoft.AnalysisServices.AdomdClient.Position> 개체는 <xref:Microsoft.AnalysisServices.AdomdClient.Member> 개체의 컬렉션으로 표현되는 하나 이상의 멤버가 포함된 단일 튜플을 나타냅니다.  
  
3.  **셀 집합 컬렉션에서 데이터를 검색 합니다.**  
  
     ADOMD.NET에서는 메타데이터뿐 아니라 셀 집합의 데이터도 검색합니다. 명령을 통해 쿼리가 실행되고 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>이 반환되면 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Cells%2A>의 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 컬렉션을 사용하여 데이터를 검색할 수 있습니다. 이 컬렉션에는 쿼리의 모든 축이 교차되는 지점을 계산한 값이 들어 있습니다. 따라서 각 교차하는 지점이나 셀에 액세스하기 위해 여러 인덱서가 존재합니다. 인덱서 목록을 보려면 <xref:Microsoft.AnalysisServices.AdomdClient.CellCollection.Item%2A>을 참조하십시오.  
  
### <a name="example-of-retrieving-data-in-a-connected-state"></a>연결된 상태에서 데이터 검색 예  
 다음 예제에서는 로컬 서버에 대한 연결을 만든 후 해당 연결에서 명령을 실행하는 방법을 보여 줍니다. 이 예제에서는 `CellSet` 개체 모델을 사용하여 결과의 구문을 분석합니다. 열의 캡션(메타데이터)은 첫 번째 축에서 검색되고, 각 행의 캡션(메타데이터)은 두 번째 축에서 검색되며, 교차 데이터는 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Cells%2A> 컬렉션을 사용하여 검색됩니다.  
  
 [!code-csharp[Adomd.NetClient#ReturnCommandUsingCellSet](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#returncommandusingcellset)]  
  
## <a name="retrieving-data-in-a-disconnected-state"></a>연결이 끊어진 상태에서 데이터 검색  
 이전 쿼리에서 반환된 XML을 로드하면 활성 연결 없이 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 개체를 사용하여 분석 데이터를 검색하는 종합적인 방법을 제공할 수 있습니다.  
  
> [!NOTE]  
>  연결이 끊어진 상태에서는 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 개체에서 사용 가능한 개체 속성이 모두 사용 가능하지는 않습니다. 자세한 내용은 참조 하세요. <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A>합니다.  
  
### <a name="example-of-retrieving-data-in-a-disconnected-state"></a>연결이 끊어진 상태에서 데이터 검색 예  
 다음 예제는 이 항목의 이전 예제인 메타데이터 및 데이터 예제와 비슷합니다. 그러나 다음 예제에서 명령은 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> 호출로 실행되고 결과가 `System.Xml.XmlReader`로 반환됩니다. 그런 다음 이 `System.Xml.XmlReader`를 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 메서드와 함께 사용하여 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A> 개체를 채웁니다. 이 예제에서는 `System.Xml.XmlReader`를 즉시 로드하지만 데이터를 셀 집합에 로드하기 전에 다른 방법을 사용하여 판독기에 포함된 XML을 하드 디스크에 캐시하거나 해당 데이터를 다른 응용 프로그램에 전송할 수도 있습니다.  
  
 [!code-csharp[Adomd.NetClient#DemonstrateDisconnectedCellset](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#demonstratedisconnectedcellset)]  
  
## <a name="see-also"></a>관련 항목  
 [분석 데이터 원본에서 데이터 검색](retrieving-data-from-an-analytical-data-source.md)   
 [AdomdDataReader를 사용 하 여 데이터를 검색 합니다.](retrieving-data-using-the-adomddatareader.md)   
 [XmlReader를 사용하여 데이터 검색](retrieving-data-using-the-xmlreader.md)  
  
  
