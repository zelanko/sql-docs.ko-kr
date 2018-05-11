---
title: XmlReader를 사용 하 여 데이터를 검색 합니다. | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2c8f4392b3cd37abb57ef2b7294e4b1ed223b27a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="retrieving-data-using-the-xmlreader"></a>XmlReader를 사용하여 데이터 검색
  **XmlReader** 클래스의 일부는 **System.Xml** Microsoft.NET Framework 클래스 라이브러리에 대 한 네임 스페이스는 비슷합니다는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 하는 클래스는 **XmlReader**클래스도 빠르고, 캐시 되지 않은 앞 으로만 이동 가능한 데이터 액세스를 제공 합니다. 필요 하지는 메모리 내 분석 뷰가 사용 하 여 데이터의 경우는 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 개체는 **XmlReader** 개체는 특히 많은 양의 데이터에 대 한 XML 데이터 검색에 대 한 완벽 한 합니다. 때문에 **XmlReader** 데이터를 스트리밍 **XmlReader** 검색 한 경우 것 처럼 호출자에 게 데이터를 제공 하기 전에 모든 데이터를 캐시 하는 없는 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 변환에 사용 된 개체는 XML for Analysis 응답을 분석 개체 모델 표현으로 합니다.  
  
 **XmlReader** 클래스는 ADOMD.NET에서 받은 Analysis 응답에 대 한 XML에 대 한 직접 액세스를 제공 때는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> 의 메서드는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 개체를 호출 합니다. 검색된 데이터는 원시 XML이므로 데이터와 메타데이터를 수동으로 구문 분석해야 합니다. 데이터가 검색 되는 즉시는 **XmlReader** 개체를 닫아야 합니다.  
  
## <a name="retrieving-data-and-metadata"></a>데이터 및 메타데이터 검색  
 사용 하 여 **XmlReader** 데이터를 검색 하는 클래스, 다음이 단계를 수행 합니다.  
  
1.  **개체의 새 인스턴스를 만듭니다.**  
  
     새 인스턴스를 만드는 **XmlReader** 호출 클래스는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 또는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> 의 메서드는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 개체입니다.  
  
2.  **데이터를 검색 합니다.**  
  
     쿼리를 실행 하 고 반환 하는 명령 후는 **XmlReader**, 데이터 및 메타 데이터를 구문 분석 해야 합니다. XML 데이터 및 메타데이터는 XML for Analysis 공급자에서 사용되는 네이티브 형식으로 표현됩니다. 네이티브 형식은 대부분 XML for Analysis 공급자에서 사용 중인는 **MDDataSet** 형식입니다. **MDDataSet** 형식은 셀 집합 구조적인 형식에 대 한 데이터와 메타 데이터를 제공 합니다. 에 대 한 자세한 내용은 **MDDataSet** 형식, XML for Analysis 사양 참조 하십시오.  
  
3.  **판독기를 닫습니다.**  
  
     항상 호출 해야는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> 메서드를 사용 하 여 완료 되 면는 **XmlReader** 개체입니다. 동안는 **XmlReader** 가 열려 있으면 해당 **XmlReader** 단독으로 사용 된 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 명령을 실행 하는 데 사용 된 개체입니다. 사용 하 여 어떤 명령도 실행할 수 없습니다 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>, 하는 등 다른 **XmlReader** 또는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>원래를 닫을 때까지, **XmlReader**합니다.  
  
### <a name="example-of-retrieving-data-from-the-xmlreader"></a>XmlReader에서의 데이터 검색 예  
 다음 예제에서는 명령을 실행 하 고으로 데이터를 검색 한 **XmlReader**, 콘솔 파일의 내용을 출력 합니다.  
  
 [!code-cs[Adomd.NetClient#OutputDataWithXML](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-data-using-th_1_1.cs)]  
  
## <a name="see-also"></a>관련 항목:  
 [분석 데이터 원본에서 데이터 검색](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)   
 [셀 집합을 사용 하 여 데이터를 검색 합니다.](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-cellset.md)   
 [AdomdDataReader를 사용하여 데이터 검색](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)  
  
  
