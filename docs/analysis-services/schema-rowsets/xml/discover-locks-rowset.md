---
title: "DISCOVER_LOCKS 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_LOCKS rowset
ms.assetid: dea48167-212c-40b7-a416-434042a1b697
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: df185344ea5af92a66c019c29b7a385ff309522b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="discoverlocks-rowset"></a>DISCOVER_LOCKS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]서버에서 현재 고정 된 잠금에 대 한 정보를 제공 합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_LOCKS** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**LOCK_CREATION_TIME**|**DBTYPE_DBTIMESTAMP**||잠금이 요청된 시점의 UTC 서버 시간입니다.|  
|**LOCK_GRANT_TIME**|**DBTYPE_DBTIMESTAMP**||리소스에서 잠금이 허용된 시점의 UTC 서버 시간입니다.|  
|**LOCK_ID**|**DBTYPE_GUID**||GUID와 같은 잠금의 고유 식별자입니다.|  
|**LOCK_OBJECT_ID**|**DBTYPE_WSTR**||잠금이 수행되는 개체의 고유 식별자입니다.|  
|**LOCK_STATUS**|**DBTYPE_I4**||잠금 상태입니다.<br /><br /> 0은 "개체를 잠그려고 대기 중"을 의미합니다.<br /><br /> 1은 "잠금 허용"을 의미합니다.|  
|**LOCK_TRANSACTION_ID**|**DBTYPE_GUID**||GUID와 같은 트랜잭션의 고유 식별자입니다.|  
|**LOCK_TYPE**|**DBTYPE_I4**||잠금 유형의 비트 마스크입니다. 자세한 내용은 이 항목의 주의 섹션을 참조하십시오.|  
|**SPID**|**DBTYPE_I4**||세션 ID입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DISCOVER_LOCKS** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|(선택 사항)|  
|LOCK_TRANSACTION_ID|DBTYPE_GUID|(선택 사항)|  
|LOCK_OBJECT_ID|DBTYPE_WSTR|(선택 사항)|  
|LOCK_STATUS|DBTYPE_I4|(선택 사항)|  
|LOCK_TYPE|DBTYPE_I4|(선택 사항)|  
|LOCK_MIN_TOTAL_MS|DBTYPE_I8|(선택 사항)|  
  
## <a name="remarks"></a>주의  
  
## <a name="lock-types"></a>잠금 유형  
  
|잠금 이름|값|설명|  
|---------------|-----------|-----------------|  
|LOCK_NONE|0x0000000|잠금이 없습니다.|  
|LOCK_SESSION_LOCK|0x0000001|비활성 세션입니다. 다른 잠금을 방해하지 않습니다.|  
|LOCK_READ|0x0000002|처리 중의 읽기 잠금입니다.|  
|LOCK_WRITE|0x0000004|처리 중의 쓰기 잠금입니다.|  
|LOCK_COMMIT_READ|0x0000008|공유 커밋 잠금입니다.|  
|LOCK_COMMIT_WRITE|0x0000010|배타적 커밋 잠금입니다.|  
|LOCK_COMMIT_ABORTABLE|0x0000020|커밋 진행 중에 중단합니다.|  
|LOCK_COMMIT_INPROGRESS|0x0000040|진행 중인 커밋입니다.|  
|LOCK_INVALID|0x0000080|잘못된 잠금입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
