---
title: AddNew를 사용 하 여 레코드를 추가 합니다. | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0be4014809500c4d83b2019dc16bd083b8ed6452
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701196"
---
# <a name="adding-records-using-addnew-method"></a>AddNew 메서드를 사용 하 여 레코드를 추가 합니다.
기본 구문은 합니다 **AddNew** 메서드:

 *레코드 집합*합니다. AddNew *FieldList*, *값*

 합니다 *FieldList* 하 고 *값* 인수는 선택 사항입니다. *FieldList* 는 단일 이름 또는 이름의 배열을 새 레코드에서 필드의 서 수 위치입니다.

 합니다 *값* 인수가 단일 값 또는 새 레코드의 필드 값의 배열입니다.

 일반적으로 단일 레코드를 추가 하려는 경우 호출 된 **AddNew** 메서드 인수 없이 합니다. 특히 호출 **AddNew**; set 합니다 **값** 각 필드에 새 레코드; 및 호출 **업데이트** 또는 **UpdateBatch**, 또는 둘 다. 있는지 확인할 수 있습니다는 프로그램 **레코드 집합** 를 사용 하 여 새 레코드를 추가 하 여 지원를 **지원** 속성을를 **adAddNew** 열거형된 상수입니다.

 다음 코드 예제를 새 운송 업체를 추가 하려면이 기법을 사용 하며 **레코드 집합**합니다. SQL Server ShipperID 필드 값을 자동으로 제공 합니다. 따라서 코드를 새 레코드에 대 한 필드 값을 제공 하지 않습니다.

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

## <a name="remarks"></a>Remarks
 이 코드는 연결이 끊긴 사용 하므로 **Recordset** 다시 연결 해야 일괄 처리 모드에서 클라이언트 쪽 커서를 **레코드 집합** 를 새 데이터 원본에 **연결** 호출 하기 전에 개체를 **UpdateBatch** 변경 내용이 데이터베이스에 게시 하는 방법입니다. 새 함수를 사용 하 여 쉽게 이렇게 **GetNewConnection**합니다.
