---
title: DISCOVER_INSTANCES 행 집합 | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0acc45eb2ea114a8d1c685aa6b3e867a4eaa967d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032904"
---
# <a name="discoverinstances-rowset"></a>DISCOVER_INSTANCES 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
  
