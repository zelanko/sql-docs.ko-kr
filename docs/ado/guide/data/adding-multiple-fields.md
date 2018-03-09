---
title: "여러 필드를 추가 합니다. | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], adding multiple fields
- editing data [ADO], AddNew method
ms.assetid: f3648ef4-9f36-4991-a868-83a617389844
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d9eac6c90c0605b157dcd83c1b23f34969f3f73c
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="adding-multiple-fields-and-values"></a>여러 필드 및 값 추가
때때로 필드와 해당 값을 배열에 전달 하는 것 수 있습니다는 **AddNew** 설정이 아닌 메서드를 **값** 각 새 필드에 대해 여러 번입니다. 경우 *FieldList* 배열 *값* 배열을 수도 있어야 같은 멤버의 숫자, 그렇지 않으면 오류가 발생 합니다. 필드 이름은 순서에는 각 배열에 있는 필드 값의 순서와 일치 해야 합니다. 다음 코드는 필드의 배열 및 값의 배열을 전달는 **AddNew** 메서드.

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
