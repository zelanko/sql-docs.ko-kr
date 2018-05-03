---
title: AddNew를 사용 하 여 레코드를 추가 합니다. | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: cab4adff-f22f-4fb1-9217-f8138c795268
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 12645f89fe08e36c024924b5580e4386cb471ee7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="adding-records-using-addnew-method"></a>AddNew 메서드를 사용 하 여 레코드를 추가 합니다.
기본 구문은 **AddNew** 메서드:

 *레코드 집합*합니다. AddNew *FieldList*, *값*

 *FieldList* 및 *값* 인수는 선택 사항입니다. *FieldList* 단일 이름 이거나 새 레코드의 필드의 서 수 위치 또는 이름 배열입니다.

 *값* 인수는 단일 값 또는 새 레코드의 필드에 대 한 값의 배열입니다.

 일반적으로 단일 레코드를 추가 하려는 경우를 호출 합니다는 **AddNew** 인수 없이 메서드. 호출 하 게 특히 **AddNew**설정;는 **값** 각각의 새 레코드; 필드를 한 다음 호출 **업데이트** 또는 **UpdateBatch**, 또는 둘 다 합니다. 있습니다 수 있는지 확인 하 여 **레코드 집합** 를 사용 하 여 새 레코드를 추가 하 여 지원는 **지원** 속성을는 **adAddNew** 열거형된 상수입니다.

 다음 코드를 새 운송 업체로 샘플에 추가 하려면이 기술을 사용 **레코드 집합**합니다. SQL Server에서 자동으로 ShipperID 필드 값을 제공 합니다. 따라서 코드는 새 레코드에 대 한 필드 값을 제공 하는 시도 하지 않습니다.

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

## <a name="remarks"></a>주의
 이 코드를 사용 하 여 연결이 끊긴 때문에 **레코드 집합** 다시 연결 해야 일괄 처리 모드에서 클라이언트 쪽 커서를 **레코드 집합** 를 새 데이터 원본에 **연결** 호출 하기 전에 개체는 **UpdateBatch** 메서드 변경 내용을 데이터베이스에 게시할 수 있습니다. 새 함수를 사용 하 여 쉽게 이렇게 **GetNewConnection**합니다.
