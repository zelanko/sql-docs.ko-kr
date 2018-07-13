---
title: 분석 데이터 원본에서 데이터를 검색할 | Microsoft Docs
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
- data retrieval [ADOMD.NET]
- retrieving data
- ADOMD.NET, data retrieval
- data retrieval [ADOMD.NET], about retrieving data
ms.assetid: 88358189-28aa-4bc7-8dda-5a92e3a012b8
caps.latest.revision: 41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4e5595bd4e001b006cb1dfe62cba40cee3bbb30c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196423"
---
# <a name="retrieving-data-from-an-analytical-data-source"></a>분석 데이터 원본에서 데이터 검색
  연결을 설정하고 쿼리를 만든 후에는 데이터를 검색할 수 있습니다. ADOMD.NET에서 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 개체의 `Execute` 메서드 중 하나를 호출하여 세 가지 다른 개체(<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, <xref:System.Xml.XmlReader> 및 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>)를 사용하는 데이터를 검색할 수 있습니다.  
  
 이러한 세 개체는 각각 다음과 같이 상호 작용과 오버헤드의 균형을 조정합니다.  
  
-   *상호 작용* 개체 모델을 통해 사용할 수 있는 정보의 양과 사용 편의성을 가리킵니다.  
  
-   *오버 헤드가* 개체 모델과 개체 모델에 데이터를 검색 하는 속도에 필요한 메모리 양 서버에 네트워크 연결을 통해 개체 모델을 생성 하는 트래픽 용량을 가리킵니다.  
  
 응용 프로그램에 가장 적합한 데이터 검색 개체를 선택할 수 있도록 다음 표에서는 각 개체의 상호 작용과 오버헤드의 차이점을 보여 줍니다.  
  
|Object|상호 작용|오버헤드|차원 유지|사용량 정보|  
|------------|-------------------|--------------|----------------------------|-----------------------|  
|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>|가장 높음|약간 높음, 데이터 검색 속도가 가장 느림|예|[CellSet을 사용하여 데이터 검색](retrieving-data-using-the-cellset.md)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter>|보통|보통|아니요|[DataAdapter에서 DataSet 채우기](http://go.microsoft.com/fwlink/?LinkId=70016)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>|보통|보통|아니요|[AdomdDataReader를 사용하여 데이터 검색](retrieving-data-using-the-adomddatareader.md)|  
|<xref:System.Xml.XmlReader>|가장 낮음|가장 낮음, 데이터 검색 속도가 가장 빠름|예|[XmlReader를 사용하여 데이터 검색](retrieving-data-using-the-xmlreader.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ADOMD.NET 클라이언트 프로그래밍](adomd-net-client-programming.md)  
  
  
