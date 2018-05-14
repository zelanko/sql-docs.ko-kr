---
title: DISCOVER_STORAGE_TABLE_COLUMNS 행 집합 | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dbbed22cc248f78409c2a1369bc082727be97bef
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="discoverstoragetablecolumns-rowset"></a>DISCOVER_STORAGE_TABLE_COLUMNS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  SharePoint 또는 테이블 형식 모드로 실행되는 Analysis Services 데이터베이스에서 사용하는 저장소 테이블에 대한 열 수준 정보를 제공합니다.  
  
 **다음에 적용:** 테이블 형식 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_STORAGE_TABLE_COLUMNS** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|**열 이름**|**유형 표시기**|**제한**|**설명**|  
|---------------------|------------------------|---------------------|---------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|예|테이블이 포함된 데이터베이스 이름을 지정합니다. 생략하는 경우 현재 데이터베이스가 사용됩니다.<br /><br /> **DISCOVER_STORAGE_TABLE_COLUMNS** 이 열을 사용 하 여 행 집합을 제한할 수 있습니다.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|예|테이블이 포함된 큐브 또는 모델을 지정합니다.<br /><br /> 이 열을 사용하여 **DISCOVER_STORAGE_TABLES** 행 집합을 제한할 수 있습니다.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|예|측정값 그룹의 이름입니다.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||차원의 이름입니다.|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**||특성의 이름입니다.|  
|**TABLE_ID**|**DBTYPE_WSTR**||테이블 ID입니다.|  
|**COLUMN_ID**|**DBTYPE_ WSTR**||열의 ID입니다. 열 ID는 xVelocity 메모리 내 분석 엔진(VertiPaq) 내부용이며 정보 제공을 위해서만 사용됩니다.|  
|**COLUMN_TYPE**|**DBTYPE_WSTR**||열의 유형입니다. 열 유형은 xVelocity 메모리 내 분석 엔진(VertiPaq) 내부용이며 정보 제공을 위해서만 사용됩니다.<br /><br /> BASIC_DATA와 함께 사용됨<br /><br /> HIERARCHY_DATAID_TO_POSITION<br /><br /> HIERARCHY_POSITION_TO_DATAID<br /><br /> RELATIONSHIP|  
|**COLUMN_ENCODING**|**DBTYPE_UI8**||열 데이터에 사용된 인코딩 유형을 나타내는 정수입니다.<br /><br /> **0**와 함께 사용 **COLUMN_TYPE**: HIERARCHY_DATAID_TO_POSITION, HIERARCHY_POSITION_TO_DATAID, 관계<br /><br /> **1**와 함께 사용 **COLUMN_TYPE**: BASIC_DATA<br /><br /> **2**와 함께 사용 **COLUMN_TYPE**: BASIC_DATA|  
|**데이터 형식**|**DBTYPE_WSTR**||열의 데이터 형식입니다. 가능한 값은 다음과 같습니다.<br /><br /> DBTYPE_BOOL<br /><br /> DBTYPE_CY<br /><br /> DBTYPE_DATE<br /><br /> DBTYPE_I4<br /><br /> DBTYPE_I8<br /><br /> DBTYPE_R8<br /><br /> DBTYPE_WSTR<br /><br /> 해당 사항 없음|  
|**ISKEY**|**DBTYPE_BOOL**||**True 이면** 열이 고, 그렇지 않으면 기본 또는 외래 키로 사용 되는 경우 **false**합니다.|  
|**ISUNIQUE**|**DBTYPE_BOOL**||**True 이면** 열에 값이 고, 그렇지 않으면 고유 **false**합니다.|  
|**ISNULLABLE**|**DBTYPE_BOOL**||**True 이면** 열이 고, 그렇지 않으면 null을 허용 하는 경우 **false**합니다.|  
|**ISROWNUMBER**|**DBTYPE_BOOL**||**True 이면** 열이 행 번호 열입니다. 행 번호 열은 xVelocity 메모리 내 분석 엔진에서 내부적으로 사용됩니다.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|a07ccd44-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|StorageTableColumns|  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 DMV 쿼리를 사용하여 결과 집합을 반환합니다.  
  
```  
SELECT *  
FROM $System.DISCOVER_STORAGE_TABLE_COLUMNS  
ORDER BY TABLE_ID DESC  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 스키마 행 집합](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
