---
description: Update Resync 속성 - 동적(ADO)
title: 업데이트 다시 동기화 속성-동적 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Update Resync property [ADO]
ms.assetid: 8a3bb608-66d7-4128-a3ef-84cb0556de0d
author: rothja
ms.author: jroth
ms.openlocfilehash: 506fd7fecee179a055e23ffad1beab76bcd2fbe2
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988094"
---
# <a name="update-resync-property-dynamic-ado"></a>Update Resync 속성 - 동적(ADO)
[UpdateBatch](./updatebatch-method.md) 메서드 뒤에 암시적 다시 [동기화](./resync-method.md) 메서드 작업이 오고 그 뒤에 해당 작업의 범위가 있는지 여부를 지정 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 하나 이상의 [ADCPROP_UPDATERESYNC_ENUM](./adcprop-updateresync-enum.md) 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 값의 나머지 조합을 이미 나타내는 adResyncAll를 제외 하 고 ADCPROP_UPDATERESYNC_ENUM의 값을 결합할 수 있습니다.  
  
 상수 **adResyncConflicts** 는 재 동기화 값을 기본 값으로 저장 하지만 보류 중인 변경 내용은 재정의 하지 않습니다.  
  
 **업데이트 다시 동기화** 는 [CursorLocation](./cursorlocation-property-ado.md) 속성이 **AdUseClient**로 설정 된 경우 [레코드 집합](./recordset-object-ado.md) 개체 [속성](./properties-collection-ado.md) 컬렉션에 추가 되는 동적 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)