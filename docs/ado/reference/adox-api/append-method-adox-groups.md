---
title: Append 메서드 (ADOX Groups) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8281b8b480289dca2b4976cea61a6d6838fa2779
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967310"
---
# <a name="append-method-adox-groups"></a>Append 메서드(ADOX 그룹)
[그룹](../../../ado/reference/adox-api/groups-collection-adox.md) 컬렉션에 새 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 개체를 추가 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>매개 변수  
 *그룹*  
 추가할 **그룹** 개체 또는 만들고 추가할 그룹의 이름입니다.  
  
## <a name="remarks"></a>설명  
 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 의 **Groups** 컬렉션은 모든 카탈로그 그룹 계정을 나타냅니다. [사용자](../../../ado/reference/adox-api/user-object-adox.md) 에 대 한 **그룹** 컬렉션은 사용자가 속한 그룹만 나타냅니다.  
  
 공급자가 그룹 만들기를 지원 하지 않는 경우 오류가 발생 합니다.  
  
> [!NOTE]
>  **그룹** 개체를 **사용자** 개체의 **groups** 컬렉션에 추가 하기 전에 추가 될 그룹과 동일한 [이름의](../../../ado/reference/adox-api/name-property-adox.md) **그룹** 개체가 **카탈로그**의 **groups** 컬렉션에 이미 존재 해야 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Groups 컬렉션(ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [Groups 및 Users Append, ChangePassword 메서드 예제 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 메서드 (ADOX Columns)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 메서드 (ADOX 인덱스)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 메서드 (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 메서드(ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
