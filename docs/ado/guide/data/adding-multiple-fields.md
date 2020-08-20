---
description: 여러 필드 및 값 추가
title: 여러 필드 추가 | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e2543741749c1521526aea18bc4600168559eb45
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453895"
---
# <a name="adding-multiple-fields-and-values"></a>여러 필드 및 값 추가
경우에 따라 각 새 필드에 대 한 **값** 을 여러 번 설정 하지 않고 필드 배열과 해당 값을 **AddNew** 메서드에 전달 하는 것이 더 효율적일 수 있습니다. *Fieldlist)* 가 배열인 경우 *값* 도 멤버 수가 같은 배열 이어야 합니다. 그렇지 않으면 오류가 발생 합니다. 필드 이름의 순서는 각 배열에서 필드 값의 순서와 일치 해야 합니다. 다음 코드는 필드의 배열과 값의 배열을 **AddNew** 메서드에 전달 합니다.

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
