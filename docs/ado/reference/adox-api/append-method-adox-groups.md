---
description: Append 메서드(ADOX 그룹)
title: Append 메서드 (ADOX Groups) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups::raw_Append
- Groups::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 56b94fc6-7ef0-4e4a-82a3-033b94c46036
author: rothja
ms.author: jroth
ms.openlocfilehash: 5890ffa77884927574f10edeb0d2acc3a428185e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985494"
---
# <a name="append-method-adox-groups"></a>Append 메서드(ADOX 그룹)
[그룹](./groups-collection-adox.md) 컬렉션에 새 [그룹](./group-object-adox.md) 개체를 추가 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>매개 변수  
 *그룹*  
 추가할 **그룹** 개체 또는 만들고 추가할 그룹의 이름입니다.  
  
## <a name="remarks"></a>설명  
 [카탈로그](./catalog-object-adox.md) 의 **Groups** 컬렉션은 모든 카탈로그 그룹 계정을 나타냅니다. [사용자](./user-object-adox.md) 에 대 한 **그룹** 컬렉션은 사용자가 속한 그룹만 나타냅니다.  
  
 공급자가 그룹 만들기를 지원 하지 않는 경우 오류가 발생 합니다.  
  
> [!NOTE]
>  **그룹** 개체를 **사용자** 개체의 **groups** 컬렉션에 추가 하기 전에 추가 될 그룹과 동일한 [이름의](./name-property-adox.md) **그룹** 개체가 **카탈로그**의 **groups** 컬렉션에 이미 존재 해야 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Groups 컬렉션(ADOX)](./groups-collection-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [Groups 및 Users Append, ChangePassword 메서드 예제 (VB)](./groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 메서드 (ADOX Columns)](./append-method-adox-columns.md)   
 [Append 메서드 (ADOX 인덱스)](./append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](./append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](./append-method-adox-procedures.md)   
 [Append 메서드 (ADOX Tables)](./append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](./append-method-adox-users.md)   
 [Append 메서드(ADOX 보기)](./append-method-adox-views.md)