---
title: EventReasonEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: EventReasonEnum
helpviewer_keywords: EventReasonEnum enumeration [ADO]
ms.assetid: 7d4a5496-ec2d-4936-b36a-7049a82be4b4
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7f4f863b81149b2cc8e6166be3cf61621fc1cc98
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="eventreasonenum"></a>EventReasonEnum
발생할 이벤트를 발생 시킨 이유를 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|새 레코드를 추가 하는 작업입니다.|  
|**adRsnClose**|9|작업 종료는 **레코드 집합**합니다.|  
|**adRsnDelete**|2|작업 레코드를 삭제 합니다.|  
|**adRsnFirstChange**|11|레코드에 첫 번째 변경 내용을 적용 하는 작업입니다.|  
|**adRsnMove**|10|작업 내에서 레코드 포인터를 이동는 **레코드 집합**합니다.|  
|**adRsnMoveFirst**|12|작업의 첫 번째 레코드를 레코드 포인터를 이동는 **레코드 집합**합니다.|  
|**adRsnMoveLast**|15|작업의 마지막 레코드를 레코드 포인터를 이동는 **레코드 집합**합니다.|  
|**adRsnMoveNext**|13|작업에서 다음 레코드를 레코드 포인터를 이동는 **레코드 집합**합니다.|  
|**adRsnMovePrevious**|14|작업에서 이전 레코드를 레코드 포인터를 이동는 **레코드 집합**합니다.|  
|**adRsnRequery**|7|쿼리가 다시 실행 하는 작업은 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.|  
|**adRsnResynch**|8|작업을 다시 동기화는 **레코드 집합** 데이터베이스와 함께 합니다.|  
|**adRsnUndoAddNew**|5|새 레코드 추가 취소 한 작업입니다.|  
|**adRsnUndoDelete**|6|레코드의 삭제를 취소 한 작업입니다.|  
|**adRsnUndoUpdate**|4|레코드의 업데이트를 취소 한 작업입니다.|  
|**adRsnUpdate**|3|기존 레코드를 업데이트 한 작업입니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 패키지에 대 한 **com.ms.wfc.data**  
  
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
