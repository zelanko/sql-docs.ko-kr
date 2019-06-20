---
title: IsolationLevelEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- IsolationLevelEnum
helpviewer_keywords:
- IsolationLevelEnum enumeration [ADO]
ms.assetid: 8e17a7bc-b8a3-4ae2-b6c9-ce088ad31fdf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: aea36947856b26d33a0d777374eccf02a7cddb6a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66694758"
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
에 대 한 트랜잭션 격리 수준을 지정 된 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adXactUnspecified**|-1|공급자가 지정 하는 보다 다양 한 격리 수준을 사용 하지만 수준을 확인할 수 없습니다 나타냅니다.|  
|**adXactChaos**|16|보류 중인 변경 내용을 격리 수준이 높은 트랜잭션에서 덮어쓸 수 없습니다 나타냅니다.|  
|**adXactBrowse**|256|하나의 트랜잭션에서 보면 커밋되지 않은 변경 내용을 다른 트랜잭션에서 나타냅니다.|  
|**adXactReadUncommitted**|256|동일 **adXactBrowse**합니다.|  
|**adXactCursorStability**|4096|하나의 트랜잭션에서 변경 확인할 수 있습니다 다른 트랜잭션에서 커밋 받은 후에 나타냅니다.|  
|**adXactReadCommitted**|4096|동일 **adXactCursorStability**합니다.|  
|**adXactRepeatableRead**|65536|한 트랜잭션에서 다른 트랜잭션의 변경 내용을 볼 수 있지만 해당 다시 쿼리하여 새로운 검색할 수 나타냅니다 **레코드 집합** 개체입니다.|  
|**adXactIsolated**|1048576|트랜잭션을 수행 하는 다른 트랜잭션 격리를 나타냅니다.|  
|**adXactSerializable**|1048576|동일 **adXactIsolated**합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.IsolationLevel.UNSPECIFIED|  
|AdoEnums.IsolationLevel.CHAOS|  
|AdoEnums.IsolationLevel.BROWSE|  
|AdoEnums.IsolationLevel.READUNCOMMITTED|  
|AdoEnums.IsolationLevel.CURSORSTABILITY|  
|AdoEnums.IsolationLevel.READCOMMITTED|  
|AdoEnums.IsolationLevel.REPEATABLEREAD|  
|AdoEnums.IsolationLevel.ISOLATED|  
|AdoEnums.IsolationLevel.SERIALIZABLE|  
  
## <a name="applies-to"></a>적용 대상  
 [IsolationLevel 속성](../../../ado/reference/ado-api/isolationlevel-property.md)
