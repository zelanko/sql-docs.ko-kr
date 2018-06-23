---
title: OLAP 스키마 행 집합 용 OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- schema rowsets [Analysis Services], OLE DB for OLAP
- OLE DB for OLAP schema rowsets
- schema rowsets [OLE DB for OLAP]
- rowsets [Analysis Services], OLE DB for OLAP
ms.assetid: 5fad3ecc-407c-4148-862e-ea6119cc7480
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 898749e17cb5b85e61a2b2c3a94b7247a7ab219b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091633"
---
# <a name="ole-db-for-olap-schema-rowsets"></a>OLAP용 OLE DB 스키마 행 집합
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA(XML for Analysis) 공급자는 다음과 같은 OLAP용 OLE DB 스키마 행 집합을 지원합니다.  
  
> [!NOTE]  
>  에 특정 데이터 원본 공급자가 행 집합을 지원 하는지 여부를 확인 하려면 사용는 `DISCOVER_ENUMERATIONS` 포함 된 행 집합의 [Discover](../../xmla/xml-elements-methods-discover.md) 메서드.  
  
 또한 이러한 행 집합에 대 한 자세한 내용은 "OLAP Schema Rowsets" 항목을 검색 하 여이에서 MSDN 라이브러리에서 찾을 수 있습니다 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkId=15426)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|스키마 행 집합<sup>1</sup>|Description|  
|-------------------------------|-----------------|  
|[DISCOVER_INSTANCES 행 집합](discover-instances-rowset.md)|서버의 인스턴스를 설명합니다.|  
|[DISCOVER_KEYWORDS 행 집합 &#40;OLAP 용 OLE DB&#41;](discover-keywords-rowset-ole-db-for-olap.md)|공급자에서 예약된 단어 목록을 열거합니다.|  
|[MDSCHEMA_ACTIONS 행 집합](mdschema-actions-rowset.md)|클라이언트 응용 프로그램에 사용할 수 있는 동작을 설명합니다.|  
|[MDSCHEMA_CUBES 행 집합](mdschema-cubes-rowset.md)|데이터베이스 내의 큐브 구조를 설명합니다.|  
|[MDSCHEMA_DIMENSIONS 행 집합](mdschema-dimensions-rowset.md)|데이터베이스 내의 공유 차원과 전용 차원을 설명합니다.|  
|[MDSCHEMA_FUNCTIONS 행 집합](mdschema-functions-rowset.md)|데이터베이스에 연결된 클라이언트 응용 프로그램에 사용할 수 있는 함수를 설명합니다.|  
|[MDSCHEMA_HIERARCHIES 행 집합](mdschema-hierarchies-rowset.md)|특정 차원에 포함된 각 계층을 설명합니다.|  
|[MDSCHEMA_INPUT_DATASOURCES 행 집합](mdschema-input-datasources-rowset.md)|데이터베이스 내에 정의된 데이터 원본을 설명합니다.|  
|[MDSCHEMA_KPIS 행 집합](mdschema-kpis-rowset.md)|데이터베이스 내의 KPI(핵심 성과 지표)를 설명합니다.|  
|[MDSCHEMA_LEVELS 행 집합](mdschema-levels-rowset.md)|특정 계층 내의 각 수준을 설명합니다.|  
|[MDSCHEMA_MEASUREGROUP_DIMENSIONS 행 집합](mdschema-measuregroup-dimensions-rowset.md)|측정값 그룹의 차원을 열거합니다.|  
|[MDSCHEMA_MEASUREGROUPS 행 집합](mdschema-measuregroups-rowset.md)|데이터베이스 내의 측정값 그룹을 설명합니다.|  
|[MDSCHEMA_MEASURES 행 집합](mdschema-measures-rowset.md)|큐브 내의 각 측정값을 설명합니다.|  
|[MDSCHEMA_MEMBERS 행 집합](mdschema-members-rowset.md)|데이터베이스 내의 멤버를 설명합니다.|  
|[MDSCHEMA_PROPERTIES 행 집합](mdschema-properties-rowset.md)|데이터베이스 내의 멤버 속성을 설명합니다.|  
|[MDSCHEMA_SETS 행 집합](mdschema-sets-rowset.md)|세션 범위 집합을 비롯하여 데이터베이스에 현재 정의된 집합에 대해 설명합니다.|  
  
 <sup>1</sup> 여기에 나열 된 모든 스키마 행 집합 용 MSOLAP 데이터 원본 공급자에서 지원 되는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA 공급자입니다.  
  
## <a name="see-also"></a>관련 항목  
 [DISCOVER_ENUMERATORS 행 집합](../xml/discover-enumerators-rowset.md)   
 [Analysis Services 스키마 행 집합](../../schema-rowsets/analysis-services-schema-rowsets.md)  
  
  