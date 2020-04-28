---
title: Append 메서드 (ADOX 사용자) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Users::raw_Append
- Users::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: b80bc5d5-78ca-4f75-956b-2ac658029cc7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 99a21cd5dd32af9e84877865cfe7c0fc92f6c087
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967221"
---
# <a name="append-method-adox-users"></a>Append 메서드(ADOX 사용자)
[사용자](../../../ado/reference/adox-api/users-collection-adox.md) 컬렉션에 새 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 개체를 추가 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *사용자*  
 추가할 **사용자** 개체 또는 만들고 추가할 사용자의 이름을 포함 하는 **Variant** 값입니다.  
  
 *암호*  
 (선택 사항) 사용자에 대 한 암호를 포함 하는 **문자열** 값입니다. *Password* 매개 변수는 **사용자** 개체의 [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) 메서드에 지정 된 값에 해당 합니다.  
  
## <a name="remarks"></a>설명  
 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 의 **사용자** 컬렉션은 모든 카탈로그의 사용자를 나타냅니다. [그룹](../../../ado/reference/adox-api/group-object-adox.md) 에 대 한 **사용자** 컬렉션은 특정 그룹의 멤버 자격이 있는 사용자만 나타냅니다.  
  
 공급자가 사용자 만들기를 지원 하지 않는 경우 오류가 발생 합니다.  
  
> [!NOTE]
>  **Group** 개체의 **사용자 컬렉션에** **사용자** 개체를 추가 하기 전에 추가 될 [이름과](../../../ado/reference/adox-api/name-property-adox.md) 같은 **사용자** 개체가 **카탈로그**의 **사용자** 컬렉션에 이미 존재 해야 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Users 컬렉션(ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [Groups 및 Users Append, ChangePassword 메서드 예제 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 메서드 (ADOX Columns)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 메서드 (ADOX Groups)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 메서드 (ADOX 인덱스)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 메서드 (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드(ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
