---
description: Type 속성(열)(ADOX)
title: Type 속성 (Column) (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::Type
- _Column::GetType
- _Column::get_Type
- _Column::put_Type
- _Column::PutType
helpviewer_keywords:
- Type property [ADOX]
ms.assetid: 5c6718b6-f728-478a-8afb-5d17b0a91d1f
author: rothja
ms.author: jroth
ms.openlocfilehash: dffb08de42e3c38a9c0a28e8cad33af95f0d8926
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983174"
---
# <a name="type-property-column-adox"></a>Type 속성(열)(ADOX)
열의 데이터 형식을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 [DataTypeEnum](../ado-api/datatypeenum.md) 상수 중 하나일 수 있는 **Long** 값을 설정 하거나 반환 합니다. 기본값은 **adVarWChar**입니다.  
  
## <a name="remarks"></a>설명  
 이 속성은 [열](./column-object-adox.md) 개체가 컬렉션 또는 다른 개체에 추가 될 때까지 읽기/쓰기가 가능한 후 읽기 전용입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [열 개체(ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [ParentCatalog 속성 예제 (VB)](./parentcatalog-property-example-vb.md)   
 [Type 속성 (Key) (ADOX)](./type-property-key-adox.md)   
 [Type 속성(테이블)(ADOX)](./type-property-table-adox.md)