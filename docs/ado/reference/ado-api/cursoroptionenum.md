---
title: CursorOptionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorOptionEnum
helpviewer_keywords:
- CursorOptionEnum enumeration [ADO]
ms.assetid: 4e10cda7-ce81-4466-94c2-844d38191cf1
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 46dbaded7bafcb7e553a58d2807e32466f7e6edf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="cursoroptionenum"></a>CursorOptionEnum
어떤 기능을 지정 된 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드를 테스트 해야 합니다.  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adAddNew**|0x1000400|지원 된 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) 메서드 새 레코드를 추가 합니다.|  
|**adApproxPosition**|0x4000|지원 된 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) 및 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 속성입니다.|  
|**adBookmark**|0x2000|지원 된 [책갈피](../../../ado/reference/ado-api/bookmark-property-ado.md) 특정 레코드에 액세스 하는 속성입니다.|  
|**adDelete**|0x1000800|지원 된 [삭제](../../../ado/reference/ado-api/delete-method-ado-recordset.md) 레코드를 삭제 하는 메서드.|  
|**adFind**|0x80000|지원 된 [찾을](../../../ado/reference/ado-api/find-method-ado.md) 의 행을 찾을 방법은 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.|  
|**adHoldRecords**|0x100|더 많은 레코드를 검색 하거나 모든 보류 중인 변경 내용을 커밋하지 않고 위치를 변경 합니다.|  
|**adIndex**|0x100000|지원 된 [인덱스](../../../ado/reference/ado-api/index-property.md) 인덱스 이름을 지정 하는 속성입니다.|  
|**adMovePrevious**|0x200|지원 된 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 및 [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 메서드 및 [이동](../../../ado/reference/ado-api/move-method-ado.md) 또는 [GetRows](../../../ado/reference/ado-api/getrows-method-ado.md) 현재 레코드를 이동 하는 메서드를 뒤로 이동 위치 책갈피 하지 않고도 합니다.|  
|**adNotify**|0x40000|기본 데이터 공급자에 알림을 지원 나타냅니다 (결정 하는 여부 **레코드 집합** 이벤트가 지원 됩니다).|  
|**adResync**|0x20000|지원 된 [Resync](../../../ado/reference/ado-api/resync-method.md) 기본 데이터베이스에 표시 되는 데이터와 함께 커서를 업데이트 하는 메서드.|  
|**adSeek**|0x200000|지원 된 [Seek](../../../ado/reference/ado-api/seek-method.md) 의 행을 찾을 방법은 **레코드 집합**합니다.|  
|**adUpdate**|0x1008000|지원 된 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드를 기존 데이터를 수정 합니다.|  
|**adUpdateBatch**|0x10000|에서는 일괄 처리 업데이트를 지원 ([UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 및 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드)를 공급자에 대 한 변경의 그룹을 전송 합니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.CursorOption.ADDNEW|  
|AdoEnums.CursorOption.APPROXPOSITION|  
|AdoEnums.CursorOption.BOOKMARK|  
|AdoEnums.CursorOption.DELETE|  
|AdoEnums.CursorOption.FIND|  
|AdoEnums.CursorOption.HOLDRECORDS|  
|AdoEnums.CursorOption.INDEX|  
|AdoEnums.CursorOption.MOVEPREVIOUS|  
|AdoEnums.CursorOption.NOTIFY|  
|AdoEnums.CursorOption.RESYNC|  
|AdoEnums.CursorOption.SEEK|  
|AdoEnums.CursorOption.UPDATE|  
|AdoEnums.CursorOption.UPDATEBATCH|  
  
## <a name="applies-to"></a>적용 대상  
 [Supports 메서드](../../../ado/reference/ado-api/supports-method.md)
