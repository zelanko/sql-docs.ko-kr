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
manager: craigg
ms.openlocfilehash: e56391357e7a11c47efdf0ffaf3c9ae9704d5db3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787212"
---
# <a name="append-method-adox-users"></a>Append 메서드(ADOX 사용자)
새로 추가 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 개체를 [사용자](../../../ado/reference/adox-api/users-collection-adox.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *사용자*  
 **Variant** 포함 하는 값을 **사용자** 추가할 개체 또는 만들고 추가 하는 사용자의 이름입니다.  
  
 *암호*  
 (선택 사항) A **문자열** 사용자 암호를 포함 하는 값입니다. *암호* 매개 변수에서 지정한 값에 해당 합니다 [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) 메서드를 **사용자** 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **사용자** 의 컬렉션을 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 카탈로그의 모든 사용자를 나타냅니다. 합니다 **사용자** 에 대 한 컬렉션을 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 특정 그룹의 멤버 자격이 있는 사용자만을 나타냅니다.  
  
 공급자를 만드는 사용자를 지원 하지 않는 경우 오류가 발생 합니다.  
  
> [!NOTE]
>  추가 하기 전에 **사용자** 개체를 **사용자** 의 컬렉션을 **그룹** 개체를 **사용자** 개체와 같은 [이름 ](../../../ado/reference/adox-api/name-property-adox.md) 추가할 것에 이미 존재 해야 합니다는 **사용자** 컬렉션을 **카탈로그**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Users 컬렉션(ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>관련 항목  
 [Groups 및 Users Append, ChangePassword 메서드 예제 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 메서드 (ADOX 열)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 메서드 (ADOX 그룹)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 메서드 (ADOX 인덱스)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 메서드 (ADOX 테이블)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드(ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
