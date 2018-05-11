---
title: 분석 데이터 원본에서 데이터를 검색할 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 36d17c0e902b5853f6b2d550c34ba96a94e02886
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="retrieving-data-from-an-analytical-data-source"></a>분석 데이터 원본에서 데이터 검색
  연결을 설정하고 쿼리를 만든 후에는 데이터를 검색할 수 있습니다. Adomd.net에서는 세 가지 다른 개체를 사용 하 여 데이터를 검색할 수 있습니다 (<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, 및 <xref:System.Xml.XmlReader>) 중 하나를 호출 하 여는 **Execute** 의 메서드는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 개체입니다.  
  
 이러한 세 개체는 각각 다음과 같이 상호 작용과 오버헤드의 균형을 조정합니다.  
  
-   *대화형 작업* 개체 모델을 통해 사용할 수 있는 정보의 양과 사용 편의성을 의미 합니다.  
  
-   *오버 헤드* 는 개체 모델에서 개체 모델 및 개체 모델이 있는 데이터를 검색 하는 속도에 필요한 메모리 양 서버에 네트워크 연결을 통해 생성 되는 트래픽 용량을 가리킵니다.  
  
 응용 프로그램에 가장 적합한 데이터 검색 개체를 선택할 수 있도록 다음 표에서는 각 개체의 상호 작용과 오버헤드의 차이점을 보여 줍니다.  
  
|개체|상호 작용|오버헤드|차원 유지|사용량 정보|  
|------------|-------------------|--------------|----------------------------|-----------------------|  
|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>|가장 높음|약간 높음, 데이터 검색 속도가 가장 느림|예|[CellSet을 사용하여 데이터 검색](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-cellset.md)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter>|보통|보통|아니요|[DataAdapter에서 DataSet 채우기](http://go.microsoft.com/fwlink/?LinkId=70016)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>|보통|보통|아니요|[AdomdDataReader를 사용하여 데이터 검색](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)|  
|<xref:System.Xml.XmlReader>|가장 낮음|가장 낮음, 데이터 검색 속도가 가장 빠름|예|[XmlReader를 사용 하 여 데이터를 검색 합니다.](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-xmlreader.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ADOMD.NET 클라이언트 프로그래밍](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
