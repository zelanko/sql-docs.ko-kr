---
title: "DISCOVER_DB_CONNECTIONS 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_DB_CONNECTIONS rowset
ms.assetid: 12a51a4e-5f3d-4449-9d94-7836fea1bc8b
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f6c6fbeac76e14dd410ed8dafcb739e5797cc270
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="discoverdbconnections-rowset"></a>DISCOVER_DB_CONNECTIONS 행 집합
  서버에서 현재 열린 데이터베이스 연결에 대한 리소스 사용량 및 작업 정보를 제공합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_DB_CONNECTIONS** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CONNECTION_CATALOG_NAME**|**DBTYPE_WSTR**||현재 연결된 데이터베이스의 이름입니다.|  
|**CONNECTION_ID**|**DBTYPE_I4**||연결을 식별하는 고유 번호입니다.|  
|**CONNECTION_IDLE_TIME_MS**|**DBTYPE_I8**||연결이 시작된 이후의 유휴 시간(밀리초)입니다.|  
|**CONNECTION_IN_USE**|**DBTYPE_I4**||연결이 활성 상태(1)인지 유휴 상태(0)인지를 나타냅니다.|  
|**CONNECTION_LAST_COMMAND_END_TIME**|**DBTYPE_DBTIMESTAMP**||마지막 명령의 실행을 마친 서버 UTC 날짜 및 시간입니다.|  
|**CONNECTION_LAST_COMMAND_START_TIME**|**DBTYPE_DBTIMESTAMP**||마지막 명령의 실행을 시작한 서버 UTC 날짜 및 시간입니다.|  
|**CONNECTION_SERVER_NAME**|**DBTYPE_WSTR**||현재 연결된 서버의 이름입니다.|  
|**CONNECTION_SPID**|**DBTYPE_I4**||세션 ID입니다.|  
|**CONNECTION_START_TIME**|**DBTYPE_DBTIMESTAMP**||연결이 시작된 서버 UTC 날짜 및 시간입니다.|  
|**CONNECTION_USAGE_TIME_MS**|**DBTYPE_I8**||연결이 시작된 이후의 연결 활성 시간(밀리초)입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
> [!IMPORTANT]  
>  **DISCOVER_DB_CONNECTIONS** 행 집합은 서비스가 관계형 데이터 원본에 연결되어 있는 경우에만 정보를 표시합니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DISCOVER_DB_CONNECTIONS** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|CONNECTION_ID|DBTYPE_I4|(선택 사항)|  
|CONNECTION_IN_USE|DBTYPE_I4|(선택 사항)|  
|CONNECTION_SERVER_NAME|DBTYPE_WSTR|(선택 사항)|  
|CONNECTION_CATALOG_NAME|DBTYPE_WSTR|필수 사항입니다.|  
|CONNECTION_SPID|DBTYPE_I4|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
