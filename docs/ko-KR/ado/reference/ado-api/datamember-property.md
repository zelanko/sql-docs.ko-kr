---
title: DataMember 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataMember
helpviewer_keywords:
- DataMember property
ms.assetid: 2c8fb09e-10ad-49b5-ab41-2603771780d9
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 53a5235fc4fc865be867811ff6144a016196979f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="datamember-property"></a>DataMember 속성
검색할 수 있는 데이터 멤버의 이름을 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 으로 참조 되는 [DataSource](../../../ado/reference/ado-api/datasource-property-ado.md) 속성입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **문자열** 값입니다. 이름은 대/소문자 구분 아닙니다.  
  
## <a name="remarks"></a>주의  
 이 속성은 데이터 환경을 사용 하 여 데이터 바인딩된 컨트롤을 만들려면 사용 합니다. 데이터 환경 컬렉션을 포함 하는 데이터 (데이터 원본)로 나타낼 수 있는 개체 (데이터 멤버) 라는 유지 관리는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
 **DataMember** 및 **DataSource** 속성을 함께 사용 되어야 합니다.  
  
 **DataMember** 속성 지정 하는 개체가 결정는 **DataSource** 속성으로 표현 되는 **레코드 집합** 개체입니다. **레코드 집합** 이 속성을 설정 하기 전에 개체를 닫아야 합니다. 오류가 발생 하는 경우는 **DataMember** 하기 전에 속성이 설정 되어 있지는 **DataSource** 속성을 또는 경우에는 **DataMember** 이름에 지정 된 개체에서 인식 되지 않습니다는 **DataSource** 속성입니다.  
  
## <a name="usage"></a>사용법  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to  
Set rs.DataSource = myDE      'Name of the object containing an IRowset  
```  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [DataSource 속성(ADO)](../../../ado/reference/ado-api/datasource-property-ado.md)
