---
title: Working with Schema Rowsets in ADOMD.NET | Microsoft Docs
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
- metadata [ADOMD.NET]
- retrieving metadata
- schema rowsets [ADOMD.NET]
ms.assetid: 7bf75bf8-f1e1-44f6-ac42-c38a681654cf
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 279cc537776f6c96193026d5f0bccafcbd8f0c8b
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="retrieving-metadata---working-with-schema-rowsets"></a>스키마 행 집합 작업-모든 메타 데이터 검색
  ADOMD.NET 개체 모델에서 사용할 수 있는 메타데이터보다 많은 메타데이터가 필요한 경우 ADOMD.NET에서는 모든 범위의 XMLA (XML for Analysis), OLE DB, OLAP용 OLE DB 및 데이터 마이닝용 OLE DB 스키마 행 집합을 검색할 수 있는 기능을 제공합니다.  
  
 **XML for Analysis 메타 데이터**  
 XML for Analysis 스키마 행 집합에서는 하위 수준의 서버 정보를 검색할 수 있는 방법을 제공합니다. 사용할 수 있는 정보에는 서버에서 사용 가능한 데이터 원본, 공급자에 예약된 키워드, 공급자가 지원하는 리터럴 등이 있습니다. XML for Analysis 스키마 행 집합을 사용하여 공급자가 지원하는 모든 스키마 행 집합을 검색할 수도 있습니다.  
  
 자세한 내용은: [XML for Analysis 스키마 행 집합](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
 **OLE DB 메타 데이터**  
 OLE DB 스키마 행 집합에서는 다양한 공급자의 정보를 검색할 수 있는 산업 표준 방법을 제공합니다.  
  
 자세한 내용은: [OLE DB 스키마 행 집합](../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
 **OLAP 메타 데이터**  
 분석 데이터 원본에 제공되는 스키마 정보에는 분석 데이터 원본에서 사용할 수 있는 데이터베이스 또는 카탈로그, 데이터베이스의 큐브 및 마이닝 모델, 데이터 원본에 있는 큐브의 역할 등이 포함됩니다.  
  
 자세한 내용은: [OLAP 스키마 행 집합 용 OLE DB](../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
 **데이터 마이닝 메타 데이터**  
 스키마 행 집합을 사용하여 OLAP 메타데이터뿐 아니라 마이닝 메타데이터도 검색할 수 있습니다. 사용할 수 있는 행 집합은 데이터베이스에서 사용 가능한 데이터 마이닝 모델, 사용 가능한 마이닝 알고리즘, 알고리즘에 필요한 매개 변수, 마이닝 구조 등에 대한 정보를 노출합니다.  
  
 자세한 내용은: [데이터 마이닝 스키마 행 집합](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
 이러한 여러 스키마 행 집합 각각에 대해 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A> 개체의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 메서드를 통해 GUID 또는 XMLA 이름을 전달하여 행 집합에서 메타데이터를 검색할 수 있습니다.  
  
## <a name="retrieving-metadata-by-passing-guids"></a>GUID를 전달하여 메타데이터 검색  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid> 클래스에는 공급자와 분석 데이터 원본에서 가장 일반적으로 지원되는 스키마 행 집합을 나타내는 필드 목록이 있습니다. 공급자 또는 분석 데이터 원본에서 일반 및 공급자 관련 메타데이터를 모두 검색하려면 다음 메서드 중 하나에서 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid> 개체에 포함된 GUID를 사용합니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
> [!NOTE]  
>  ADOMD.NET 데이터 공급자는 특정 공급자 및 분석 데이터 원본에서 사용할 수 있도록 만든 기능을 통해 스키마 정보를 노출합니다. 각 공급자와 데이터 원본은 다른 메타데이터를 제공할 수 있습니다.  
  
## <a name="retrieving-metadata-by-passing-xmla-names"></a>XMLA 이름을 전달하여 메타데이터 검색  
 다음 메서드에서는 반환할 스키마 정보를 식별하는 XMLA 스키마 이름과 반환된 열에 대한 제한으로 구성된 배열을 인수로 사용합니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
 인스턴스를 반환 하는 이러한 각 방법의 한 **DataSet** 스키마 정보로 채워지는 개체입니다. **DataSet** 에서 개체는는 **System.Data** Microsoft.NET Framework 클래스 라이브러리의 네임 스페이스입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 GetActions 함수는 연결, 큐브 이름, 좌표 및 좌표 형식을 사용, 검색 된 [MDSCHEMA_ACTIONS 행 집합](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-actions-rowset.md), 다음 선택한 좌표에서 사용할 수 있는 작업을 반환 합니다.  
  
 [!code-cs[Adomd.NetClient#GetActions](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-metadata-work_0_1.cs)]  
  
## <a name="see-also"></a>관련 항목:  
 [분석 데이터 원본에서 메타데이터 검색](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
  
