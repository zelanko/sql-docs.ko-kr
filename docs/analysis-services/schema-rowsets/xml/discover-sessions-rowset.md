---
title: "DISCOVER_SESSIONS 행 집합 | Microsoft Docs"
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
helpviewer_keywords: DISCOVER_SESSIONS rowset
ms.assetid: 47a79542-3142-4e62-a66f-6c4dbfe0f5c0
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5f8fef815cbb4a648bacb6ab90a40bfc41d57d3e
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="discoversessions-rowset"></a>DISCOVER_SESSIONS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]서버에서 현재 열려 있는 세션에 대 한 리소스 사용량 및 작업 정보를 제공 합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_SESSIONS** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**SESSION_COMMAND_COUNT**|**DBTYPE_I4**||세션이 시작된 이후에 실행되기 시작한 명령 수입니다.|  
|**SESSION_CONNECTION_ID**|**DBTYPE_I4**||세션에 대한 연결 식별자입니다.|  
|**SESSION_CPU_TIME_MS의 경우**|**DBTYPE_UI8**||세션이 시작된 이후에 모든 요청에 사용된 CPU 시간(밀리초)입니다.|  
|**SESSION_CURRENT_DATABASE**|**DBTYPE_WSTR**||현재 실행 중인 명령에서 사용하고 있는 데이터베이스 또는 마지막으로 실행된 명령에서 사용하고 있는 데이터베이스의 이름입니다.|  
|**SESSION_ELAPSED_TIME_MS**|**DBTYPE_UI8**||세션이 시작된 이후에 경과된 시간(밀리초)입니다.|  
|**SESSION_ID**|**DBTYPE_WSTR**||GUID와 같은 세션 고유 식별자입니다.|  
|**SESSION_IDLE_TIME_MS**|**DBTYPE_UI8**||세션이 시작된 이후의 유휴 시간(밀리초)입니다.|  
|**SESSION_LAST_COMMAND**|**DBTYPE_WSTR**||현재 실행 중인 명령 또는 마지막으로 실행된 명령의 텍스트입니다.|  
|**SESSION_LAST_COMMAND_CPU_TIME_MS**|**DBTYPE_UI8**||**SESSION_LAST_COMMAND**에 사용된 CPU 시간(밀리초)입니다.|  
|**SESSION_LAST_COMMAND_ELAPSED_TIME_MS**|**DBTYPE_UI8**||**SESSION_LAST_COMMAND**가 시작된 이후에 경과된 시간(밀리초)입니다.|  
|**SESSION_LAST_COMMAND_END_TIME**|**DBTYPE_DBTIMESTAMP**||마지막 명령의 실행을 마친 시점의 UTC 서버 시간입니다.|  
|**SESSION_LAST_COMMAND_START_TIME**|**DBTYPE_DBTIMESTAMP**||마지막 명령의 실행이 시작된 시점의 UTC 서버 시간입니다.|  
|**SESSION_PROPERTIES**|**DBTYPE_WSTR**||나중에 사용하도록 예약되어 있습니다.|  
|**SESSION_READ_KB**|**DBTYPE_UI8**||세션이 시작된 이후부터 디스크에서 읽은 누적 데이터 값(KB)입니다.|  
|**SESSION_READS**|**DBTYPE_UI8**||세션이 시작된 이후부터 누적된 디스크 읽기 수입니다.|  
|**SESSION_SPID**|**DBTYPE_I4**||세션 ID입니다.|  
|**SESSION_START_TIME**|**DBTYPE_DBTIMESTAMP**||서버 UTC 시간과 같이 세션이 시작된 날짜 및 시간입니다.|  
|**SESSION_STATUS**|**DBTYPE_I4**||세션의 작업 상태입니다.<br /><br /> 0 = "유휴": 현재 진행 중인 작업이 없습니다.<br /><br /> 1 = "활성": 세션에서 요청된 태스크를 실행하고 있습니다.<br /><br /> 2 = "차단": 세션에서 일부 리소스가 일시 중지된 태스크를 계속해서 실행할 때까지 기다리고 있습니다.<br /><br /> 3 = "취소됨": 세션이 취소됨으로 태그가 지정되었습니다.|  
|**SESSION_USED_MEMORY**|**DBTYPE_I4**||세션에서 사용하는 현재 메모리 크기(KB)입니다. 보고되는 값은 축소 가능 및 축소 불가능 메모리 사이에 구분이 없는 SPID별 RAM 사용입니다. 메모리 사용에 대해 보고하는 다른 DMVS와 달리 DISCOVER_SESSIONS에서는 메모리 사용을 범주별로 나누지 않습니다.<br /><br /> 여러 세션에서 공유되는 개체를 제외하기 때문에 SESSION_USED_MEMORY는 실제 메모리 사용을 적게 보고하는 경향이 있습니다.  세션에 고유한 개체만 메모리 계산에 표시됩니다.|  
|**SESSION_USER_NAME**|**DBTYPE_WSTR**||세션 사용자 이름입니다.|  
|**SESSION_WRITE_KB**|**DBTYPE_UI8**||세션이 시작된 이후부터 디스크에 기록된 누적 데이터 값(KB)입니다.|  
|**SESSION_WRITES**|**DBTYPE_UI8**||세션이 시작된 이후부터 누적된 디스크 쓰기 수입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DISCOVER_SESSIONS** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|SESSION_ID|DBTYPE_WSTR|(선택 사항)|  
|SESSION_SPID|DBTYPE_I4|(선택 사항)|  
|SESSION_CONNECTION_ID|DBTYPE_I4|(선택 사항)|  
|SESSION_USER_NAME|DBTYPE_WSTR|(선택 사항)|  
|SESSION_CURRENT_DATABASE|DBTYPE_WSTR|(선택 사항)|  
|SESSION_ELAPSED_TIME_MS|DBTYPE_UI8|(선택 사항)|  
|SESSION_CPU_TIME_MS|DBTYPE_UI8|(선택 사항)|  
|SESSION_IDLE_TIME_MS|DBTYPE_UI8|(선택 사항)|  
|SESSION_STATUS|DBTYPE_I4|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
