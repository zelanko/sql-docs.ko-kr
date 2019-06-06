---
title: Append 메서드 (ADOX 인덱스) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7190fa68b8204e6b1cfea68a6571e07fd78a9bbc
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718960"
---
# <a name="append-method-adox-indexes"></a>Append 메서드(ADOX 인덱스)
새로 추가 [인덱스](../../../ado/reference/adox-api/index-object-adox.md) 개체를 [인덱스](../../../ado/reference/adox-api/indexes-collection-adox.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Index*  
 합니다 **인덱스** 추가할 개체 또는 만들기 및 추가 인덱스의 이름입니다.  
  
 *열*  
 (선택 사항) A **Variant** 인덱싱할 열 이름을 지정 하는 값입니다. *열* 의 값에 해당 하는 매개 변수를 [이름](../../../ado/reference/adox-api/name-property-adox.md) 속성을 [열](../../../ado/reference/adox-api/column-object-adox.md) 개체 또는 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 *열* 열의 이름 또는 열 이름의 배열 매개 변수를 사용할 수 있습니다.  
  
 공급자 만들기 인덱스를 지원 하지 않는 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Indexes 컬렉션(ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>관련 항목  
 [Indexes Append 메서드 예제 (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Append 메서드 (ADOX 열)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 메서드 (ADOX 그룹)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 메서드 (ADOX 키)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 메서드 (ADOX 테이블)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 메서드(ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
