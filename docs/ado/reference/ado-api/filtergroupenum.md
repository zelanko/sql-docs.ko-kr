---
title: FilterGroupEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FilterGroupEnum
helpviewer_keywords:
- FilterGroupEnum enumeration [ADO]
ms.assetid: b22e725e-84bd-4286-a070-290c278c3783
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 89cab313736a8d5acf2f7796ea79fb5649f85ab2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028133"
---
# <a name="filtergroupenum"></a>FilterGroupEnum
필터링 할 레코드의 그룹을 지정 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|마지막 영향을 받는 레코드만 보기에 대 한 필터 [삭제](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [Resync](../../../ado/reference/ado-api/resync-method.md)를 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), 또는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 호출 합니다.|  
|**adFilterConflictingRecords**|5|마지막 일괄 처리 업데이트를 실패 한 레코드를 보기 위한 필터입니다.|  
|**adFilterFetchedRecords**|3|현재 캐시에서 레코드를 보기에 대 한 필터-즉, 데이터베이스에서 레코드를 검색에 대 한 마지막 호출 결과입니다.|  
|**adFilterNone**|0|현재 필터를 제거 하 고 보기에 대 한 모든 레코드를 복원 합니다.|  
|**adFilterPendingRecords**|1|레코드만 보기에 대 한 필터는 변경 되었지만 서버에 아직 보내지 않았습니다. 일괄 업데이트 모드에만 적용 됩니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.FilterGroup.AFFECTEDRECORDS|  
|AdoEnums.FilterGroup.CONFLICTINGRECORDS|  
|AdoEnums.FilterGroup.FETCHEDRECORDS|  
|AdoEnums.FilterGroup.NONE|  
|AdoEnums.FilterGroup.PENDINGRECORDS|  
  
## <a name="applies-to"></a>적용 대상  
 [Filter 속성](../../../ado/reference/ado-api/filter-property.md)
