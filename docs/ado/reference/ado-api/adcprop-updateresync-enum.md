---
title: ADCPROP_UPDATERESYNC_ENUM | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ADCPROP_UPDATERESYNC_ENUM
helpviewer_keywords: ADCPROP_UPDATERESYNC_ENUM [ADO]
ms.assetid: bc9e1a37-e969-47e9-8382-0bbfffa2034f
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 998868819c0e0b56783598ea3f2af5a3d799f82c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="adcpropupdateresyncenum"></a>ADCPROP_UPDATERESYNC_ENUM
지정 여부는 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드 뒤 암시적 [다시 동기화](../../../ado/reference/ado-api/resync-method.md) 메서드 작업 그리고 있다면 해당 작업의 범위입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|호출 **Resync** 다른 ADCPROP_UPDATERESYNC_ENUM 멤버의 조합 된 값을 사용 합니다.|  
|**adResyncAutoIncrement**|1.|기본. 자동으로 증가 되거나 Microsoft Jet 일련 번호 필드 또는 Microsoft SQL Server Id 열 등과 같이 데이터 소스에서 생성 된 열에 대 한 새 id 값을 검색 하려고 시도 합니다.|  
|**adResyncConflicts**|2|호출 **Resync** 동시성 충돌이 발생 하 여 업데이트 또는 삭제 작업이 실패 하는 모든 행에 대 한 합니다.|  
|**adResyncInserts**|8|호출 **Resync** 성공적으로 삽입 된 모든 행에 대 한 합니다. 그러나 자동 증분 열 값 재 동기화 되지 않습니다. 대신, 새로 삽입된 된 행의 내용은 다시 동기화 되 고 기존 기본 키 값에 따라 합니다. 기본 키가 자동 증가 하는 값을 **Resync** 의도 한 행의 콘텐츠를 검색 하지 않습니다. 자동 증분 기본 키 값을 자동으로 증가 하는 경우에 대 한 호출 **UpdateBatch** 조합 된 값을 가진 **adResyncAutoIncrement** + **adResyncInserts**.|  
|**adResyncNone**|0|호출 하지 않습니다 **Resync**합니다.|  
|**adResyncUpdates**|4|호출 **Resync** 성공적으로 업데이트 된 모든 행에 대 한 합니다.|  
  
## <a name="applies-to"></a>적용 대상  
 [Update Resync 속성 - 동적(ADO)](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)
