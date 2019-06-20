---
title: DataMember 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataMember
helpviewer_keywords:
- DataMember property
ms.assetid: 2c8fb09e-10ad-49b5-ab41-2603771780d9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9de69478469a6bd177d12beab96e199b4720f3f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66695488"
---
# <a name="datamember-property"></a>DataMember 속성
검색 되는 데이터 멤버의 이름을 나타냅니다 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 에서 참조 하는 [DataSource](../../../ado/reference/ado-api/datasource-property-ado.md) 속성입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 **문자열** 값입니다. 이름은 대/소문자 구분 되지 않습니다.  
  
## <a name="remarks"></a>Remarks  
 이 속성은 데이터 환경을 사용 하 여 데이터 바인딩된 컨트롤을 만드는 데 사용 됩니다. 데이터 환경 데이터 (데이터 원본)가 포함 된 컬렉션으로 표현 되는 개체 (데이터 멤버) 라는 유지 관리를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
 합니다 **DataMember** 하 고 **DataSource** 속성을 함께 사용 되어야 합니다.  
  
 **DataMember** 속성으로 지정 된 개체를 결정 합니다 **DataSource** 속성으로 표현 되는 **레코드 집합** 개체입니다. 합니다 **레코드 집합** 이 속성을 설정 하기 전에 개체를 닫아야 합니다. 경우 오류가 생성 됩니다는 **DataMember** 전에 속성이 설정 되어 있지는 **DataSource** 속성을 또는 경우에는 **DataMember** 이름에 지정 된 개체에서 인식 되지 않습니다는 **DataSource** 속성입니다.  
  
## <a name="usage"></a>사용법  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to  
Set rs.DataSource = myDE      'Name of the object containing an IRowset  
```  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [DataSource 속성(ADO)](../../../ado/reference/ado-api/datasource-property-ado.md)
