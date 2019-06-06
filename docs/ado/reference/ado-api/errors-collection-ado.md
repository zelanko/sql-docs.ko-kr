---
title: Errors 컬렉션 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Errors
- Connection15::get_Errors
- Connection15::GetErrors
helpviewer_keywords:
- Errors collection [ADO]
ms.assetid: 290819e1-7b39-4e1e-a93b-801257138b00
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 109b7ff83e6b3f722560dae0a034c4bf37da137f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719271"
---
# <a name="errors-collection-ado"></a>Errors 컬렉션(ADO)
모든 포함 된 [오류](../../../ado/reference/ado-api/error-object.md) 단일 공급자 관련 오류에 대 한 응답에서 생성 된 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 ADO 개체와 관련 된 모든 작업이 하나 이상의 공급자 오류를 생성할 수 있습니다. 하나 이상의 오류가 발생할 때마다 **오류** 개체에 배치할 수 있습니다 합니다 **오류** 의 컬렉션을 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다. 다른 ADO 작업에서 오류를 생성 하는 경우는 **오류** 컬렉션의 선택을 취소 하 고 새 집합입니다 **오류** 개체에 배치할 수 있습니다를 **오류** 컬렉션.  
  
 각 **오류** 개체는 ADO 오류가 아니라 특정 공급자 오류를 나타냅니다. ADO 오류는 런타임 예외 처리 메커니즘에 노출 됩니다. 예를 들어, Microsoft Visual Basic의 ADO 관련 오류가 발생 트리거할를 [onError](../../../ado/reference/rds-api/onerror-event-rds.md) 이벤트에 표시 합니다 **Err** 개체입니다.  
  
 ADO 작업 오류를 생성 하지는 영향을 주지 않습니다는 **오류** 컬렉션입니다. 사용 하 여는 [지우기](../../../ado/reference/ado-api/clear-method-ado.md) 수동으로 지워야 메서드를 **오류** 컬렉션입니다.  
  
 집합이 **오류** 개체를 **오류** 컬렉션에 하나의 명령문에 대 한 응답으로 발생 한 모든 오류에 설명 합니다. 특정 오류를 열거 합니다 **오류** 컬렉션 보다 정확 하 게, 오류의 원인과 확인 하 고 복구 하는 적절 한 단계를 수행 하면 오류 처리 루틴을 사용 하면 됩니다.  
  
 일부 속성 및 메서드 반환로 표시 되는 경고 **오류** 개체를 **오류** 컬렉션 하지만 프로그램의 실행을 중단 되지는 않습니다. 호출 하기 전에 [다시 동기화](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), 또는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체는 [엽니다](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드를를 **연결** 개체를 가져오거나 설정 합니다 [필터](../../../ado/reference/ado-api/filter-property.md) 속성을를 **레코드 집합** 개체를 호출를 **지우기**메서드는 **오류** 컬렉션입니다. 이런 방식으로 읽을 수 있습니다를 [개수](../../../ado/reference/ado-api/count-property-ado.md) 의 속성을 **오류** 를 테스트할 컬렉션 경고를 반환 합니다.  
  
> [!NOTE]
>  참조 된 **오류** 단일 ADO 작업 오류가 여러 개 생성 되는 방식에 대 한 자세한 설명은 항목 개체입니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [오류 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/errors-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
