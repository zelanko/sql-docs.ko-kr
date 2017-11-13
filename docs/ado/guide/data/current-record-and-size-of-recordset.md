---
title: "현재 레코드와 레코드 집합의 크기 | Microsoft Docs"
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
- record location [ADO]
- current record [ADO]
ms.assetid: e63ff331-8655-4be7-82c6-e6cd6cc9d16d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb50826230e46cc71106a2b17d01914eae024f47
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="current-record-and-size-of-recordset"></a>현재 레코드와 레코드 집합의 크기
이 섹션에서는 샘플에는 커서의 현재 위치를 찾는 방법을 설명 **레코드 집합** 에 [JScript 코드 예제에서는 레코드 집합을 반환 하려면](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)합니다.  
  
## <a name="current-record"></a>현재 레코드  
 에 해당 하는 데이터 집합의 현재 레코드의 커서의 위치를 가리키는 하는 **레코드 집합** 개체입니다. 경우는 **레코드 집합** 가 반환 되는 개체 데이터 소스에서 호출한 결과 **Recordset.Open**, **Command.Execute**, 또는 **Connection.Execute**  (포함 하 여 **Connection.NamedCommand** 및 **Connection.StoredProcedure**), 커서가 첫 번째 레코드를 가리키도록 설정 합니다. 샘플 데이터 집합의 초기 현재 레코드 인지는 "의 유기적 가공 (배)" 항목입니다.  
  
## <a name="size-of-recordset"></a>레코드 집합의 크기  
 크기를 확인 하려면 한 **레코드 집합** 개체, 값을 가져올는 **Recordset.RecordCount** 속성입니다. 이 값은 레코드의 수를 나타내는 long 정수는 **레코드 집합**합니다. Microsoft SQL Server에 대 한 데이터 집합에서 OLEDB 공급자에서 반환 되 면 반환 된 행 수가이 값에 제공 합니다. 읽기는 **RecordCount** 닫힌된 속성 **레코드 집합** 하면 오류가 발생 합니다.  
  
 레코드의 수를 확인할 수 없는 경우 속성의 값은-1입니다.  
  
 값은 **RecordCount** 속성도 사용 되는 커서 형식과 공급자의 기능에 따라 달라 집니다. 정방향 전용 커서에 대 한 값은-1입니다. 정적 또는 키 집합 커서에 대 한 값이 실제 수에서 반환 되는 레코드는 **레코드 집합** 개체입니다. 동적 커서는 값은-1 또는 데이터 원본에 따라 레코드의 실제 수입니다.  
  
 지 원하는 커서 **Recordcount** 해야 작업 이므로 더 어려워지므로, 추가 컴퓨팅 기능이 필요, 커서를 지원 하지 않습니다 보다 **Recordcount**합니다. 레코드의 수를 파악 해야 하는 경우 다른 커서 유형을 사용 하 여 향상 시킬 수 있습니다 응용 프로그램의 성능을 특히 큰 데이터 집합으로 처리 해야 하는 경우.  
  
 경우에 따라 공급자 또는 커서 수 없으면 결정 하는 **RecordCount** 데이터 원본의 모든 레코드를 먼저 반입 값입니다. 정확한 계산을 보장 하려면 호출는 **레코드 집합**. **MoveLast** 메서드 호출 하기 전에 **Recordset.RecordCount**합니다.  
  
 샘플 **레코드 집합** 사용 하 여 가져온 개체는 [JScript 코드 예제에서는](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md) 호출 하는 정방향 전용 커서를 사용 하 여 **RecordCount** 이 개체에서 항상 수행-1입니다. 호출 하는 코드 줄을 변경 하는 경우는 **레코드 집합**. **열기** 다음 예에서 같이 메서드는 **RecordCount** 속성은 인출 된 레코드의 실제 수를 반환 합니다.  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 즉, 정적 커서와는 [Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) 지원 **RecordCount**합니다. 이 예제는 다섯 개의 레코드가 이므로 **RecordCount** 5의 값을 양보 해야 합니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
 [레코드 집합의 경계](../../../ado/guide/data/boundaries-of-a-recordset.md)

