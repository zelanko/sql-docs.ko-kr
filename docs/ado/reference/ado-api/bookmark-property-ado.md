---
description: Bookmark 속성(ADO)
title: Bookmark 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Bookmark
helpviewer_keywords:
- Bookmark property [ADO]
ms.assetid: 481dcc93-487b-490e-ac58-a1e9b2ebfd43
author: rothja
ms.author: jroth
ms.openlocfilehash: b3ab83bb44bca7598074eb81d832ca9ed9b954d2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451115"
---
# <a name="bookmark-property-ado"></a>Bookmark 속성(ADO)
[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 현재 레코드를 고유 하 게 식별 하거나 **레코드 집합** 개체의 현재 레코드를 유효한 책갈피로 식별 되는 레코드로 설정 하는 책갈피를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 유효한 책갈피로 계산 되는 **Variant** 식을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **책갈피** 속성을 사용 하 여 현재 레코드의 위치를 저장 하 고 언제 든 지 해당 레코드로 돌아갈 수 있습니다. 책갈피는 책갈피 기능을 지 원하는 **레코드 집합** 개체 에서만 사용할 수 있습니다.  
  
 **레코드 집합** 개체를 열면 각 레코드에 고유한 책갈피가 있습니다. 현재 레코드에 대 한 책갈피를 저장 하려면 **책갈피** 속성의 값을 변수에 할당 합니다. 다른 레코드로 이동한 후 언제 든 지 해당 레코드로 빠르게 돌아오려면 **레코드 집합** 개체의 **책갈피** 속성을 해당 변수 값으로 설정 합니다.  
  
 사용자가 책갈피의 값을 볼 수 없습니다. 또한 같은 레코드를 참조 하는 두 책갈피의 값이 서로 다를 수 있으므로 사용자가 책갈피를 직접 비교할 수 있어야 합니다.  
  
 [Clone](../../../ado/reference/ado-api/clone-method-ado.md) 메서드를 사용 하 여 **레코드 집합** 개체의 복사본을 만드는 경우 원본 및 중복 **레코드 집합** 개체에 대 한 **책갈피** 속성 설정은 동일 하 고 서로 바꿔 사용할 수 있습니다. 그러나 서로 다른 **레코드 집합** 개체의 책갈피는 동일한 원본이 나 명령에서 생성 된 경우에도 사용할 수 없습니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽 **레코드 집합** 개체에서 사용 하는 경우 **책갈피** 속성을 항상 사용할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [BOF, EOF 및 Bookmark 속성 예제 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF, EOF 및 Bookmark 속성 예제 (VC + +)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Supports 메서드](../../../ado/reference/ado-api/supports-method.md)
