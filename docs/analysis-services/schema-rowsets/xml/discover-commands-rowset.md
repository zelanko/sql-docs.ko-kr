---
title: "DISCOVER_COMMANDS 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
helpviewer_keywords:
- DISCOVER_COMMANDS rowset
ms.assetid: d228f265-05d9-4d2c-a622-44c73eab7a71
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 49d95852f838c67a34e175ed160c6abdad93bd61
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="discovercommands-rowset"></a>DISCOVER_COMMANDS 행 집합
  서버에 열려 있는 연결의 현재 실행 중이거나 마지막으로 실행된 명령에 대한 리소스 사용량 및 작업 정보를 제공합니다.  
  
 **적용 대상:** 테이블 형식 모델, 다차원 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_COMMANDS** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|제한|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**SESSION_SPID**|**DBTYPE_I4**|예|세션 ID입니다.|  
|**SESSION_COMMAND_COUNT**|**DBTYPE_I4**||세션이 시작된 이후에 실행된 명령 수입니다.|  
|**COMMAND_START_TIME**|**DBTYPE_DBTIMESTAMP**||마지막 명령이 시작된 날짜 및 시간(서버 UTC 시간으로 표시)입니다.|  
|**COMMAND_ELAPSED_TIME_MS**|**DBTYPE_I8**||명령이 시작된 이후에 경과된 시간(밀리초)입니다.|  
|**COMMAND_CPU_TIME_MS**|**DBTYPE_I8**||명령 실행이 시작된 이후에 명령에 사용된 CPU 시간(밀리초)입니다.|  
|**COMMAND_READS**|**DBTYPE_I8**||명령이 시작된 이후부터 누적된 디스크 읽기 수입니다.|  
|**COMMAND_READ_KB**|**DBTYPE_I8**||명령이 시작된 이후부터 디스크에서 읽은 누적 데이터 값(KB)입니다.|  
|**COMMAND_WRITES**|**DBTYPE_I8**||명령이 시작된 이후부터 누적된 디스크 쓰기 수입니다.|  
|**COMMAND_WRITE_KB**|**DBTYPE_I8**||명령이 시작된 이후부터 디스크에 기록된 누적 데이터 값(KB)입니다.|  
|**COMMAND_TEXT**|**DBTYPE_WSTR**||명령 텍스트입니다.|  
|**COMMAND_END_TIME**|**DBTYPE_DBTIMESTAMP**||명령의 실행을 마친 서버 UTC 날짜 및 시간입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|a07ccd34-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|명령|  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

