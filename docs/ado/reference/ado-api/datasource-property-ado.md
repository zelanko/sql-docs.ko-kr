---
title: "DataSource 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset20::DataSource
helpviewer_keywords: DataSource property [ADO]
ms.assetid: 300a702a-3544-48c5-b759-83b511fe97e0
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 901dc09e94acfbd6299cfcb72586e80edc687360
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="datasource-property-ado"></a>DataSource 속성 (ADO)
로 나타낼 수 있는 데이터를 포함 하는 개체를 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
## <a name="remarks"></a>주의  
 이 속성은 데이터 환경을 사용 하 여 데이터 바인딩된 컨트롤을 만들려면 사용 합니다. 데이터 환경 컬렉션을 포함 하는 데이터 (데이터 원본)로 나타낼 수 있는 개체 (데이터 멤버) 라는 유지 관리는 **레코드 집합** 개체*합니다.*  
  
 [DataMember](../../../ado/reference/ado-api/datamember-property.md) 및 **DataSource** 속성을 함께에서 사용 해야 합니다.  
  
 참조 하는 개체가 구현 해야 합니다는 **IDataSource** 인터페이스를 포함 해야 합니다는 **IRowset** 인터페이스입니다.  
  
## <a name="usage"></a>사용법  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to.  
Set rs.DataSource = myDE      'Name of the object containing an IRowset.  
```  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [DataMember 속성](../../../ado/reference/ado-api/datamember-property.md)
