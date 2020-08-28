---
description: Append 메서드(ADOX 인덱스)
title: Append 메서드 (ADOX 인덱스) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Indexes::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6695769f-275b-4b70-81bd-1a5f7d74926c
author: rothja
ms.author: jroth
ms.openlocfilehash: 00b37055efe15f204049d02c337b54c228468419
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985514"
---
# <a name="append-method-adox-indexes"></a>Append 메서드(ADOX 인덱스)
[인덱스](./indexes-collection-adox.md) 컬렉션에 새 [인덱스](./index-object-adox.md) 개체를 추가 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Index*  
 추가할 **인덱스** 개체 또는 만들고 추가할 인덱스의 이름입니다.  
  
 *열*  
 선택 사항입니다. 인덱싱할 열의 이름을 지정 하는 Variant 값입니다 ( **Variant** ). *Columns* 매개 변수는 [열](./column-object-adox.md) 개체의 [Name](./name-property-adox.md) 속성 값에 해당 합니다.  
  
## <a name="remarks"></a>설명  
 *Columns* 매개 변수는 열 이름 또는 열 이름 배열을 사용할 수 있습니다.  
  
 공급자가 인덱스 생성을 지원 하지 않는 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Indexes 컬렉션(ADOX)](./indexes-collection-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [Indexes Append 메서드 예제 (VB)](./indexes-append-method-example-vb.md)   
 [Append 메서드 (ADOX Columns)](./append-method-adox-columns.md)   
 [Append 메서드 (ADOX Groups)](./append-method-adox-groups.md)   
 [Append 메서드 (ADOX 키)](./append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](./append-method-adox-procedures.md)   
 [Append 메서드 (ADOX Tables)](./append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](./append-method-adox-users.md)   
 [Append 메서드(ADOX 보기)](./append-method-adox-views.md)