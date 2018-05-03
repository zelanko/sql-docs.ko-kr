---
title: 데이터 모양 지정에 필요한 공급자 | Microsoft Docs
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
helpviewer_keywords:
- providers [ADO], data shaping
- data shaping [ADO], providers required
ms.assetid: d49d48d2-ac2d-4c11-895c-5a149b444620
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c30bf74788ba7fe1bd27edbc814aa0277867ac13
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="required-providers-for-data-shaping"></a>데이터 모양 지정에 필요한 공급자
데이터 모양 지정 두 공급자는 일반적으로 필요 합니다. 서비스 공급자 [for OLE DB Data Shaping Service](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md), 데이터를 셰이핑 기능 및 OLE DB Provider for SQL Server와 같은 데이터 공급자를 제공, 모양을 채우는 데이터의 행을 제공 [레코드 집합 ](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 서비스 공급자 (MSDataShape)의 이름을 값으로 지정할 수 있습니다는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성 또는 연결 문자열 키워드 "Provider = MSDataShape;"입니다.  
  
 데이터 공급자의 이름을 값으로 지정할 수는 **데이터 공급자** 동적 속성에 추가 되 고 **연결** 개체 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 사용 하 여 컬렉션 연결 문자열 키워드 또는 OLE DB Data Shaping Service "**데이터 공급자 = * * * 공급자*"입니다.  
  
 데이터 공급자가 없는 필요한 경우는 **레코드 집합** 채워지지 않습니다 (예를 들어 한 맞추어진 에서처럼 **레코드 집합** 열 새 키워드와 함께 생성 되는 위치). 이 경우에 지정 "**데이터 공급자 =** none;"입니다.  
  
## <a name="example"></a>예제  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 예제를 셰이핑](../../../ado/guide/data/data-shaping-example.md)   
 [형식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
