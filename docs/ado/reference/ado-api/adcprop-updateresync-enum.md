---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: afaadf62c38c318c759be1c452ff0953ba19c7d7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065299"
---
# <a name="adcpropupdateresyncenum"></a>ADCPROP_UPDATERESYNC_ENUM
지정 여부는 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드 뒤에 암시적 [다시 동기화](../../../ado/reference/ado-api/resync-method.md) 메서드 작업 그렇다면 해당 작업의 범위.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|호출 **Resync** 결합된 한 다른 모든 ADCPROP_UPDATERESYNC_ENUM 멤버 값을 사용 하 여 합니다.|  
|**adResyncAutoIncrement**|1|기본. 자동으로 증가 되거나 Microsoft Jet 일련 번호 필드 등 Microsoft SQL Server Id 열 데이터 원본에 의해 생성 되는 열에 대 한 새 id 값을 검색 하려고 시도 합니다.|  
|**adResyncConflicts**|2|호출 **Resync** 동시성 충돌로 인해 업데이트 또는 삭제 작업이 실패 하는 모든 행에 대 한 합니다.|  
|**adResyncInserts**|8|호출 **Resync** 성공적으로 삽입 되는 모든 행에 대 한 합니다. 그러나 자동 증분 열 값 재 동기화 되지 않습니다. 대신, 새로 삽입된 된 행의 내용은 기존 기본 키 값에 따라 다시 동기화 합니다. 기본 키가 자동 증가 값을 **Resync** 의도 한 행의 콘텐츠를 검색 하지 않습니다. 자동 증분 기본 키 값을 자동으로 증가 하는 것에 대 한 호출 **UpdateBatch** 결합 된 값을 가진 **adResyncAutoIncrement** + **adResyncInserts**.|  
|**adResyncNone**|0|호출 하지 않습니다 **Resync**합니다.|  
|**adResyncUpdates**|4|호출 **Resync** 성공적으로 업데이트 된 모든 행에 대 한 합니다.|  
  
## <a name="applies-to"></a>적용 대상  
 [Update Resync 속성 - 동적(ADO)](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)
