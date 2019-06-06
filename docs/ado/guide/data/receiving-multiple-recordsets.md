---
title: 다중 레코드 집합 수신 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 78e6ed78e8c61a9ce14e30f0eb286d55da0e63b9
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700750"
---
# <a name="receiving-multiple-recordsets"></a>다중 레코드 집합 수신
[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) 지 원하는 여러 반환 **Recordset** 여러 SQL 문이 포함 된 단일 명령에 대 한 개체 하나 **레코드 집합**당 SQL 문입니다. 순서를 **레코드 집합**명령 텍스트에서 SQL 문을 배치 되는 순서를 따릅니다이 반환 됩니다.  
  
 또한 Microsoft OLE DB Provider for SQL Server 명령을 COMPUTE 절을 포함 하는 경우 여러 결과 집합 ADO에 게 반환 합니다. 예를 들어, 다음 SQL 문을 포함 하는 명령을 돌아갑니다 결과 두 **Recordset** 개체:의 행 집합에 대 한 하나 (*ProductID*를 *ProductName*, *UnitPrice*), 다른 테이블의 모든 제품의 평균 가격 중 한 합니다.  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 사용할 수는 **Recordset.NextRecordset** 두 개체를 열거 하는 방법입니다.  
  
 자세한 내용은 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)합니다.
