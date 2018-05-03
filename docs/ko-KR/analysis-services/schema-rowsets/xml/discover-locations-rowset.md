---
title: DISCOVER_LOCATIONS 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 6d3a1171-8e4d-4022-ade0-b785cf795d70
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b58cba508faeb566f1ddb5f19bf24ef19d1e8d95
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="discoverlocations-rowset"></a>DISCOVER_LOCATIONS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  백업 파일의 콘텐츠에 대한 정보를 반환합니다. 백업 파일 위치에 액세스할 수 있는 권한이 있어야 합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_LOCATIONS** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|제한|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**LOCATION_BACKUP_FILE_PATHNAME**|**DBTYPE_WSTR**|필수 열입니다. 아래를 참조하십시오.|백업 파일의 위치입니다.|  
|**LOCATION_PARTITION_OBJECTPATH**|**DBTYPE_WSTR**||데이터 폴더에 상대적인 파티션의 경로입니다.|  
|**LOCATION_PARTITION_DATASOURCEID**|**DBTYPE_WSTR**||파티션을 처리하는 데 사용되는 데이터 원본 ID입니다.|  
|**LOCATION_PARTITION_DATASOURCENAME**|**DBTYPE_WSTR**||처리하는 데 사용되는 데이터 원본의 이름입니다.|  
|**LOCATION_PARTITION_NAME**|**DBTYPE_WSTR**||파티션 이름입니다.|  
|**LOCATION_PARTITION_SIZE**|**DBTYPE_WSTR**||파티션의 대략적인 크기입니다.|  
|**LOCATION_CONNECTION_STRING**|**DBTYPE_WSTR**||처리하는 데 사용되는 데이터 원본의 연결 문자열입니다.|  
|**LOCATION_PARTITION_FOLDER**|**DBTYPE_WSTR**||백업 파일이 생성된 때 이 파티션의 원래 위치입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DISCOVER_LOCATIONS** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**LOCATION_BACKUP_FILE_PATHNAME**|**DBTYPE_WSTR**|필수임|  
|**LOCATION_PASSWORD PF_DBTYPE**|**DBTYPE_WSTR**|백업하는 동안 지정된 경우 필수 이 제한은 반환되는 행을 제한하는 데는 사용되지 않습니다. 해당 위치에 액세스하기 위한 암호를 제공하는 데 사용됩니다.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|a07ccd92-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|위치|  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
