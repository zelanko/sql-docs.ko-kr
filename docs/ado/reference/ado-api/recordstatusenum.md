---
title: RecordStatusEnum | Microsoft Docs
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
- RecordStatusEnum
helpviewer_keywords:
- RecordStatusEnum enumeration [ADO]
ms.assetid: 506fdd70-4452-4e83-95d5-c94311988dfa
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9bf2413bed1bbdf96b83b7e805aac90529a721c9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="recordstatusenum"></a>RecordStatusEnum
지정 된 [상태](../../../ado/reference/ado-api/status-property-ado-recordset.md) 일괄 업데이트 및 다른 대량 작업과 관련 된 레코드의 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adRecCanceled**|0x100|작업이 취소 된 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecCantRelease**|0x400|기존 레코드 잠 겼으 새 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecConcurrencyViolation**|0x800|낙관적 동시성을 사용 하는 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecDBDeleted**|0x40000|레코드에 이미 데이터 원본에서 삭제 되었음을 나타냅니다.|  
|**adRecDeleted**|0x4|레코드가 삭제 되었음을 나타냅니다.|  
|**adRecIntegrityViolation**|0x1000|무결성 제약 조건을 위반 하는 사용자 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecInvalid**|0x10|올바르지 않으면 해당 책갈피는 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecMaxChangesExceeded**|0x2000|보류 중인 변경 내용이 너무 많은 없었기 때문에 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecModified**|0x2|레코드가 수정 된 것을 나타냅니다.|  
|**adRecMultipleChanges**|0x40|것에 영향을 미칠 레코드가 여러 개 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecNew**|0x1|새 레코드 임을 나타냅니다.|  
|**adRecObjectOpen**|0x4000|열려 있는 저장소 개체와 충돌이 발생 하는 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecOK**|0|레코드 성공적으로 업데이트 했는지를 나타냅니다.|  
|**adRecOutOfMemory**|0x8000|컴퓨터에 메모리 부족 때문에 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecPendingChanges**|0x80|보류 중인 삽입을 했기 때문에 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecPermissionDenied**|0x10000|사용자에 게 권한이 부족 하 여 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecSchemaViolation**|0x20000|기본 데이터베이스의 구조를 위반 하기 때문에 레코드가 저장 되지 않았음을 나타냅니다.|  
|**adRecUnmodified**|0x8|레코드가 수정 되지 않았음을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 AdoEnums.RecordStatus 합니다.  
  
 패키지에 대 한 **com.ms.wfc.data**  
  
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
