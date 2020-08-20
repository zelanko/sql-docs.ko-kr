---
description: 계층적 레코드 집합 구성
title: Suz 계층 구조 레코드 집합 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset fabrication [ADO]
- hierarchical Recordsets [ADO]
- fabricating hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: a584e642-a4a3-418e-bc20-3aff81a5625a
author: rothja
ms.author: jroth
ms.openlocfilehash: 2f418d2eb21f2cb02223234f6231efb39b232faa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453405"
---
# <a name="fabricating-hierarchical-recordsets"></a>계층적 레코드 집합 구성
다음 예에서는 데이터 셰이핑 문법을 사용 하 여 부모, 자식 및 손자 **레코드 집합**에 대 한 열을 정의 하 여 기본 데이터 원본 없이 계층적 레코드 집합을 만드는 방법을 보여 줍니다.  
  
 계층적 **레코드 집합**을 만들려면 [OLE DB (ADO 서비스 공급자)에 대 한 Microsoft 데이터 셰이핑 서비스](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) 를 지정 해야 합니다 (MSDataShape). [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드의 CONNECTION string 매개 변수에서 Data Provider 값을 NONE으로 지정할 수 있습니다. 자세한 내용은 [데이터 셰이핑에 필요한 공급자](../../../ado/guide/data/required-providers-for-data-shaping.md)를 참조 하세요.  
  
```  
Dim cn As New ADODB.Connection  
Dim rsCustomers As New ADODB.Recordset  
  
cn.Open "Provider=MSDataShape;Data Provider=NONE;"  
  
strShape = _  
"SHAPE APPEND NEW adInteger AS CustID," & _  
            " NEW adChar(25) AS FirstName," & _  
            " NEW adChar(25) AS LastName," & _  
            " NEW adChar(12) AS SSN," & _  
            " NEW adChar(50) AS Address," & _  
         " ((SHAPE APPEND NEW adChar(80) AS VIN_NO," & _  
                        " NEW adInteger AS CustID," & _  
                        " NEW adChar(20) AS BodyColor, " & _  
                     " ((SHAPE APPEND NEW adChar(80) AS VIN_NO," & _  
                                    " NEW adChar(20) AS Make, " & _  
                                    " NEW adChar(20) AS Model," & _  
                                    " NEW adChar(4) AS Year) " & _  
                        " AS VINS RELATE VIN_NO TO VIN_NO))" & _  
            " AS Vehicles RELATE CustID TO CustID) "  
  
rsCustomers.Open strShape, cn, adOpenStatic, adLockOptimistic, -1  
```  
  
 **레코드 집합** 을 만든 후에는 파일에 대해 채우거 나 조작 하거나 저장할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [계층적 레코드 집합의 행 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [공식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [데이터 셰이핑에 필요한 공급자](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape APPEND 절](../../../ado/guide/data/shape-append-clause.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
