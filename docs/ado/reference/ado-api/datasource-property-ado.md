---
description: DataSource 속성(ADO)
title: DataSource 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataSource
helpviewer_keywords:
- DataSource property [ADO]
ms.assetid: 300a702a-3544-48c5-b759-83b511fe97e0
author: rothja
ms.author: jroth
ms.openlocfilehash: 48c5969df864364cd87d131fce2740a5a0e043f7
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974264"
---
# <a name="datasource-property-ado"></a>DataSource 속성(ADO)
[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체로 표시할 데이터를 포함 하는 개체를 나타냅니다.  
  
## <a name="remarks"></a>설명  
 이 속성은 데이터 환경을 사용 하 여 데이터 바인딩된 컨트롤을 만드는 데 사용 됩니다. 데이터 환경에서는 **레코드 집합** 개체로 표시 되는 명명 된 개체 (데이터 멤버)를 포함 하는 데이터 (데이터 원본) 컬렉션을 유지 관리 합니다.  
  
 [DataMember](../../../ado/reference/ado-api/datamember-property.md) 및 **DataSource** 속성은 함께 사용 해야 합니다.  
  
 참조 되는 개체는 **IDataSource** 인터페이스를 구현 해야 하며 **IRowset** 인터페이스를 포함 해야 합니다.  
  
## <a name="usage"></a>사용  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to.  
Set rs.DataSource = myDE      'Name of the object containing an IRowset.  
```  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [DataMember 속성](../../../ado/reference/ado-api/datamember-property.md)
