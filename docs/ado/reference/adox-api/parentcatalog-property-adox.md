---
title: "ParentCatalog 속성 (ADOX) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f5229c37299494ca2b3b31e3ca3e0d091c93d96a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="parentcatalog-property-adox"></a>ParentCatalog 속성 (ADOX)
공급자별 속성에 대 한 액세스를 제공 하는 테이블, 사용자 또는 열 개체의 부모 카탈로그를 지정 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하 고 반환 된 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 개체입니다. 설정 **ParentCatalog** 열린 **카탈로그** 테이블이 나 열을 추가 하기 전에 공급자별 속성에 액세스할 수 있습니다는 **카탈로그** 컬렉션입니다.  
  
## <a name="remarks"></a>주의  
 일부 데이터 공급자는 공급자별 속성 값을 만들 때만 쓰도록 허용: 테이블 또는 열에 추가 됩니다 때에 즉, 해당 **카탈로그** 컬렉션입니다. 이러한 개체를 추가 하기 전에 이러한 속성에 액세스 하는 **카탈로그**, 지정 된 **카탈로그** 에 **ParentCatalog** 속성 첫 번째 합니다.  
  
 오류가 발생할 때 다른 테이블이 나 열을 추가할 때 **카탈로그** 보다는 **ParentCatalog**합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Column 개체(ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Table 개체(ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|  
|[User 개체(ADOX)](../../../ado/reference/adox-api/user-object-adox.md)||  
  
## <a name="see-also"></a>관련 항목:  
 [ParentCatalog 속성 예제(VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)

