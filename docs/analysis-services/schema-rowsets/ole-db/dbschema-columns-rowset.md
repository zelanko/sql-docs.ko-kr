---
title: DBSCHEMA_COLUMNS 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DBSCHEMA_COLUMNS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DBSCHEMA_COLUMNS rowset
ms.assetid: 653bdd07-a533-4a99-8b6a-6e5c7322e1f3
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 32df882f6f6b34c4cd5049713240460c62324ddb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="dbschemacolumns-rowset"></a>DBSCHEMA_COLUMNS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]제공 된 제한 조건을 충족 하는 모든 열에 대 한 열 정보를 제공 합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DBSCHEMA_COLUMNS** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**TABLE_CATALOG**|**DBTYPE_WSTR**||데이터베이스의 이름입니다.|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**||지원되지 않습니다.|  
|**TABLE_NAME**|**DBTYPE_WSTR**||큐브의 이름입니다.|  
|**COLUMN_NAME**|**DBTYPE_WSTR**||특성 계층 또는 측정값의 이름입니다.|  
|**COLUMN_GUID**|**DBTYPE_GUID**||지원되지 않습니다.|  
|**COLUMN_PROPID**|**DBTYPE_UI4**||지원되지 않습니다.|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**||1부터 시작하는 열 위치입니다.|  
|**COLUMN_HAS_DEFAULT**|**DBTYPE_BOOL**||지원되지 않습니다.|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**||지원되지 않습니다.|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**||A **DBCOLUMNFLAGS** 열 속성을 나타내는 비트 마스크입니다. 'DBCOLUMNFLAGS 열거 형식' 참조 [icolumnsinfo:: Getcolumninfo](http://msdn2.microsoft.com/library/ms722704.aspx)|  
|**IS_NULLABLE**|**DBTYPE_BOOL**||항상 반환 **false**합니다.|  
|**DATA_TYPE**|**DBTYPE_WSTR**<br /><br /> **DBTYPE_VARIANT**||열의 데이터 형식입니다. 차원 열의 경우 문자열을 반환하고 측정값의 경우 변형을 반환합니다.|  
|**TYPE_GUID**|**DBTYPE_GUID**||지원되지 않습니다.|  
|**때**|**DBTYPE_UI4**||열 값의 최대 길이입니다.<br /><br /> 이 검색 되는 **DataSize** 속성에는 **DataItem**합니다.|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||문자 또는 이진 열의 경우 열 값의 최대 길이(바이트)입니다.<br /><br /> 0 값은 열에 최대 길이가 없음을 나타냅니다.<br /><br /> **NULL** 이진 또는 문자 데이터 형식을 반환 하지 않는 열에 대 한 반환 됩니다.|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||최대 전체 자릿수 숫자 데이터에 대 한 열이 아닌 형식 **DBTYPE_VARNUMERIC**합니다.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||에 대 한 소수점 오른쪽 자릿수 **DBTYPE_DECIMAL**, **DBTYPE_NUMERIC**, **DBTYPE_VARNUMERIC**합니다. 그렇지 않으면 이것이 **NULL**합니다.|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**||지원되지 않습니다.|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**||지원되지 않습니다.|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**||지원되지 않습니다.|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**||지원되지 않습니다.|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**||지원되지 않습니다.|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**||지원되지 않습니다.|  
|**데이터 정렬 이름**|**DBTYPE_WSTR**||지원되지 않습니다.|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**||지원되지 않습니다.|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**||지원되지 않습니다.|  
|**DOMAIN_NAME**|**DBTYPE_WSTR**||지원되지 않습니다.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||지원되지 않습니다.|  
|**COLUMN_OLAP_TYPE**|**DBTYPE_WSTR**||개체의 OLAP 유형입니다.<br /><br /> **측정값** 는 개체가 측정값 임을 나타냅니다.<br /><br /> **특성** 은 개체가 차원 특성 임을 나타냅니다.<br /><br /> **스키마** 는 개체가 스키마의 열 임을 나타냅니다.|  
  
 에 행 집합은 정렬 **TABLE_CATALOG**, **TABLE_SCHEMA**, **TABLE_NAME**합니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DBSCHEMA_COLUMNS** 행 집합은 다음 표에 나열 된 열에 제한 될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**TABLE_CATALOG**|**DBTYPE_WSTR**|선택 사항|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**|선택 사항|  
|**TABLE_NAME**|**DBTYPE_WSTR**|선택 사항|  
|**COLUMN_NAME**|**DBTYPE_WSTR**|선택 사항|  
|**COLUMN_OLAP_TYPE**|**DBTYPE_WSTR**|선택 사항|  
  
## <a name="see-also"></a>관련 항목:  
 [OLE DB 스키마 행 집합](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
