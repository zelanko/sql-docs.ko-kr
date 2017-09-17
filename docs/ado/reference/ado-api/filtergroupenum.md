---
title: FilterGroupEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- FilterGroupEnum
helpviewer_keywords:
- FilterGroupEnum enumeration [ADO]
ms.assetid: b22e725e-84bd-4286-a070-290c278c3783
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 424bb4b32915c774778cfd32dab18c42c5e573a8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="filtergroupenum"></a>FilterGroupEnum
필터링 할 레코드의 그룹을 지정 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|마지막 영향을 받는 레코드만 보기에 대 한 필터 [삭제](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), 또는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 호출 합니다.|  
|**adFilterConflictingRecords**|5|마지막 일괄 처리 업데이트를 실패 한 레코드를 보기 위한 필터입니다.|  
|**adFilterFetchedRecords**|3|현재 캐시에서 레코드를 보기 위한 필터-즉, 데이터베이스에서 레코드를 검색 한 마지막 호출의 결과입니다.|  
|**adFilterNone**|0|현재 필터를 제거 하 고 보기에 대 한 모든 레코드를 복원 합니다.|  
|**그**|1.|레코드에만 보기에 대 한 필터를 변경 되었지만 서버로 아직 보내지 않았습니다. 일괄 업데이트 모드에만 적용할 수 있습니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 패키지에 대 한 **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.FilterGroup.AFFECTEDRECORDS|  
|AdoEnums.FilterGroup.CONFLICTINGRECORDS|  
|AdoEnums.FilterGroup.FETCHEDRECORDS|  
|AdoEnums.FilterGroup.NONE|  
|AdoEnums.FilterGroup.PENDINGRECORDS|  
  
## <a name="applies-to"></a>적용 대상  
 [Filter 속성](../../../ado/reference/ado-api/filter-property.md)
