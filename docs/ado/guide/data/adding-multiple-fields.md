---
title: 여러 필드를 추가 합니다. | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], adding multiple fields
- editing data [ADO], AddNew method
ms.assetid: f3648ef4-9f36-4991-a868-83a617389844
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 90904154f324a86088fac0d637301193464feb2c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701237"
---
# <a name="adding-multiple-fields-and-values"></a>여러 필드 및 값 추가
경우에 따라 필드 및 해당 값에 배열을 전달할 더 효율적일 수 있습니다는 **AddNew** 설정이 아닌 메서드인 **값** 각 새 필드에 대해 여러 번. 경우 *FieldList* 배열이 *값* 배열 해야과 동일한 멤버의 수 고, 그렇지 않으면 오류가 발생 합니다. 필드 이름의 순서는 각 배열에 있는 필드 값의 순서가 일치 해야 합니다. 다음 코드는 필드의 배열 및 값의 배열을 전달 합니다 **AddNew** 메서드.

```
'BeginAddNew2
    Dim avarFldNames As Variant
    Dim avarFldValues As Variant

    avarFldNames = Array("CompanyName", "Phone")
    avarFldValues = Array("Sample Shipper 2", "(931) 555-6334")

    If objRs1.Supports(adAddNew) Then
        objRs1.AddNew avarFldNames, avarFldValues
    End If

    'Re-establish a Connection and update
    Set objRs1.ActiveConnection = GetNewConnection
    objRs1.UpdateBatch
'EndAddNew2
```
