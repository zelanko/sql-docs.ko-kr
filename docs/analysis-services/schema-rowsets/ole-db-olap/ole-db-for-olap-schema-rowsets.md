---
title: "OLAP 스키마 행 집합 용 OLE DB | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- schema rowsets [Analysis Services], OLE DB for OLAP
- OLE DB for OLAP schema rowsets
- schema rowsets [OLE DB for OLAP]
- rowsets [Analysis Services], OLE DB for OLAP
ms.assetid: 5fad3ecc-407c-4148-862e-ea6119cc7480
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f06af3341034ccc9ddebe1ac6a130be705bdd0cd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="ole-db-for-olap-schema-rowsets"></a>OLAP용 OLE DB 스키마 행 집합
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA(XML for Analysis) 공급자는 다음과 같은 OLAP용 OLE DB 스키마 행 집합을 지원합니다.  
  
> [!NOTE]  
>  에 특정 데이터 원본 공급자가 행 집합을 지원 하는지 여부를 확인 하려면 사용는 **DISCOVER_ENUMERATIONS** 포함 된 행 집합의 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드.  
  
 또한 이러한 행 집합에 대 한 자세한 내용은 "OLAP Schema Rowsets" 항목을 검색 하 여이에서 MSDN 라이브러리에서 찾을 수 있습니다 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkId=15426)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|스키마 행 집합<sup>1</sup>|Description|  
|-------------------------------|-----------------|  
|[DISCOVER_INSTANCES 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/discover-instances-rowset.md)|서버의 인스턴스를 설명합니다.|  
|[DISCOVER_KEYWORDS 행 집합 &#40; OLE DB OLAP &#41;](../../../analysis-services/schema-rowsets/ole-db-olap/discover-keywords-rowset-ole-db-for-olap.md)|공급자에서 예약된 단어 목록을 열거합니다.|  
|[MDSCHEMA_ACTIONS 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-actions-rowset.md)|클라이언트 응용 프로그램에 사용할 수 있는 동작을 설명합니다.|  
|[MDSCHEMA_CUBES 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-cubes-rowset.md)|데이터베이스 내의 큐브 구조를 설명합니다.|  
|[MDSCHEMA_DIMENSIONS 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-dimensions-rowset.md)|데이터베이스 내의 공유 차원과 전용 차원을 설명합니다.|  
|[MDSCHEMA_FUNCTIONS 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-functions-rowset.md)|데이터베이스에 연결된 클라이언트 응용 프로그램에 사용할 수 있는 함수를 설명합니다.|  
|[MDSCHEMA_HIERARCHIES 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset.md)|특정 차원에 포함된 각 계층을 설명합니다.|  
|[MDSCHEMA_INPUT_DATASOURCES 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md)|데이터베이스 내에 정의된 데이터 원본을 설명합니다.|  
|[MDSCHEMA_KPIS 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-kpis-rowset.md)|데이터베이스 내의 KPI(핵심 성과 지표)를 설명합니다.|  
|[MDSCHEMA_LEVELS 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-levels-rowset.md)|특정 계층 내의 각 수준을 설명합니다.|  
|[MDSCHEMA_MEASUREGROUP_DIMENSIONS 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset.md)|측정값 그룹의 차원을 열거합니다.|  
|[MDSCHEMA_MEASUREGROUPS 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroups-rowset.md)|데이터베이스 내의 측정값 그룹을 설명합니다.|  
|[MDSCHEMA_MEASURES 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measures-rowset.md)|큐브 내의 각 측정값을 설명합니다.|  
|[MDSCHEMA_MEMBERS 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-members-rowset.md)|데이터베이스 내의 멤버를 설명합니다.|  
|[MDSCHEMA_PROPERTIES 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-properties-rowset.md)|데이터베이스 내의 멤버 속성을 설명합니다.|  
|[MDSCHEMA_SETS 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-sets-rowset.md)|세션 범위 집합을 비롯하여 데이터베이스에 현재 정의된 집합에 대해 설명합니다.|  
  
 <sup>1</sup> 여기에 나열 된 모든 스키마 행 집합 용 MSOLAP 데이터 원본 공급자에서 지원 되는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA 공급자입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [DISCOVER_ENUMERATORS 행 집합](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)   
 [Analysis Services 스키마 행 집합](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
