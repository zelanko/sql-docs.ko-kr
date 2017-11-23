---
title: "DMSCHEMA_MINING_STRUCTURES 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DMSCHEMA_MINING_STRUCTURES
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DMSCHEMA_MINING_STRUCTURES rowset
ms.assetid: 6224556b-08a0-496e-bd7c-632c3e833e26
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: beaf272e97b8e7f49539311f5f635dd544b88347
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="dmschemaminingstructures-rowset"></a>DMSCHEMA_MINING_STRUCTURES 행 집합
  현재 카탈로그의 마이닝 구조에 대한 정보를 열거합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DMSCHEMA_MINING_STRUCTURES** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**||카탈로그 이름입니다.|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**||정규화되지 않은 스키마 이름입니다. 공급자가 스키마를 지원하지 않는 경우**NULL** 입니다.|  
|**STRUCTURE_NAME**|**DBTYPE_WSTR**||구조 이름입니다. 이 열에는 **NULL**이 포함될 수 없습니다.|  
|**STRUCTURE_GUID**|**DBTYPE_GUID**||구조를 고유하게 식별하는 GUID입니다. 공급자가 지원하지 않는 경우**NULL** 입니다.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||구조에 대한 간단한 설명입니다. 구조와 연결된 설명이 없으면**NULL** 입니다.|  
|**STRUCTURE_PROPID**|**DBTYPE_UI4**||구조의 속성 ID입니다. 공급자가 지원하지 않는 경우**NULL** 입니다.|  
|**DATE_CREATED**|**DBTYPE_DBTIMESTAMP**||구조를 만든 날짜입니다. 공급자가 제공하지 않는 경우**NULL** 입니다.|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||구조를 마지막으로 수정한 날짜입니다. 공급자가 제공하지 않는 경우**NULL** 입니다.|  
|**CREATION_STATEMENT**|**DBTYPE_WSTR**||(선택 사항) 원본 데이터 마이닝 모델을 만드는 데 사용된 문입니다.|  
|**IS_POPULATED**|**DBTYPE_BOOL**||구조가 채워졌는지 여부를 나타내는 부울입니다.<br /><br /> 구조가 채워져 있으면**VARIANT_TRUE** 이고, 그렇지 않으면 **VARIANT_FALSE** 입니다.|  
|**LAST_PROCESSED**|**DBTYPE_DBTIMESTAMP**||구조가 마지막으로 처리된 날짜입니다. 공급자가 제공하지 않는 경우**NULL** 입니다.|  
|**HOLDOUT_MAXPERCENT**|**DBTYPE_ U I 1**||테스트 집합으로 홀드아웃한 입력 사례의 최대 비율을 나타내는 사용자 지정 값입니다.<br /><br /> 0 또는 **NULL** 은 제한이 없음을 나타냅니다.|  
|**HOLDOUT_MAXCASES**|**DBTYPE_UI8**||테스트 집합으로 홀드아웃한 입력 사례의 최대 수를 나타내는 사용자 지정 값입니다.<br /><br /> 0 또는 **NULL** 은 제한이 없음을 나타냅니다.|  
|**HOLDOUT_SEED**|**DBTYPE_UI8**||반복 가능한 분할의 초기값으로 사용되는 사용자 지정 값입니다.<br /><br /> 0은 마이닝 구조 ID의 해시가 초기값으로 사용됨을 나타냅니다.|  
|**HOLDOUT_ACTUAL_SIZE**|**DBTYPE_UI8**||마이닝 구조가 처리되면 이 열은 테스트 데이터 집합의 실제 크기(사례 수로 표시됨)를 나타냅니다.<br /><br /> **NULL** 은 마이닝 구조가 처리되지 않았음을 나타냅니다.|  
  
 행 집합은 **STRUCTURE_CATALOG**, **STRUCTURE_SCHEMA**, **STRUCTURE_NAME**을 기준으로 정렬됩니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DMSCHEMA_MINING_STRUCTURES** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**|(선택 사항)|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**|(선택 사항)|  
|**STRUCTURE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 스키마 행 집합](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
