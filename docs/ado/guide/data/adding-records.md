---
description: 레코드 집합에 레코드 추가
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2394cf5612dab45ccd2e0f3cc6e2204b6d451142
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453885"
---
# <a name="adding-records-to-a-recordset"></a>레코드 집합에 레코드 추가
**AddNew** 메서드를 사용 하 여 기존 레코드 **집합**에 새 레코드를 만들고 초기화 합니다. **CursorOptionEnum** 값이 **Adaddnew** 인 **Supports** 메서드를 사용 하 여 현재 **레코드 집합** 개체에 레코드를 추가할 수 있는지 여부를 확인할 수 있습니다.

 **AddNew** 메서드를 호출 하면 새 레코드가 현재 레코드가 되며 **Update** 메서드를 호출한 후에는 현재 레코드가 됩니다. **레코드 집합** 개체가 책갈피를 지원 하지 않는 경우에는 다른 레코드로 이동 하는 동안 새 레코드에 액세스 하지 못할 수 있습니다. 따라서 커서 유형에 따라 **Requery** 메서드를 호출 하 여 새 레코드를 액세스할 수 있도록 해야 할 수도 있습니다.

 현재 레코드를 편집 하는 동안 **AddNew** 를 호출 하거나 새 레코드를 추가 하는 동안 ADO에서 **Update** 메서드를 호출 하 여 변경 내용을 저장 한 다음 새 레코드를 만듭니다.

 이 섹션에서는 다음 항목을 다룹니다.

-   [AddNew를 사용하여 레코드 추가](../../../ado/guide/data/adding-records-using-addnew.md)

-   [다중 필드 추가](../../../ado/guide/data/adding-multiple-fields.md)

-   [편집 모드 확인](../../../ado/guide/data/determining-edit-mode.md)

-   [직접 실행 및 일괄 처리 모드에서 AddNew 사용](../../../ado/guide/data/using-addnew-in-immediate-and-batch-modes.md)
