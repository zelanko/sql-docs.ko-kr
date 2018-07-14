---
title: XmlReader를 사용 하 여 데이터를 검색 합니다. | Microsoft Docs
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
- retrieving data
- XmlReader object
- data retrieval [ADOMD.NET], XmlReader object
ms.assetid: 420ec40e-be2d-413a-b4b2-6d2b1756e270
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fa47902131522f807ebe96b0b14a3df28aaf657f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267569"
---
# <a name="retrieving-data-using-the-xmlreader"></a>XmlReader를 사용하여 데이터 검색
  `XmlReader` 클래스의 일부를 `System.Xml` Microsoft.NET Framework 클래스 라이브러리에 대 한 네임 스페이스는 비슷합니다는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 클래스는를 `XmlReader` 클래스에서는 빠르고 캐시 되지 않은, 정방향 전용 데이터에 액세스할 수 합니다. <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 개체를 사용하는 데이터의 메모리 내 분석 뷰가 필요 없는 경우 대량의 XML 데이터를 검색하는 데는 `XmlReader` 개체가 가장 적합합니다. `XmlReader`는 데이터를 스트리밍하므로 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 개체를 사용하여 XML for Analysis 응답을 분석 개체 모델 표현으로 변환할 때처럼 `XmlReader`에서 데이터를 호출자에게 제공하기 전에 모든 데이터를 검색 및 캐시할 필요가 없습니다.  
  
 `XmlReader` 클래스를 사용하면 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> 개체의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 메서드가 호출될 때 ADOMD.NET에서 받은 XML for Analysis 응답에 직접 액세스할 수 있습니다. 검색된 데이터는 원시 XML이므로 데이터와 메타데이터를 수동으로 구문 분석해야 합니다. 또한 데이터가 검색되는 즉시 `XmlReader` 개체를 닫아야 합니다.  
  
## <a name="retrieving-data-and-metadata"></a>데이터 및 메타데이터 검색  
 `XmlReader` 클래스를 사용하여 데이터를 검색하려면 다음 단계를 수행하십시오.  
  
1.  **개체의 새 인스턴스를 만듭니다.**  
  
     `XmlReader` 클래스의 새 인스턴스를 만들려면 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 개체의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> 또는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 메서드를 호출합니다.  
  
2.  **데이터를 검색 합니다.**  
  
     명령을 통해 쿼리를 실행하고 `XmlReader`를 반환한 후에는 데이터와 메타데이터를 구문 분석해야 합니다. XML 데이터 및 메타데이터는 XML for Analysis 공급자에서 사용되는 네이티브 형식으로 표현됩니다. 대부분의 XML for Analysis 공급자에서 사용되는 네이티브 형식은 `MDDataSet` 형식입니다. `MDDataSet` 형식은 셀 집합의 데이터와 메타데이터를 모두 적절한 구조의 형식으로 제공합니다. `MDDataSet` 형식에 대한 자세한 내용은 XML for Analysis 사양을 참조하십시오.  
  
3.  **판독기를 닫습니다.**  
  
     <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> 개체의 사용을 마친 후에는 항상 `XmlReader` 메서드를 호출해야 합니다. `XmlReader`가 열려 있으면 해당 `XmlReader`는 명령을 실행하는 데 사용된 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체를 배타적으로 사용합니다. 원래 `XmlReader`를 닫기 전까지는 다른 `XmlReader` 또는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>를 만드는 명령을 포함하여 해당 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>을 사용하는 어떤 명령도 실행할 수 없습니다.  
  
### <a name="example-of-retrieving-data-from-the-xmlreader"></a>XmlReader에서의 데이터 검색 예  
 다음 예에서는 명령을 실행하고 데이터를 `XmlReader`로 검색한 다음 파일 내용을 콘솔에 출력합니다.  
  
 [!code-csharp[Adomd.NetClient#OutputDataWithXML](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#outputdatawithxml)]  
  
## <a name="see-also"></a>관련 항목  
 [분석 데이터 원본에서 데이터 검색](retrieving-data-from-an-analytical-data-source.md)   
 [CellSet을 사용 하 여 데이터를 검색 합니다.](retrieving-data-using-the-cellset.md)   
 [AdomdDataReader를 사용하여 데이터 검색](retrieving-data-using-the-adomddatareader.md)  
  
  
