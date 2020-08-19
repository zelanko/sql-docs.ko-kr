---
description: RecordStatusEnum
title: RecordStatusEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordStatusEnum
helpviewer_keywords:
- RecordStatusEnum enumeration [ADO]
ms.assetid: 506fdd70-4452-4e83-95d5-c94311988dfa
author: rothja
ms.author: jroth
ms.openlocfilehash: 0d48e9538fb8ec4f0dac8c3a17457b04b0ace963
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442393"
---
# <a name="recordstatusenum"></a>RecordStatusEnum
일괄 업데이트 및 기타 대량 작업과 관련 된 레코드의 [상태](../../../ado/reference/ado-api/status-property-ado-recordset.md) 를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adRecCanceled**|0x100|작업이 취소 되었으므로 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecCantRelease**|0x400|기존 레코드가 잠겨있기 때문에 새 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecConcurrencyViolation**|0x800|낙관적 동시성이 사용 중이기 때문에 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecDBDeleted**|0x40000|레코드를 데이터 소스에서 이미 삭제 했음을 나타냅니다.|  
|**adRecDeleted**|0x4|레코드가 삭제 되었음을 나타냅니다.|  
|**adRecIntegrityViolation**|0x1000|사용자가 무결성 제약 조건을 위반 하 여 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecInvalid**|0x10|해당 책갈피가 잘못 되어 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecMaxChangesExceeded**|0x2000|보류 중인 변경 내용이 너무 많기 때문에 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecModified**|0x2|레코드가 수정 되었음을 나타냅니다.|  
|**adRecMultipleChanges**|0x40|여러 레코드에 영향을 주므로 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecNew**|0x1|레코드가 새로운 레코드 임을 나타냅니다.|  
|**adRecObjectOpen**|0x4000|열려 있는 저장소 개체와 충돌 하 여 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecOK**|0|레코드가 성공적으로 업데이트 되었음을 나타냅니다.|  
|**adRecOutOfMemory**|0x8000|컴퓨터에 메모리가 부족 하 여 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecPendingChanges**|0x80|보류 중인 insert를 참조 하므로 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecPermissionDenied**|0x10000|사용자의 권한이 부족 하 여 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecSchemaViolation**|0x20000|는 기본 데이터베이스의 구조를 위반 하므로 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecUnmodified**|0x8|레코드가 수정 되지 않았음을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 AdoEnums.RecordStatus.  
  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums. RecordStatus|  
|AdoEnums.RecordStatus.CANTRELEASE|  
|AdoEnums. RecordStatus. CONCURRENCYVIOLATION|  
|AdoEnums.RecordStatus.DBDELETED|  
|AdoEnums.RecordStatus.DELETED|  
|AdoEnums. RecordStatus|  
|AdoEnums.RecordStatus.INVALID|  
|AdoEnums.RecordStatus.MAXCHANGESEXCEEDED|  
|AdoEnums.RecordStatus.MODIFIED|  
|AdoEnums.RecordStatus.MULTIPLECHANGES|  
|AdoEnums.RecordStatus.NEW|  
|AdoEnums. RecordStatus를 엽니다.|  
|AdoEnums.RecordStatus.OK|  
|AdoEnums. RecordStatus. OUTOFMEMORY|  
|AdoEnums. RecordStatus 변경|  
|AdoEnums. RecordStatus가 거부 되었습니다.|  
|AdoEnums.RecordStatus.SCHEMAVIOLATION|  
|AdoEnums.RecordStatus.UNMODIFIED|  
  
## <a name="applies-to"></a>적용 대상  
 [Status 속성(ADO 레코드 집합)](../../../ado/reference/ado-api/status-property-ado-recordset.md)
