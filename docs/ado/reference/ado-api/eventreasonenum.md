---
title: EventReasonEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventReasonEnum
helpviewer_keywords:
- EventReasonEnum enumeration [ADO]
ms.assetid: 7d4a5496-ec2d-4936-b36a-7049a82be4b4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ba7675f5fe0abe02130de3c6bfc905070b24ec10
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697938"
---
# <a name="eventreasonenum"></a>EventReasonEnum
발생할 이벤트를 발생 시킨 이유를 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|작업에 새 레코드를 추가 합니다.|  
|**adRsnClose**|9|작업을 종료 합니다 **레코드 집합**합니다.|  
|**adRsnDelete**|2|작업 레코드를 삭제 합니다.|  
|**adRsnFirstChange**|11|작업은 레코드에 변경한 첫 번째입니다.|  
|**adRsnMove**|10|작업 내에서 레코드 포인터를 이동 합니다 **레코드 집합**합니다.|  
|**adRsnMoveFirst**|12|작업의 첫 번째 레코드를 레코드 포인터를 이동 합니다 **레코드 집합**합니다.|  
|**adRsnMoveLast**|15|작업의 마지막 레코드를 레코드 포인터를 이동 합니다 **레코드 집합**합니다.|  
|**adRsnMoveNext**|13|작업에서 다음 레코드를 레코드 포인터를 이동 합니다 **레코드 집합**합니다.|  
|**adRsnMovePrevious**|14|작업에서 이전 레코드를 레코드 포인터를 이동 합니다 **레코드 집합**합니다.|  
|**adRsnRequery**|7|쿼리가 다시 실행 하는 작업은 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.|  
|**adRsnResynch**|8|작업을 다시 동기화 합니다 **레코드 집합** 데이터베이스를 사용 하 여 합니다.|  
|**adRsnUndoAddNew**|5|새 레코드 추가 취소 하는 작업입니다.|  
|**adRsnUndoDelete**|6|작업은 레코드의 삭제를 취소 합니다.|  
|**adRsnUndoUpdate**|4|레코드의 업데이트를 취소 하는 한 작업입니다.|  
|**adRsnUpdate**|3|작업은 기존 레코드를 업데이트 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.EventReason.ADDNEW|  
|AdoEnums.EventReason.CLOSE|  
|AdoEnums.EventReason.DELETE|  
|AdoEnums.EventReason.FIRSTCHANGE|  
|AdoEnums.EventReason.MOVE|  
|AdoEnums.EventReason.MOVEFIRST|  
|AdoEnums.EventReason.MOVELAST|  
|AdoEnums.EventReason.MOVENEXT|  
|AdoEnums.EventReason.MOVEPREVIOUS|  
|AdoEnums.EventReason.REQUERY|  
|AdoEnums.EventReason.RESYNCH|  
|AdoEnums.EventReason.UNDOADDNEW|  
|AdoEnums.EventReason.UNDODELETE|  
|AdoEnums.EventReason.UNDOUPDATE|  
|AdoEnums.EventReason.UPDATE|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[WillChangeRecord 및 RecordChangeComplete 이벤트(ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[WillChangeRecordset 및 RecordsetChangeComplete 이벤트(ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|  
|[WillMove 및 MoveComplete 이벤트(ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)||
