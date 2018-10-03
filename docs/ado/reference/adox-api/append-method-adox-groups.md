---
title: Append 메서드 (ADOX 그룹) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 171aaa250930d5563d8ce6ec3b08b5939710b881
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742531"
---
# <a name="append-method-adox-groups"></a>Append 메서드(ADOX 그룹)
새로 추가 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 개체를 [그룹](../../../ado/reference/adox-api/groups-collection-adox.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>매개 변수  
 *그룹*  
 합니다 **그룹** 만들고 추가 하는 그룹의 이름 또는 추가할 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **그룹** 의 컬렉션을 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 모든 카탈로그의 그룹 계정을 나타냅니다. 합니다 **그룹** 에 대 한 컬렉션을 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 사용자가 속한 그룹에만 나타냅니다.  
  
 공급자 그룹 만들기를 지원 하지 않는 경우 오류가 발생 합니다.  
  
> [!NOTE]
>  추가 하기 전에 **그룹** 개체를 **그룹** 의 컬렉션을 **사용자** 개체를 **그룹** 개체와 같은 [ 이름](../../../ado/reference/adox-api/name-property-adox.md) 추가할 것에 이미 존재 해야 합니다는 **그룹** 컬렉션을 **카탈로그**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Groups 컬렉션(ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>관련 항목  
 [Groups 및 Users Append, ChangePassword 메서드 예제 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 메서드 (ADOX 열)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 메서드 (ADOX 인덱스)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 메서드 (ADOX 테이블)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 메서드(ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
