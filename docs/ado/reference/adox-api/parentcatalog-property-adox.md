---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10d6715a19212c87ece9c890ee99516571713d4f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62710339"
---
# <a name="parentcatalog-property-adox"></a>ParentCatalog 속성(ADOX)
공급자별 속성에 대 한 액세스를 제공 하는 테이블, 사용자 또는 열 개체의 부모 카탈로그를 지정 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하 고 반환 된 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 개체입니다. 설정 **ParentCatalog** 열린 **카탈로그** 테이블 또는 열을 추가 하기 전에 공급자별 속성에 액세스할 수는 **카탈로그** 컬렉션입니다.  
  
## <a name="remarks"></a>Remarks  
 일부 데이터 공급자는 공급자별 속성 값을 만들 때만 기록 허용: 테이블 또는 열에 추가 되 면에, 해당 **카탈로그** 컬렉션입니다. 이러한 개체를 추가 하기 전에 이러한 속성에 액세스 하는 **카탈로그**를 지정 합니다 **카탈로그** 에서 **ParentCatalog** 속성 첫 번째.  
  
 오류가 발생할 때 다른 테이블 또는 열을 추가할 때 **카탈로그** 보다는 **ParentCatalog**합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Column 개체(ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Table 개체(ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|  
|[User 개체(ADOX)](../../../ado/reference/adox-api/user-object-adox.md)||  
  
## <a name="see-also"></a>관련 항목  
 [ParentCatalog 속성 예제(VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
