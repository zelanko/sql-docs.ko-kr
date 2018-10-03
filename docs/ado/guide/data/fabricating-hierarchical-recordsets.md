---
title: 계층적 레코드 집합 구성 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17cf661e092e253e206b595dec5d807a35b895fb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770891"
---
# <a name="fabricating-hierarchical-recordsets"></a>계층적 레코드 집합 구성
다음 예제는 데이터 셰이핑 부모, 자식 및 손자에 대 한 열을 정의 하는 문법을 사용 하 여 기본 데이터 원본 사용 하지 않고 계층적 레코드 집합을 구성 하는 방법을 보여 줍니다 **레코드 집합**합니다.  
  
 계층을 구성 하 **레코드 집합**를 지정 해야 합니다는 [OLE DB (ADO 서비스 공급자)에 대 한 Microsoft Data Shaping Service](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (MSDataShape)에서 NONE 데이터 공급자 값을 지정할 수 있습니다는 연결 문자열 매개 변수를 [엽니다](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체. 자세한 내용은 [데이터 셰이프에 필요한 공급자](../../../ado/guide/data/required-providers-for-data-shaping.md)합니다.  
  
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
  
 즉시 합니다 **레코드 집합** 되었습니다을 채우거 채워진, 조작 하거나 수를 파일에 저장 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [계층적 레코드 집합의 행에 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [공식적인 셰이프 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [데이터 셰이프에 필요한 공급자](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [셰이프 APPEND 절](../../../ado/guide/data/shape-append-clause.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
