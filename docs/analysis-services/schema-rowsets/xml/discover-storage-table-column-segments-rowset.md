---
title: "DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 3e514715-9fe6-4e6a-accb-4149ffd7e0bf
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8fd3bd96766ad26c21813f137f8f12452932dea7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="discoverstoragetablecolumnsegments-rowset"></a>DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS 행 집합
  테이블 형식에서 실행 되는 Analysis Services 데이터베이스에서 사용 되는 저장소 테이블에 대 한 열 및 세그먼트 수준 정보를 제공 하거나 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 모드입니다. 이 행 집합은 주로 문제 해결 및 분석을 위해 사용됩니다.  
  
 **다음에 적용:** 테이블 형식 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|**열 이름**|**유형 표시기**|**제한**|**Description**|  
|---------------------|------------------------|---------------------|---------------------|  
|**A S E _**|**DBTYPE_WSTR**|예|테이블 형식 데이터베이스를 지정합니다.<br /><br /> **DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS** 이 열을 사용 하 여 행 집합을 제한할 수 있습니다. 생략하는 경우 현재 데이터베이스가 사용됩니다.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|예|모델의 이름입니다.<br /><br /> 이 열을 사용하여 **DISCOVER_STORAGE_TABLES** 행 집합을 제한할 수 있습니다.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|예|측정값 그룹의 이름입니다.|  
|**PARTITION_NAME**|**DBTYPE_WSTR**|예|파티션의 이름입니다.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||차원의 이름입니다.|  
|**TABLE_ID**|**DBTYPE_WSTR**||테이블 세그먼트의 내부 ID입니다.|  
|**COLUMN_ID**|**DBTYPE_WSTR**||열의 내부 ID입니다.|  
|**세그먼트 수 (_N)**|**DBTYPE_I8**||테이블 세그먼트의 서수입니다.|  
|**TABLE_PARTTION_NUMBER**|**DBTYPE_I8**||파티션의 서수입니다.|  
|**RECORDS_COUNT**|**DBTYPE_I8**||파티션에 있는 레코드 수입니다.|  
|**ALLOCATED_SIZE**|**DBTYPE_UI8**||열 세그먼트에 할당된 크기(바이트)입니다.|  
|**USED_SIZE**|**DBTYPE_UI8**||열 세그먼트에서 사용하는 크기(바이트)입니다.|  
|**COMPRESSION_TYPE**|**DBTYPE_WSTR**||열 세그먼트에 적용된 압축 유형입니다. 이 값은 내부 전용 및 고객 지원 전용으로 사용되는 값입니다. Microsoft는 이 열에 대한 유효한 값 또는 설명을 게시하지 않습니다.|  
|**BITS_COUNT**|**DBTYPE_I8**||비트 수입니다.|  
|**BOOKMARK_BITS_COUNT**|**DBTYPE_I8**||책갈피 비트 수입니다.|  
|**VERTIPAQ_STATE**|**DBTYPE_WSTR**||이 열 세그먼트에 대한 VertiPaq 압축 상태입니다. 값은 다음 중 하나입니다.<br /><br /> SKIPPED – VertiPaq 압축을 건너뛰었습니다.<br /><br /> COMPLETED – VertiPaq 압축이 성공적으로 완료되었습니다.<br /><br /> TIMEBOXED - VertiPaq 압축이 시간 내에 완료되었습니다.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|a07ccd45-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|StorageSegments|  
  
## <a name="example"></a>예제  
 다음 쿼리는 현재 데이터베이스에서 모델 특성 LastName과 연결된 저장소 테이블 세그먼트를 반환합니다.  
  
```  
SELECT DISTINCT TABLE_ID, COLUMN_ID   
FROM $system.DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS  
WHERE COLUMN_ID = 'LastName'  
ORDER BY TABLE_ID  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 스키마 행 집합](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  

