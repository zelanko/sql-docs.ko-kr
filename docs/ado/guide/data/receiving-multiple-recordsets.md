---
title: "다중 레코드 집합을 받는 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- receiving multiple Recordsets [ADO]
- Recordset object [ADO], receiving multiple Recordsets
ms.assetid: 2a7ad7a6-f00d-4355-b0b5-d0ab957b0566
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ab72906b1f36e22bba58b58ca7917b3399ebc458
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="receiving-multiple-recordsets"></a>다중 레코드 집합 받기
[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) 여러 반환 지원 **레코드 집합** 여러 SQL 문을 포함 하는 단일 명령에 대 한 개체 하나 **레코드 집합**SQL 문당 합니다. 되는 순서는 **레코드 집합**명령 텍스트에 SQL 문이 배치 되는 순서에 따라 반환 됩니다.  
  
 또한 Microsoft OLE DB Provider for SQL Server 명령 COMPUTE 절이 포함 된 경우 여러 결과 집합 ADO에 게 반환 합니다. 예를 들어 다음 SQL 문을 포함 하는 명령을 돌아갑니다 결과를 두 개의 **레코드 집합** 개체:의 행 집합에 대 한 (*ProductID*, *ProductName*, *UnitPrice*), 오류 코드 및 기타 테이블의 모든 제품의 평균 가격에 대 한 합니다.  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 사용할 수는 **Recordset.NextRecordset** 메서드 두 개체를 열거 합니다.  
  
 자세한 내용은 참조 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)합니다.
