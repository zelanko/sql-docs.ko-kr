---
title: "MDSCHEMA_CUBES 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDSCHEMA_CUBES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_CUBES rowset
ms.assetid: 5f1b63d4-aa3f-48c6-b866-7ffd91675044
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a3fa75f9ea6bcab54d123d6e914d5d77077b44e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemacubes-rowset"></a>MDSCHEMA_CUBES 행 집합
  데이터베이스 내의 큐브 구조를 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **MDSCHEMA_CUBES** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|데이터베이스의 이름입니다.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|지원되지 않습니다.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|큐브 또는 차원의 이름입니다. 차원 이름 앞에는 달러 기호($)가 붙습니다.<br /><br /> 참고: 서버 및 데이터베이스 관리자만 차원에서 만든 큐브를 볼 권한이 있어야 합니다.|  
|**CUBE_TYPE**|**DBTYPE_WSTR**|큐브의 유형입니다. 유효한 값은<br /><br /> **큐브**<br /><br /> **차원**|  
|**CUBE_GUID**|**DBTYPE_GUID**|지원되지 않습니다.|  
|**CREATED_ON**|**DBTYPE_DBTIMESTAMP**|지원되지 않습니다.|  
|**LAST_SCHEMA_UPDATE**|**DBTYPE_DBTIMESTAMP**|큐브가 마지막으로 처리된 시간입니다.|  
|**SCHEMA_UPDATED_BY**|**DBTYPE_WSTR**|지원되지 않습니다.|  
|**LAST_DATA_UPDATE**|**DBTYPE_DBTIMESTAMP**|큐브가 마지막으로 처리된 시간입니다.|  
|**DATA_UPDATED_BY**|**DBTYPE_WSTR**|지원되지 않습니다.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|큐브에 대한 알기 쉬운 설명입니다.|  
|**IS_DRILLTHROUGH_ENABLED**|**DBTYPE_BOOL**|항상 true를 반환하는 부울입니다.|  
|**IS_LINKABLE**|**DBTYPE_BOOL**|큐브를 연결된 큐브에 사용할 수 있는지 여부를 나타내는 부울입니다.|  
|**IS_WRITE_ENABLED**|**DBTYPE_BOOL**|큐브가 쓰기 가능한지 여부를 나타내는 부울입니다.|  
|**IS_SQL_ENABLED**|**DBTYPE_BOOL**|큐브에 SQL을 사용할 수 있는지 여부를 나타내는 부울입니다.|  
|**CUBE_CAPTION**|**DBTYPE_WSTR**|큐브의 캡션입니다.|  
|**BASE_CUBE_NAME**|**DBTYPE_WSTR**|이 큐브가 큐브 뷰인 경우 원본 큐브의 이름입니다.|  
|**주석**|**DBTYPE_WSTR**|(선택 사항) XML 형식의 메모 집합입니다.|  
  
 행 집합은 **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**을 기준으로 정렬됩니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **MDSCHEMA_CUBES** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(선택 사항) 기본 제한 값 1은 합니다. 이 유효한 값 중 하나를 사용 하 여 비트맵:<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**기본 Cube_Name**|**DBTYPE_WSTR**|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목:  
 [OLAP 스키마 행 집합 용 OLE DB](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

