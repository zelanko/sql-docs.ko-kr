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
author: rothja
ms.author: jroth
ms.openlocfilehash: 864938729153a1cd3f8f31f2e4ba04b075d2f713
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758649"
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
[연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체에 대 한 트랜잭션 격리 수준을 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adXactUnspecified**|-1|공급자가 지정 된 것과 다른 격리 수준을 사용 하 고 있지만 수준을 확인할 수 없음을 나타냅니다.|  
|**adXactChaos**|16|격리 된 높은 트랜잭션 으로부터의 보류 중인 변경 내용을 덮어쓸 수 없음을 나타냅니다.|  
|**adXactBrowse**|256|한 트랜잭션에서 다른 트랜잭션의 커밋되지 않은 변경 내용을 볼 수 있음을 나타냅니다.|  
|**adXactReadUncommitted**|256|**AdXactBrowse**와 동일 합니다.|  
|**adXactCursorStability**|4096|한 트랜잭션에서 커밋된 후에만 다른 트랜잭션의 변경 내용을 볼 수 있음을 나타냅니다.|  
|**adXactReadCommitted**|4096|**AdXactCursorStability**와 동일 합니다.|  
|**adXactRepeatableRead**|65536|한 트랜잭션에서 다른 트랜잭션의 변경 내용을 볼 수 없지만 다시 쿼리하면 새 **레코드 집합** 개체를 검색할 수 있음을 나타냅니다.|  
|**adXactIsolated**|1048576|트랜잭션이 다른 트랜잭션과 격리 되어 수행 됨을 나타냅니다.|  
|**adXactSerializable**|1048576|**AdXactIsolated**와 동일 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums. IsolationLevel|  
|AdoEnums. IsolationLevel|  
|AdoEnums. IsolationLevel|  
|AdoEnums. IsolationLevel. READUNCOMMITTED|  
|AdoEnums. IsolationLevel. CURSORSTABILITY|  
|AdoEnums. IsolationLevel. READCOMMITTED|  
|AdoEnums. IsolationLevel. REPEATABLEREAD|  
|AdoEnums. IsolationLevel|  
|AdoEnums. IsolationLevel|  
  
## <a name="applies-to"></a>적용 대상  
 [IsolationLevel 속성](../../../ado/reference/ado-api/isolationlevel-property.md)
