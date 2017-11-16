---
title: "DISCOVER_CONNECTIONS 행 집합 | Microsoft Docs"
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
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_CONNECTIONS rowset
ms.assetid: e4703970-c31d-448c-ab68-503303c91aa4
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3b02c9f5d9a9e22e626143a6ca5701ac5b1db50e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="discoverconnections-rowset"></a>DISCOVER_CONNECTIONS 행 집합
  서버에서 현재 열린 연결에 대한 리소스 사용량 및 작업 정보를 제공합니다.  
  
 **적용 대상:** 테이블 형식 모델, 다차원 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_CONNECTIONS** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|제한 사항|Description|  
|-----------------|--------------------|------------------|-----------------|  
|**CONNECTION_ID**|**DBTYPE_I4**|예|연결을 식별하는 고유 번호입니다.|  
|**CONNECTION_USER_NAME**|**DBTYPE_WSTR**|예|연결 사용자 이름입니다.|  
|**CONNECTION_IMPERSONATED_USER_NAME**|**DBTYPE_WSTR**|예|나중에 사용하도록 예약되어 있습니다. Analysis Services는 항상 CONNECTION_IMPERSONATED_USER_NAME 값으로 NULL을 반환합니다.|  
|**CONNECTION_HOST_NAME**|**DBTYPE_WSTR**|예|연결을 시작한 컴퓨터의 이름입니다.|  
|**CONNECTION_HOST_APPLICATION**|**DBTYPE_WSTR**||연결을 시작한 응용 프로그램의 이름입니다.|  
|**CONNECTION_START_TIME**|**DBTYPE_DBTIMESTAMP**||연결이 시작된 서버 UTC 날짜 및 시간입니다.|  
|**CONNECTION_ELAPSED_TIME_MS**|**DBTYPE_I8**|예|연결이 시작된 이후에 경과된 시간(밀리초)입니다.|  
|**CONNECTION_LAST_COMMAND_START_TIME**|**DBTYPE_DBTIMESTAMP**||마지막 명령의 실행이 시작된 서버 UTC 날짜 및 시간입니다.|  
|**CONNECTION_LAST_COMMAND_END_TIME**|**DBTYPE_DBTIMESTAMP**||마지막 명령의 실행을 마친 서버 UTC 날짜 및 시간입니다.|  
|**CONNECTION_LAST_COMMAND_ELAPSED_TIME_MS**|**DBTYPE_I8**|예|마지막 명령 실행이 끝난 이후에 경과된 시간(밀리초)입니다.|  
|**CONNECTION_IDLE_TIME_MS**|**DBTYPE_I8**|예|연결이 시작된 이후의 유휴 시간(밀리초)입니다.|  
|**CONNECTION_BYTES_SENT**|**DBTYPE_I8**||연결이 시작된 이후에 연결이 보낸 누적 바이트 수입니다.|  
|**CONNECTION_DATA_BYTES_SENT**|**DBTYPE_I8**||연결이 시작된 이후에 연결이 보낸 누적 데이터 바이트 수입니다.<br /><br /> 연결 내에서 압축된 데이터 이동입니다. 이 값은 보낸 확장 데이터를 나타냅니다.|  
|**CONNECTION_BYTES_RECEIVED**|**DBTYPE_I8**||연결이 시작된 이후에 연결이 받은 누적 바이트 수입니다.|  
|**CONNECTION_DATA_BYTES_RECEIVED**|**DBTYPE_I8**||연결이 시작된 이후에 연결이 받은 누적 데이터 바이트 수입니다.<br /><br /> 연결 내에서 압축된 데이터 이동입니다. 이 값은 받은 확장 데이터를 나타냅니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|a07ccd25-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|연결|  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

