---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7c57878b73c3c6a20f8dc0a8abd422c12a0446a2
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711731"
---
# <a name="recordstatusenum"></a>RecordStatusEnum
지정 된 [상태](../../../ado/reference/ado-api/status-property-ado-recordset.md) 일괄 처리 업데이트 및 기타 대량 작업 관련 레코드의 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adRecCanceled**|0x100|작업 취소 되었기 때문에 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecCantRelease**|0x400|새 레코드가 기존 레코드 잠겨 있으므로 저장 되지 않았습니다 나타냅니다.|  
|**adRecConcurrencyViolation**|0x800|낙관적 동시성을 사용 하는 레코드 저장 되지 않았음을 나타냅니다.|  
|**adRecDBDeleted**|0x40000|데이터 원본에서 레코드를 이미 삭제 된 것을 나타냅니다.|  
|**adRecDeleted**|0x4|레코드가 삭제 되었음을 나타냅니다.|  
|**adRecIntegrityViolation**|0x1000|사용자 무결성 제약 조건을 위반 했습니다. 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecInvalid**|0x10|해당 책갈피 유효 하지 않으므로 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecMaxChangesExceeded**|0x2000|덤프가 너무 많아 보류 중인 변경 내용 레코드 저장 되지 않았음을 나타냅니다.|  
|**adRecModified**|0x2|레코드 수정 된 것을 나타냅니다.|  
|**adRecMultipleChanges**|0x40|이 영향을 미칠 수 레코드가 여러 개 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecNew**|0x1|새 레코드를 나타냅니다.|  
|**adRecObjectOpen**|0x4000|열려 있는 저장소 개체와 충돌이 발생 하는 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecOK**|0|레코드가 성공적으로 업데이트 되었음을 나타냅니다.|  
|**adRecOutOfMemory**|0x8000|컴퓨터에 메모리가 부족 하기 때문에 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecPendingChanges**|0x80|보류 중인 삽입을 가리키는 레코드 저장 되지 않았음을 나타냅니다.|  
|**adRecPermissionDenied**|0x10000|사용자의 권한이 부족 하기 때문에 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecSchemaViolation**|0x20000|기본 데이터베이스의 구조를 위반 하기 때문에 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecUnmodified**|0x8|레코드 수정 되지 않았음을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 AdoEnums.RecordStatus.  
  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.RecordStatus.CANCELED|  
|AdoEnums.RecordStatus.CANTRELEASE|  
|AdoEnums.RecordStatus.CONCURRENCYVIOLATION|  
|AdoEnums.RecordStatus.DBDELETED|  
|AdoEnums.RecordStatus.DELETED|  
|AdoEnums.RecordStatus.INTEGRITYVIOLATION|  
|AdoEnums.RecordStatus.INVALID|  
|AdoEnums.RecordStatus.MAXCHANGESEXCEEDED|  
|AdoEnums.RecordStatus.MODIFIED|  
|AdoEnums.RecordStatus.MULTIPLECHANGES|  
|AdoEnums.RecordStatus.NEW|  
|AdoEnums.RecordStatus.OBJECTOPEN|  
|AdoEnums.RecordStatus.OK|  
|AdoEnums.RecordStatus.OUTOFMEMORY|  
|AdoEnums.RecordStatus.PENDINGCHANGES|  
|AdoEnums.RecordStatus.PERMISSIONDENIED|  
|AdoEnums.RecordStatus.SCHEMAVIOLATION|  
|AdoEnums.RecordStatus.UNMODIFIED|  
  
## <a name="applies-to"></a>적용 대상  
 [Status 속성(ADO 레코드 집합)](../../../ado/reference/ado-api/status-property-ado-recordset.md)
