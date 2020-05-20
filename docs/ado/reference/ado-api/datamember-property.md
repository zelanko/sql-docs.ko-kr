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
author: rothja
ms.author: jroth
ms.openlocfilehash: 87d525907edde2e3dc99b78eb827c571c604d8b7
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763484"
---
# <a name="datamember-property"></a>DataMember 속성
[DataSource](../../../ado/reference/ado-api/datasource-property-ado.md) 속성이 참조 하는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 에서 검색 되는 데이터 멤버의 이름을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **문자열** 값을 설정 하거나 반환 합니다. 이름은 대/소문자를 구분하지 않습니다.  
  
## <a name="remarks"></a>설명  
 이 속성은 데이터 환경을 사용 하 여 데이터 바인딩된 컨트롤을 만드는 데 사용 됩니다. 데이터 환경에서는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체로 표시 되는 명명 된 개체 (데이터 멤버)를 포함 하는 데이터 (데이터 원본) 컬렉션을 유지 관리 합니다.  
  
 **DataMember** 및 **DataSource** 속성은 함께 사용 해야 합니다.  
  
 **DataMember** 속성은 **DataSource** 속성으로 지정 되는 개체를 **레코드 집합** 개체로 나타낼지 여부를 결정 합니다. 이 속성을 설정 하려면 먼저 **레코드 집합** 개체를 닫아야 합니다. **Datasource 속성이 datasource** 속성 **앞에 설정** 되어 있지 않거나 **datasource** 속성에 지정 된 개체에서 **datamember** 이름이 인식 되지 않는 경우 오류가 생성 됩니다.  
  
## <a name="usage"></a>사용량  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to  
Set rs.DataSource = myDE      'Name of the object containing an IRowset  
```  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [DataSource 속성(ADO)](../../../ado/reference/ado-api/datasource-property-ado.md)
