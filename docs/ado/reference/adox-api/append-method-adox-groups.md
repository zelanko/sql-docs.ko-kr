---
title: "Append 메서드 (ADOX 그룹) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Groups::raw_Append
- Groups::Append
helpviewer_keywords: Append method [ADOX]
ms.assetid: 56b94fc6-7ef0-4e4a-82a3-033b94c46036
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b88abda8492902df0c050cad085e758bf6562fca
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="append-method-adox-groups"></a>Append 메서드 (ADOX 그룹)
새로 추가 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 개체는 [그룹](../../../ado/reference/adox-api/groups-collection-adox.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>매개 변수  
 *그룹*  
 **그룹** 추가할 개체 또는 그룹을 만든 추가의 이름입니다.  
  
## <a name="remarks"></a>주의  
 **그룹** 의 컬렉션을 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 모든 카탈로그의 그룹 계정을 나타냅니다. **그룹** 에 대 한 컬렉션은 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 유일한 사용자가 속한 그룹을 나타냅니다.  
  
 공급자는 그룹 만들기를 지원 하지 않는 경우 오류가 발생 합니다.  
  
> [!NOTE]
>  추가 하기 전에 **그룹** 개체는 **그룹** 의 컬렉션은 **사용자** 개체는 **그룹** 개체와 같은 [ 이름](../../../ado/reference/adox-api/name-property-adox.md) 추가할 하나에 이미 있어야 하는 대로 **그룹** 의 컬렉션은 **카탈로그**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Groups 컬렉션(ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>관련 항목:  
 [그룹 및 사용자 추가, ChangePassword 메서드 예제 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 메서드 (ADOX 열)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 메서드 (ADOX 인덱스)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 메서드 (ADOX 테이블)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 메서드(ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
