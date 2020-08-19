---
description: ParentCatalog 속성(ADOX)
title: ParentCatalog 속성 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User::get_ParentCatalog
- _Column::ParentCatalog
- _Table::put_ParentCatalog
- _Group::put_ParentCatalog
- _Column::get_ParentCatalog
- _Table::PutParentCatalog
- _Group::putref_ParentCatalog
- _Group::ParentCatalog
- _Column::PutParentCatalog
- _Column::put_ParentCatalog
- _Group::get_ParentCatalog
- _User::put_ParentCatalog
- _User::putref_ParentCatalog
- _Table::get_ParentCatalog
- _Group::PutParentCatalog
- _Table::ParentCatalog
- _Column::GetParentCatalog
- _Table::PutRefParentCatalog
- _User::GetParentCatalog
- _Table::GetParentCatalog
- _Table::putref_ParentCatalog
- _User::PutParentCatalog
- _User::ParentCatalog
- _User::PutRefParentCatalog
- _Group::GetParentCatalog
- _Group::PutRefParentCatalog
helpviewer_keywords:
- ParentCatalog property [ADOX]
ms.assetid: a0bb2ed8-d4cb-4f92-8de7-769bbe0e6273
author: rothja
ms.author: jroth
ms.openlocfilehash: 93d15cdac3d8f7a47c74a783d176d806271f68a3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439725"
---
# <a name="parentcatalog-property-adox"></a>ParentCatalog 속성(ADOX)
공급자별 속성에 대 한 액세스를 제공 하기 위해 테이블, 사용자 또는 열 개체의 부모 카탈로그를 지정 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 개체를 설정 하 고 반환 합니다. **ParentCatalog** 을 열려 있는 **카탈로그로** 설정 하면 테이블이 나 열을 **카탈로그** 컬렉션에 추가 하기 전에 공급자별 속성에 액세스할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 일부 데이터 공급자는 생성 시, 즉 테이블이 나 열이 **카탈로그** 컬렉션에 추가 되는 경우에만 공급자별 속성 값을 쓸 수 있습니다. 이러한 개체를 **카탈로그**에 추가 하기 전에 이러한 속성에 액세스 하려면 먼저 **ParentCatalog** 속성에서 **카탈로그** 를 지정 합니다.  
  
 테이블이 나 열이 **ParentCatalog**아닌 다른 **카탈로그** 에 추가 되 면 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [Column 개체(ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
    :::column-end:::
    :::column:::
        [Table 개체(ADOX)](../../../ado/reference/adox-api/table-object-adox.md)  
    :::column-end:::
    :::column:::
        [User 개체(ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [ParentCatalog 속성 예제(VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
