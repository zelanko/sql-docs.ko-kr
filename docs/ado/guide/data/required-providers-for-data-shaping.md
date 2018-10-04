---
title: 데이터 셰이프에 필요한 공급자 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping
- data shaping [ADO], providers required
ms.assetid: d49d48d2-ac2d-4c11-895c-5a149b444620
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 482139f8aa3dc42bbd17593b58fcc8510f1fc9a8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713841"
---
# <a name="required-providers-for-data-shaping"></a>데이터 셰이프에 필요한 공급자
두 공급자를 해야 일반적으로 데이터 모양 지정 합니다. 서비스 공급자 [OLE db Data Shaping Service](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)데이터를 셰이핑 기능 및 OLE DB Provider for SQL Server 같은 데이터 공급자를 제공, 모양을 채우는 데이터의 행을 제공 [레코드 집합 ](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 서비스 공급자 (MSDataShape)의 이름을 값으로 지정할 수 있습니다 합니다 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성 또는 연결 문자열 키워드 "공급자에서는 MSDataShape; ="입니다.  
  
 데이터 공급자의 이름을 값으로 지정할 수 있습니다 합니다 **Data Provider** 에 추가 되는 동적 속성을 **연결** 개체 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 사용 하 여 컬렉션 OLE DB 또는 연결 문자열 키워드에 대 한 Data Shaping Service "**Data Provider = * 공급자*"입니다.  
  
 없는 데이터 공급자가 필요 합니다 **레코드 집합** 채워지지 않습니다 (작성을 같이 예를 들어 **레코드 집합** 열 NEW 키워드를 사용 하 여 생성 되는 위치). 이 경우 지정 "**Data Provider =** none;"입니다.  
  
## <a name="example"></a>예제  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터 셰이핑 예제](../../../ado/guide/data/data-shaping-example.md)   
 [공식적인 셰이프 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
