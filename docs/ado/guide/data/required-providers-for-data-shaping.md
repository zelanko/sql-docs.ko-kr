---
description: 데이터 셰이프에 필요한 공급자
title: 데이터 셰이핑에 필요한 공급자 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping
- data shaping [ADO], providers required
ms.assetid: d49d48d2-ac2d-4c11-895c-5a149b444620
author: rothja
ms.author: jroth
ms.openlocfilehash: bd2829c49adb318ae80eeefd2ec2913fd8620d2b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979804"
---
# <a name="required-providers-for-data-shaping"></a>데이터 셰이프에 필요한 공급자
데이터 셰이핑에는 일반적으로 두 개의 공급자가 필요 합니다. [OLE DB에 대 한 서비스 공급자, 데이터 셰이핑 서비스](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)는 데이터 셰이핑 기능을 제공 하 고 SQL Server 용 OLE DB 공급자와 같은 데이터 공급자는 셰이프 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)을 채울 데이터 행을 제공 합니다.  
  
 서비스 공급자 (MSDataShape)의 이름은 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성의 값 또는 연결 문자열 키워드 "provider = MSDataShape;"로 지정할 수 있습니다.  
  
 데이터 공급자의 이름을 **Data Provider** 동적 속성 값으로 지정할 수 있습니다 .이 속성은 OLE DB에 대 한 데이터 셰이핑 서비스에서 **연결** 개체 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 추가 하거나 연결 문자열 키워드인 "**Data Provider =** _provider_"로 추가 됩니다.  
  
 **레코드 집합이** 채워지지 않은 경우 데이터 공급자가 필요 하지 않습니다 (예: 새 키워드로 열을 생성 하는 생성 된 **레코드 집합** 의 경우). 이 경우 "**Data Provider =** none;"을 지정 합니다.  
  
## <a name="example"></a>예제  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 셰이핑 예](../../../ado/guide/data/data-shaping-example.md)   
 [공식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
