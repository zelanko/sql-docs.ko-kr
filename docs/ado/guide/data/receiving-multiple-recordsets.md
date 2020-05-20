---
title: 여러 레코드 집합 받기 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving multiple Recordsets [ADO]
- Recordset object [ADO], receiving multiple Recordsets
ms.assetid: 2a7ad7a6-f00d-4355-b0b5-d0ab957b0566
author: rothja
ms.author: jroth
ms.openlocfilehash: 12aa80b918d11dad07119a26da3da8f27ef82cdb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759109"
---
# <a name="receiving-multiple-recordsets"></a>다중 레코드 집합 수신
[SQL Server 용 Microsoft OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) 는 여러 sql 문을 포함 하는 단일 명령에 대 한 여러 **레코드 집합** 개체를 반환 하는 것을 지원 합니다. Sql 문 당 하나의 **레코드 집합** **레코드 집합**의 반환 순서는 SQL 문이 명령 텍스트에 배치 되는 순서에 따라 결정 됩니다.  
  
 또한 SQL Server에 대 한 Microsoft OLE DB 공급자는 명령에 COMPUTE 절이 포함 된 경우 ADO에 여러 결과 집합을 반환 합니다. 예를 들어 다음 SQL 문을 포함 하는 명령은 두 개의 **레코드 집합** 개체 (*ProductID*, *ProductName*, *UnitPrice*)의 행 집합에 대 한 결과를 반환 하 고 다른 하나는 테이블에 있는 모든 제품의 평균 가격을 반환 합니다.  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 **NextRecordset** 메서드를 사용 하 여 두 개체를 열거할 수 있습니다.  
  
 자세한 내용은 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)를 참조 하세요.
