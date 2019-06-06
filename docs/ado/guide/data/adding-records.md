---
title: 레코드 추가 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- editing data [ADO], AddNew method
- editing data [ADO], adding data
ms.assetid: dd34669e-6f06-403b-9241-1c85c82aecc2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 87d8358344d75cd6995d43d081abbec7aeaabe1c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701052"
---
# <a name="adding-records-to-a-recordset"></a>레코드 집합에 레코드를 추가합니다.
사용 된 **AddNew** 메서드를 만들고 기존에서 새 레코드를 초기화할 **레코드 집합**합니다. 사용할 수는 **지원** 메서드를 **CursorOptionEnum** 의 값 **adAddNew** 현재 레코드를 추가할 수 있는지 여부를 확인 하려면 **레코드집합** 개체입니다.

 호출한 후 합니다 **AddNew** 메서드 새 레코드를 현재 레코드가 호출한 후에 현재 상태로 유지 됩니다 합니다 **업데이트** 메서드. 경우는 **레코드 집합** 개체가 책갈피를 지원 하지 않습니다, 다른 레코드로 이동 되 면 새 레코드에 액세스할 수 있습니다. 따라서 커서 유형에 따라 수 호출 해야 합니다 **Requery** 새 레코드에 액세스할 수 있도록 하는 방법입니다.

 호출 하는 경우 **AddNew** ADO를 호출 하는 현재 레코드를 편집 하는 동안 또는 새 레코드를 추가 하는 동안 합니다 **업데이트** 메서드 하나를 변경 하 고 새 레코드를 만듭니다.

 이 섹션에서는 다음 항목을 다룹니다.

-   [AddNew를 사용하여 레코드 추가](../../../ado/guide/data/adding-records-using-addnew.md)

-   [다중 필드 추가](../../../ado/guide/data/adding-multiple-fields.md)

-   [편집 모드 확인](../../../ado/guide/data/determining-edit-mode.md)

-   [직접 실행 및 일괄 처리 모드에서 AddNew 사용](../../../ado/guide/data/using-addnew-in-immediate-and-batch-modes.md)
