---
title: "Errors 컬렉션 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::Errors
- Connection15::get_Errors
- Connection15::GetErrors
helpviewer_keywords:
- Errors collection [ADO]
ms.assetid: 290819e1-7b39-4e1e-a93b-801257138b00
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 27ca46528314f34b769d505269ade0c73fb1b051
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="errors-collection-ado"></a>Errors 컬렉션 (ADO)
모든 포함 된 [오류](../../../ado/reference/ado-api/error-object.md) 단일 공급자 관련 오류에 대 한 응답에서 생성 된 개체입니다.  
  
## <a name="remarks"></a>주의  
 ADO 개체를 관련 된 모든 작업 공급자 오류가 하나 이상 생성할 수 있습니다. 하나 이상의 오류가 발생할 때마다 **오류** 에 개체를 배치할 수 있습니다는 **오류** 의 컬렉션은 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다. 다른 ADO 작업에서 오류를 생성 하는 경우는 **오류** 컬렉션을 지울 및 새로운 집합이 **오류** 개체에 추가할 수는 **오류** 컬렉션입니다.  
  
 각 **오류** 개체는 ADO 오류가 아니라 공급자 특정 오류를 나타냅니다. ADO 오류는 런타임 예외 처리 메커니즘에 노출 됩니다. 예를 들어 Microsoft Visual Basic에서 ADO 관련 오류 발생 트리거할는 [onError](../../../ado/reference/rds-api/onerror-event-rds.md) 이벤트에 표시는 **Err** 개체입니다.  
  
 오류를 생성 하지 않는 ADO 작업에 영향을 주지 않습니다 있어야는 **오류** 컬렉션입니다. 사용 하 여는 [지우기](../../../ado/reference/ado-api/clear-method-ado.md) 수동으로 지워야 메서드는 **오류** 컬렉션입니다.  
  
 집합이 **오류** 개체에 **오류** 하나의 명령문에 대 한 응답으로 발생 한 모든 오류 컬렉션에 설명 합니다. 특정 오류를 열거 하는 **오류** 컬렉션 보다 정확 하 게 한 오류의 원인과 확인 하 고 복구 하는 적절 한 단계를 수행 하면 오류 처리 루틴을 사용 하면 됩니다.  
  
 일부 속성 및 메서드로 표시 되는 경고를 반환 **오류** 개체에 **오류** 컬렉션 하지만 프로그램 실행이 중단 되지는 않습니다. 호출 하기 전에 [다시 동기화](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), 또는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 에 대 한 메서드는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체는 [열](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드를 한 **연결** , 개체 또는 설정는 [필터](../../../ado/reference/ado-api/filter-property.md) 속성에는 **레코드 집합** 개체를 호출 하는 **의선택을취소**에서 메서드는 **오류** 컬렉션입니다. 이런 방식으로 읽을 수는 [개수](../../../ado/reference/ado-api/count-property-ado.md) 속성은 **오류** 테스트할 컬렉션을 경고를 반환 합니다.  
  
> [!NOTE]
>  참조는 **오류** 단일 ADO 작업 오류가 여러 개 생성 되는 방식에 대 한 자세한 설명은 대 한 개체 항목.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [오류 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/errors-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)

