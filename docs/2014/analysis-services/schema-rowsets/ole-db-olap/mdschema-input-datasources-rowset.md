---
title: MDSCHEMA_INPUT_DATASOURCES 행 집합 | Microsoft Docs
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
api_name:
- MDSCHEMA_INPUT_DATASOURCES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_INPUT_DATASOURCES rowset
ms.assetid: 12482fd5-16e3-4171-9cb0-76d0d4f5308e
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aedd2980b6c51872a9d78d6d1c2cbbecc84d7ec4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249113"
---
# <a name="mdschemainputdatasources-rowset"></a>MDSCHEMA_INPUT_DATASOURCES 행 집합
  데이터베이스 내에 정의된 데이터 원본을 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `MDSCHEMA_INPUT_DATASOURCES` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||이 데이터 원본이 속한 카탈로그의 이름입니다.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`DATASOURCE_NAME`|`DBTYPE_WSTR`||데이터 원본 개체의 이름입니다.|  
|`DATASOURCE_TYPE`|`DBTYPE_WSTR`||데이터 원본의 유형입니다. 유효한 값은 다음과 같습니다.<br /><br /> -   `Relational`<br />-   `Olap`|  
|`CREATED_ON`|`DBTYPE_DBTIMESTAMP`||데이터 원본이 만들어진 날짜입니다.|  
|`LAST_SCHEMA_UPDATE`|`DBTYPE_DBTIMESTAMP`||데이터 원본을 마지막으로 수정한 날짜와 시간입니다.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||동작에 대한 알기 쉬운 설명입니다.|  
|`TIMEOUT`|`DBTYPE_UI4`||데이터 원본의 제한 시간입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 `MDSCHEMA_INPUT_DATASOURCES` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`DATASOURCE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`DATASOURCE_TYPE`|`DBTYPE_WSTR`|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목  
 [OLAP용 OLE DB 스키마 행 집합](ole-db-for-olap-schema-rowsets.md)  
  
  
