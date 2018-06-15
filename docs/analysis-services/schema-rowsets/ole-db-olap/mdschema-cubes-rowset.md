---
title: MDSCHEMA_CUBES 행 집합 | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: da0fc34fedcd6980f8dd19e199314fc1295c78bb
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34037074"
---
# <a name="mdschemacubes-rowset"></a>MDSCHEMA_CUBES 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  데이터베이스 내의 큐브 구조를 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **MDSCHEMA_CUBES** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|데이터베이스의 이름입니다.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|지원되지 않습니다.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|큐브 또는 차원의 이름입니다. 차원 이름 앞에는 달러 기호($)가 붙습니다.<br /><br /> 참고: 서버 및 데이터베이스 관리자만 차원에서 만든 큐브를 볼 권한이 있어야 합니다.|  
|**CUBE_TYPE**|**DBTYPE_WSTR**|큐브의 유형입니다. 유효한 값은 다음과 같습니다.<br /><br /> **큐브**<br /><br /> **차원**|  
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
  
  
