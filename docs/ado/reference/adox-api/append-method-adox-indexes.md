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
ms.openlocfilehash: ef30faf0fef05c4e86ffb4d2c21781592094c198
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967307"
---
# <a name="append-method-adox-indexes"></a>Append 메서드(ADOX 인덱스)
[인덱스](../../../ado/reference/adox-api/indexes-collection-adox.md) 컬렉션에 새 [인덱스](../../../ado/reference/adox-api/index-object-adox.md) 개체를 추가 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *인덱싱할*  
 추가할 **인덱스** 개체 또는 만들고 추가할 인덱스의 이름입니다.  
  
 *열*  
 (선택 사항) 인덱싱할 열의 이름을 지정 하는 Variant 값입니다 ( **Variant** ). *Columns* 매개 변수는 [열](../../../ado/reference/adox-api/column-object-adox.md) 개체의 [Name](../../../ado/reference/adox-api/name-property-adox.md) 속성 값에 해당 합니다.  
  
## <a name="remarks"></a>설명  
 *Columns* 매개 변수는 열 이름 또는 열 이름 배열을 사용할 수 있습니다.  
  
 공급자가 인덱스 생성을 지원 하지 않는 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Indexes 컬렉션(ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [Indexes Append 메서드 예제 (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Append 메서드 (ADOX Columns)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 메서드 (ADOX Groups)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 메서드 (ADOX 키)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 메서드 (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 메서드(ADOX 보기)](../../../ado/reference/adox-api/append-method-adox-views.md)
