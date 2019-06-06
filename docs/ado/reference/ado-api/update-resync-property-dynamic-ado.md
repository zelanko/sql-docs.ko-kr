---
title: Resync 속성-동적 (ADO)를 업데이트 합니다. | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Update Resync property [ADO]
ms.assetid: 8a3bb608-66d7-4128-a3ef-84cb0556de0d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 57ff6e224537feebaf51eee1435ed64ab845025d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710521"
---
# <a name="update-resync-property-dynamic-ado"></a>Update Resync 속성 - 동적(ADO)
지정 여부는 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드 뒤에 암시적 [다시 동기화](../../../ado/reference/ado-api/resync-method.md) 메서드 작업 그렇다면 해당 작업의 범위.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 하나를 반환 합니다 [ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md) 값입니다.  
  
## <a name="remarks"></a>Remarks  
 이미를 나머지 값의 조합을 나타내는 adResyncAll 제외 하 고 ADCPROP_UPDATERESYNC_ENUM의 값을 결합할 수 있습니다.  
  
 상수 **adResyncConflicts** 기본 값으로 다시 동기화 값을 저장 하지만 보류 중인 변경 내용이 재정의 하지 않습니다.  
  
 **다시 동기화를 업데이트** 에 추가 하는 동적 속성을 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션 때 합니다 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성**adUseClient**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
