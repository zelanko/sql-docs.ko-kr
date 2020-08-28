---
description: Errors 컬렉션(ADO)
title: Errors 컬렉션 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3606827f95330bf75915463bba8225bccdc62cd7
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973624"
---
# <a name="errors-collection-ado"></a>Errors 컬렉션(ADO)
단일 공급자 관련 오류에 대 한 응답으로 생성 된 모든 [오류](../../../ado/reference/ado-api/error-object.md) 개체를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 ADO 개체와 관련 된 모든 작업은 하나 이상의 공급자 오류를 생성할 수 있습니다. 각 오류가 발생 하면 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 **Errors** 컬렉션에 하나 이상의 **오류** 개체를 배치할 수 있습니다. 다른 ADO 작업에서 오류를 생성 하는 경우 **errors** 컬렉션이 지워지고 새 **오류** 개체 집합을 **errors** 컬렉션에 배치할 수 있습니다.  
  
 각 **Error** 개체는 ADO 오류가 아닌 특정 공급자 오류를 나타냅니다. ADO 오류는 런타임 예외 처리 메커니즘에 노출 됩니다. 예를 들어 Microsoft Visual Basic에서 ADO 관련 오류가 발생 하면 [onError](../../../ado/reference/rds-api/onerror-event-rds.md) 이벤트가 트리거되고 **Err** 개체에 표시 됩니다.  
  
 오류를 생성 하지 않는 ADO 작업은 **Errors** 컬렉션에 영향을 주지 않습니다. [Clear](../../../ado/reference/ado-api/clear-method-ado.md) 메서드를 사용 하 여 수동으로 **오류** 컬렉션을 지웁니다.  
  
 **Errors** 컬렉션의 **오류** 개체 집합은 단일 문에 대 한 응답으로 발생 한 모든 오류를 설명 합니다. **오류 수집의** 특정 오류를 열거 하면 오류 처리 루틴이 오류의 원인과 원인을 보다 정확 하 게 파악 하 고 적절 한 단계를 수행 하 여 복구할 수 있습니다.  
  
 일부 속성 및 **메서드는 오류 컬렉션에** **오류** 개체로 표시 되지만 프로그램의 실행을 중단 하지 않는 경고를 반환 합니다. [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체에 대해 [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)또는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드를 호출 하거나 **연결** 개체의 [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드를 호출 하거나 **레코드 집합** 개체에 대해 [Filter](../../../ado/reference/ado-api/filter-property.md) 속성을 설정 하기 전에 **Errors** 컬렉션에서 **Clear** 메서드를 호출 합니다. 이렇게 하면 **Errors** 컬렉션의 [Count](../../../ado/reference/ado-api/count-property-ado.md) 속성을 읽어 반환 된 경고를 테스트할 수 있습니다.  
  
> [!NOTE]
>  단일 ADO 작업에서 여러 오류를 생성 하는 방법에 대 한 자세한 설명은 **Error** 개체 항목을 참조 하세요.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Errors 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/errors-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
