---
title: DISCOVER_INSTANCES 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DISCOVER_INSTANCES
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_INSTANCES rowset
ms.assetid: e0842e63-089d-468d-869f-634da343d9fb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8a0f716f32898668e019db15aef62e140e9c0d09
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198593"
---
# <a name="discoverinstances-rowset"></a>DISCOVER_INSTANCES 행 집합
  서버의 인스턴스를 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DISCOVER_INSTANCES` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`INSTANCE_NAME`|`DBTYPE_WSTR`||인스턴스의 이름입니다.|  
|`INSTANCE_PORT_NUMBER`|`DBTYPE_I4`||인스턴스가 수신하는 포트 번호입니다.|  
|`INSTANCE_STATE`|`DBTYPE_I4`||서버 인스턴스의 상태입니다.<br /><br /> -   `Started`<br />-   `Stopped`<br />-   `Starting`<br />-   `Stopping`<br />-   `Paused`|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 `DISCOVER_INSTANCES` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`INSTANCE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목  
 [OLAP용 OLE DB 스키마 행 집합](ole-db-for-olap-schema-rowsets.md)  
  
  
