---
title: "Append 메서드 (ADOX 사용자) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Users::raw_Append
- Users::Append
helpviewer_keywords: Append method [ADOX]
ms.assetid: b80bc5d5-78ca-4f75-956b-2ac658029cc7
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 69f839a24ee99d0db10435a3562926786f2d4620
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="append-method-adox-users"></a>Append 메서드 (ADOX 사용자)
새로 추가 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 개체는 [사용자](../../../ado/reference/adox-api/users-collection-adox.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *사용자*  
 A **Variant** 포함 된 값은 **사용자** 추가할 개체 또는 만들고 추가 하는 사용자의 이름입니다.  
  
 *암호*  
 (선택 사항) A **문자열** 사용자에 대 한 암호를 포함 하는 값입니다. *암호* 에 지정 된 값에 해당 하는 매개 변수는 [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) 의 메서드는 **사용자** 개체입니다.  
  
## <a name="remarks"></a>주의  
 **사용자** 의 컬렉션을 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 카탈로그의 모든 사용자를 나타냅니다. **사용자** 에 대 한 컬렉션은 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 특정 그룹에는 구성원 자격이 있는 사용자만 나타냅니다.  
  
 공급자 사용자 만들기를 지원 하지 않는 경우 오류가 발생 합니다.  
  
> [!NOTE]
>  추가 하기 전에 **사용자** 개체는 **사용자** 의 컬렉션은 **그룹** 개체는 **사용자** 개체와 같은 [이름 ](../../../ado/reference/adox-api/name-property-adox.md) 추가할 하나에 이미 있어야 하는 대로 **사용자** 의 컬렉션은 **카탈로그**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Users 컬렉션(ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>관련 항목:  
 [그룹 및 사용자 추가, ChangePassword 메서드 예제 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 메서드 (ADOX 열)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 메서드 (ADOX 그룹)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 메서드 (ADOX 인덱스)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 메서드 (ADOX 테이블)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드(ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
