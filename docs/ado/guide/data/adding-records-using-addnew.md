---
description: AddNew 메서드를 사용 하 여 레코드 추가
title: AddNew를 사용 하 여 레코드 추가 | Microsoft Docs
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
- editing data [ADO], AddNew method
ms.assetid: cab4adff-f22f-4fb1-9217-f8138c795268
author: rothja
ms.author: jroth
ms.openlocfilehash: 27b42b9d65a4c00d4786ed900ad35ce00ef4b8f1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453875"
---
# <a name="adding-records-using-addnew-method"></a>AddNew 메서드를 사용 하 여 레코드 추가
다음은 **AddNew** 메서드의 기본 구문입니다.

 *레코드 집합*. AddNew *fieldlist)*, *Values*

 *Fieldlist)* 및 *Values* 인수는 선택 사항입니다. *Fieldlist)* 은 단일 이름 이거나 새 레코드에 있는 필드의 이름 또는 서 수 위치 배열입니다.

 *Values* 인수는 단일 값 이거나 새 레코드의 필드에 대 한 값의 배열입니다.

 일반적으로 단일 레코드를 추가 하려는 경우에는 인수 없이 **AddNew** 메서드를 호출 합니다. 특히 **AddNew**를 호출 합니다. 새 레코드의 각 필드 **값** 을 설정 합니다. 그런 다음 **Update** , **UpdateBatch**또는 both를 호출 합니다. **지원** 속성을 **adaddnew** 열거 상수와 함께 사용 하 여 **레코드 집합** 에서 새 레코드를 추가 하도록 지원 하는지 확인할 수 있습니다.

 다음 코드에서는이 기술을 사용 하 여 샘플 **레코드 집합**에 새 전달자를 추가 합니다. SQL Server은로 자동으로 제공 됩니다. 따라서 코드는 새 레코드에 대 한 필드 값을 제공 하지 않습니다.

```
'BeginAddNew1.1
If objRs.Supports(adAddNew) Then
    With objRs
        .AddNew
        .Fields("CompanyName") = "Sample Shipper"
        .Fields("Phone") = "(931) 555-6334"
        .Update
    End With
End If
'EndAddNew1.1
```

## <a name="remarks"></a>설명
 이 코드는 일괄 처리 모드에서 클라이언트 쪽 커서에 연결 되지 않은 **레코드 집합** 을 사용 하기 때문에 데이터베이스에 변경 내용을 게시 하기 위해 **UpdateBatch** 메서드를 호출 하려면 먼저 새 **연결** 개체를 사용 하 여 **레코드 집합** 을 데이터 원본에 다시 연결 해야 합니다. 새 함수 **Getnewconnection**을 사용 하 여이 작업을 쉽게 수행할 수 있습니다.
