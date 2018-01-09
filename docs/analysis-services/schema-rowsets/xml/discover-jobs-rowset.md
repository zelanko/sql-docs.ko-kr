---
title: "DISCOVER_JOBS 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_JOBS rowset
ms.assetid: b4d83bb6-aed3-4513-b516-cefadf95dad2
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0fd27205ff919130eed2e7708031b0268f35408f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="discoverjobs-rowset"></a>DISCOVER_JOBS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]서버에서 실행 하는 활성 작업에 대 한 정보를 제공 합니다. 작업은 명령을 대신하여 특정 태스크를 실행하는 명령의 일부입니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_JOBS** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**JOB_CREATION_TIME**|**DBTYPE_DBTIMESTAMP**||작업이 만들어진 서버 UTC 날짜 및 시간입니다.|  
|**JOB_DESCRIPTION**|**DBTYPE_WSTR**||서버 서비스에서 할당한 작업 설명입니다.|  
|**JOB_EXECUTION_TIME_MS**|**DBTYPE_I8**||작업이 활성 상태인 시간(밀리초)입니다.|  
|**JOB_ID**|**DBTYPE_I4**||작업의 고유 식별자입니다.|  
|**JOB_START_TIME**|**DBTYPE_DBTIMESTAMP**||작업이 시작된 서버 UTC 날짜 및 시간입니다.|  
|**JOB_THREADPOOL_ID**|**DBTYPE_I4**||현재 작업이 시작된 스레드 풀입니다.|  
|**JOB_TOTAL_TIME_MS**|**DBTYPE_I8**||작업이 시작된 이후의 시간(밀리초)입니다.|  
|**SPID**|**DBTYPE_I4**||세션 ID입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DISCOVER_JOBS** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|(선택 사항)|  
|JOB_ID|DBTYPE_I4|(선택 사항)|  
|JOB_DESCRIPTION|DBTYPE_WSTR|(선택 사항)|  
|JOB_THREADPOOL_ID|DBTYPE_I4|(선택 사항)|  
|JOB_MIN TOTAL_TIME_MS|DBTYPE_I8|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
