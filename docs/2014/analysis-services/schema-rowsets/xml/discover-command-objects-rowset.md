---
title: DISCOVER_COMMAND_OBJECTS 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DISCOVER_COMMAND_OBJECTS rowset
ms.assetid: 325114ee-3a50-4504-9782-dbf7c1a44778
caps.latest.revision: 21
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 78970be3b1ed127ad25e4c27fcf81044b1eb9dca
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37261199"
---
# <a name="discovercommandobjects-rowset"></a>DISCOVER_COMMAND_OBJECTS 행 집합
  참조된 명령에서 사용 중인 개체에 대한 리소스 사용량 및 작업 정보를 제공합니다.  
  
 **적용 대상:** 테이블 형식 모델, 다차원 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DISCOVER_COMMAND_OBJECTS` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|제한|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`SESSION_SPID`|`DBTYPE_I4`|예|세션 ID입니다.|  
|`SESSION_ID`|`DBTYPE_WSTR`|예|GUID와 같은 세션 고유 식별자입니다.|  
|`SESSION_COMMAND_COUNT`|`DBTYPE_I4`||명령 시퀀스 번호입니다.|  
|`OBJECT_PARENT_PATH`|`DBTYPE_WSTR`|예|현재 개체의 부모에 대한 경로입니다.|  
|`OBJECT_ID`|`DBTYPE_WSTR`|예|개체를 만들 때 정의된 개체 ID입니다.|  
|`OBJECT_VERSION`|`DBTYPE_I4`||개체의 메타데이터 버전 번호입니다. 이 번호는 개체가 변경될 때마다 변경됩니다.|  
|`OBJECT_DATA_VERSION`|`DBTYPE_I4`||개체 데이터의 계보 번호로서 개체가 처리될 때마다 증가합니다.|  
|`OBJECT_CPU_TIME_MS`|`DBTYPE_I8`||명령 실행이 시작된 이후에 개체에 사용된 CPU 시간(밀리초)입니다.|  
|`OBJECT_READ_KB`|`DBTYPE_I8`||명령이 시작된 이후부터 개체가 읽은 누적 데이터 값(KB)입니다.|  
|`OBJECT_READS`|`DBTYPE_I8`||명령이 시작된 이후부터 개체가 수행한 누적 읽기 작업 수입니다.|  
|`OBJECT_WRITE_KB`|`DBTYPE_I8`||명령이 시작된 이후부터 개체가 기록한 누적 데이터 값(킬로바이트)입니다.|  
|`OBJECT_WRITES`|`DBTYPE_I8`||명령이 시작된 이후부터 개체가 수행한 누적 쓰기 작업 수입니다.|  
|`OBJECT_ROWS_RETURNED`|`DBTYPE_I8`||명령이 시작된 이후에 개체가 호출자에게 반환한 행 수입니다.|  
|`OBJECT_ROWS_SCANNED`|`DBTYPE_I8`||명령이 시작된 이후에 개체가 검색한 행 수입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
> [!IMPORTANT]  
>  DISCOVER_COMMAND_OBJECTS 스키마 행 집합은 DMV 쿼리를 사용한 작업은 보고하지 않습니다.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|a07ccd35-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|CommandObjects|  
  
## <a name="see-also"></a>관련 항목  
 [XML for Analysis 스키마 행 집합](xml-for-analysis-schema-rowsets.md)  
  
  
