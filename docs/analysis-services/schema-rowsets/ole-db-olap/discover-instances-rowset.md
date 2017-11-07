---
title: "DISCOVER_INSTANCES 행 집합 | Microsoft Docs"
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
apiname:
- DISCOVER_INSTANCES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_INSTANCES rowset
ms.assetid: e0842e63-089d-468d-869f-634da343d9fb
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fbed6de71f83da959591003039fe5910a1a4c53d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="discoverinstances-rowset"></a>DISCOVER_INSTANCES 행 집합
  서버의 인스턴스를 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_INSTANCES** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**INSTANCE_NAME**|**DBTYPE_WSTR**||인스턴스의 이름입니다.|  
|**INSTANCE_PORT_NUMBER**|**DBTYPE_I4**||인스턴스가 수신하는 포트 번호입니다.|  
|**INSTANCE_STATE**|**DBTYPE_I4**||서버 인스턴스의 상태입니다.<br /><br /> **시작**<br /><br /> **중지됨**<br /><br /> **시작**<br /><br /> **중지**<br /><br /> **일시 중지됨**|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DISCOVER_INSTANCES** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**INSTANCE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목:  
 [OLAP 스키마 행 집합 용 OLE DB](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

