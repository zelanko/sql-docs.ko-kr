---
description: ADCPROP_UPDATERESYNC_ENUM
title: ADCPROP_UPDATERESYNC_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATERESYNC_ENUM
helpviewer_keywords:
- ADCPROP_UPDATERESYNC_ENUM [ADO]
ms.assetid: bc9e1a37-e969-47e9-8382-0bbfffa2034f
author: rothja
ms.author: jroth
ms.openlocfilehash: 81d1ff4bf67f103b613cb925a590b4d00e54482a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451595"
---
# <a name="adcprop_updateresync_enum"></a>ADCPROP_UPDATERESYNC_ENUM
[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드 뒤에 암시적 다시 [동기화](../../../ado/reference/ado-api/resync-method.md) 메서드 작업이 오고 그 뒤에 해당 작업의 범위가 있는지 여부를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|다른 모든 ADCPROP_UPDATERESYNC_ENUM 멤버의 결합 된 값을 사용 하 여 다시 **동기화** 를 호출 합니다.|  
|**adResyncAutoIncrement**|1|기본값 Microsoft Jet 일련 번호 필드 또는 Microsoft SQL Server Id 열과 같은 데이터 원본에 의해 자동으로 증가 하거나 생성 되는 열의 새 id 값을 검색 하려고 시도 합니다.|  
|**adResyncConflicts**|2|동시성 충돌 때문에 업데이트 또는 삭제 작업이 실패 한 모든 행에 대해 다시 **동기화** 를 호출 합니다.|  
|**adResyncInserts**|8|성공적으로 삽입 된 모든 행에 대해 다시 **동기화** 를 호출 합니다. 그러나 AutoIncrement 열 값은 다시 동기화 되지 않습니다. 대신, 새로 삽입 된 행의 내용이 기존 기본 키 값에 따라 다시 동기화 됩니다. 기본 키가 AutoIncrement 값 이면 다시 **동기화** 는 원하는 행의 내용을 검색 하지 않습니다. 자동 증분 기본 키 값을 자동으로 증가 시키려면 조합 된 값 **adResyncAutoIncrement**adResyncInserts를 사용 하 여 **UpdateBatch** 를 호출 합니다  +  **adResyncInserts**.|  
|**adResyncNone**|0|는 **Resync**를 호출 하지 않습니다.|  
|**adResyncUpdates**|4|성공적으로 업데이트 된 모든 행에 대해 다시 **동기화** 를 호출 합니다.|  
  
## <a name="applies-to"></a>적용 대상  
 [Update Resync 속성 - 동적(ADO)](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)
