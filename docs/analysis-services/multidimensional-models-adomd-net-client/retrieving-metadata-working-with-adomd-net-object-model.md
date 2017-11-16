---
title: "ADOMD.NET 개체 모델 사용 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- metadata [ADOMD.NET]
- object model (client) [ADOMD.NET]
- retrieving metadata
ms.assetid: 0183dcdc-f2ea-4246-ad00-6e8ccc9d8217
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 81a9272284e662eb7f5f47e464e85e324b92a39d
ms.contentlocale: ko-kr
ms.lasthandoff: 10/24/2017

---
# <a name="retrieving-metadata---working-with-adomdnet-object-model"></a>ADOMD.NET 개체 모델 사용-메타 데이터 검색
  ADOMD.NET에서는 분석 데이터 원본에 들어 있는 큐브 및 하위 개체를 보기 위한 개체 모델을 제공합니다. 하지만 개체 모델을 통해 특정 분석 데이터 원본의 모든 메타데이터를 사용할 수 있는 것은 아닙니다. 개체 모델을 통해서는 클라이언트 응용 프로그램에서 사용자가 대화형으로 명령을 생성할 수 있도록 하기 위해 표시하기에 가장 유용한 정보에만 액세스할 수 있습니다. 제공되는 메타데이터의 복잡성이 줄어들기 때문에 ADOMD.NET 개체 모델은 보다 사용하기 쉽습니다.  
  
 ADOMD.NET 개체 모델에서 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체는 분석 데이터 원본에 정의된 OLAP(온라인 분석 처리) 큐브 및 마이닝 모델과 차원, 명명된 집합, 마이닝 알고리즘 등의 관련 개체에 대한 정보에 액세스할 수 있게 해 줍니다.  
  
## <a name="retrieving-olap-metadata"></a>OLAP 메타데이터 검색  
 각 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체에는 사용자 또는 응용 프로그램이 사용할 수 있는 큐브를 나타내는 <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> 개체의 컬렉션이 포함됩니다. <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> 개체는 큐브에 대한 정보뿐 아니라 차원, 핵심 성과 지표, 측정값, 명명된 집합 등 큐브와 관련된 다양한 개체에 대한 정보도 제공합니다.  
  
 여러 OLAP 서버를 지원하도록 설계되거나 일반적인 메타데이터 표시 및 액세스용으로 설계된 클라이언트 응용 프로그램에서 메타데이터를 나타내는 데는 가능하면 항상 <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> 개체를 사용해야 합니다.  
  
> [!NOTE]  
>  공급자 관련 메타데이터나 세부적인 메타데이터 표시 및 액세스의 경우에는 스키마 행 집합을 사용하여 메타데이터를 검색하십시오. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)을 참조하세요.  
  
 다음 예에서는 <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> 개체를 사용하여 로컬 서버에서 표시 가능한 큐브와 큐브 차원을 검색합니다.  
  
 [!code-cs[Adomd.NetClient#RetrieveCubesAndDimensions](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-metadata-work_1_1.cs)]  
  
## <a name="retrieving-data-mining-metadata"></a>데이터 마이닝 메타데이터 검색  
 각 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체에는 데이터 원본의 데이터 마이닝 기능에 대한 정보를 제공하는 몇 개의 컬렉션이 포함됩니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelCollection>에는 데이터 원본의 모든 마이닝 모델 목록이 들어 있습니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningServiceCollection>은 사용 가능한 마이닝 알고리즘에 대한 정보를 제공합니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningStructureCollection>은 서버의 마이닝 구조에 대한 정보를 표시합니다.  
  
 서버에서 마이닝 모델에 대해 쿼리하는 방법을 결정하려면 <xref:Microsoft.AnalysisServices.AdomdServer.MiningModel.Columns%2A> 컬렉션을 반복합니다. 각 <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelColumn> 개체는 다음과 같은 특성을 제공합니다.  
  
-   개체가 입력 열인지 여부(<xref:Microsoft.AnalysisServices.AdomdClient.MiningModelColumn.IsInput%2A>)  
  
-   개체가 예측 열인지 여부(<xref:Microsoft.AnalysisServices.AdomdClient.MiningModelColumn.IsPredictable%2A>)  
  
-   불연속 열과 관련된 값(<xref:Microsoft.AnalysisServices.AdomdClient.MiningModelColumn.Values%2A>)  
  
-   열의 데이터 형식(<xref:Microsoft.AnalysisServices.AdomdClient.MiningModelColumn.Type%2A>)  
  
## <a name="see-also"></a>관련 항목:  
 [분석 데이터 원본에서 메타데이터 검색](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
  

