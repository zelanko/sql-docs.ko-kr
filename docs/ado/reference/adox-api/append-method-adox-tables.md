---
description: Append 메서드(ADOX 테이블)
title: Append 메서드 (ADOX Tables) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Tables::Append
- Tables::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: a362ed51-314c-4783-9598-538dbf755f3d
author: rothja
ms.author: jroth
ms.openlocfilehash: ffd2ef32cae3fafb7179568d1342606d32236657
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985474"
---
# <a name="append-method-adox-tables"></a>Append 메서드(ADOX 테이블)
[Tables](./tables-collection-adox.md) 컬렉션에 새 [Table](./table-object-adox.md) 개체를 추가 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Tables.Append Table  
```  
  
#### <a name="parameters"></a>매개 변수  
 *테이블*  
 추가할 **테이블** 에 대 한 참조 또는 만들고 추가할 테이블의 이름을 포함 하는 **Variant** 값입니다.  
  
## <a name="remarks"></a>설명  
 공급자가 테이블 생성을 지원 하지 않으면 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Tables 컬렉션(ADOX)](./tables-collection-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [Columns 및 Tables Append 메서드, Name 속성 예제 (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](./parentcatalog-property-example-vb.md)   
 [Append 메서드 (ADOX Columns)](./append-method-adox-columns.md)   
 [Append 메서드 (ADOX Groups)](./append-method-adox-groups.md)   
 [Append 메서드 (ADOX 인덱스)](./append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](./append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](./append-method-adox-procedures.md)   
 [Append 메서드 (ADOX 사용자)](./append-method-adox-users.md)   
 [Append 메서드(ADOX 보기)](./append-method-adox-views.md)