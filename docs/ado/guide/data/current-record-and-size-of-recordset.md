---
title: 현재 레코드 및 레코드 집합의 크기 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e63ff331-8655-4be7-82c6-e6cd6cc9d16d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a01e17ea9c786a724e5869a28bf4d8927b58ac81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925690"
---
# <a name="current-record-and-size-of-recordset"></a>현재 레코드 및 레코드 집합의 크기
이 섹션에서는 샘플에서 커서의 현재 위치를 찾는 방법에 설명 합니다 **Recordset** 에 [JScript 코드 예제에서는 레코드 집합을 반환할](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)합니다.  
  
## <a name="current-record"></a>현재 레코드  
 데이터 집합의 현재 레코드에 해당 하는 커서의 위치를 가리키는 합니다 **레코드 집합** 개체입니다. 경우는 **Recordset** 개체가 호출의 결과로 데이터 소스에서 반환 됩니다 **Recordset.Open**, **Command.Execute**, 또는 **Connection.Execute**  (포함 **Connection.NamedCommand** 하 고 **Connection.StoredProcedure**), 커서가 첫 번째 레코드를 가리키도록 설정 됩니다. 샘플 데이터 집합을 초기 현재 레코드의 "대양 유기적 건과 배" 항목입니다.  
  
## <a name="size-of-recordset"></a>레코드 집합의 크기  
 크기를 확인 하는 **레코드 집합** 개체, 값을 가져옵니다 합니다 **Recordset.RecordCount** 속성입니다. 이 값은 레코드의 수를 나타내는 정수를 **레코드 집합**합니다. 데이터 집합은 Microsoft SQL Server에 대 한 OLEDB 공급자에서 반환 되 면이 값 반환 되는 행 수를 제공 합니다. 읽기를 **RecordCount** 속성에 닫힌 **레코드 집합** 오류가 발생 합니다.  
  
 레코드의 수를 확인할 수 없는 속성의 값은-1입니다.  
  
 값을 **RecordCount** 속성 또한 사용 되는 커서 형식과 공급자의 기능에 따라 달라 집니다. 정방향 전용 커서는 값은-1입니다. 정적 또는 키 집합 커서에 대 한 값이에서 반환 된 레코드의 실제 수는 **레코드 집합** 개체입니다. 동적 커서는 값은-1 또는 데이터 원본에 따라 레코드의 실제 수입니다.  
  
 지 원하는 커서 **Recordcount** 해야 작업 있어 harder, 필요한 추가 컴퓨팅 기능이 보다 커서를 지원 하지 않습니다 **Recordcount**합니다. 레코드의 수를 알 필요가 없습니다, 하는 경우 다른 커서 유형을 사용 하 여 향상 시킬 수 있습니다 응용 프로그램의 성능, 특히 큰 데이터 집합을 처리 해야 하는 경우.  
  
 경우에 따라 공급자 또는 커서 수 없는 확인 합니다 **RecordCount** 첫 번째 데이터 원본의 모든 레코드를 페치 하지 않고 값입니다. 정확한 계산을 위해 호출 된 **Recordset**. **MoveLast** 메서드를 호출 하기 전에 **Recordset.RecordCount**합니다.  
  
 샘플 **레코드 집합** 사용 하 여 가져온 개체는 [JScript 코드 예제](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md) 호출 하므로 앞 으로만 이동 가능한 커서를 사용 하 여 **RecordCount** 이 개체에서 항상-1의 결과입니다. 호출 하는 코드 줄을 변경 하는 경우는 **Recordset**. **열기** 다음 예제와 같이 메서드를 **RecordCount** 속성은 인출 된 레코드의 실제 수를 반환 합니다.  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 왜냐하면 정적 커서를 합니다 [Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) 지원 **RecordCount**합니다. 이 예제는 5 개 레코드 이므로 **RecordCount** 5의 값을 생성 해야 합니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
 [레코드 집합의 경계](../../../ado/guide/data/boundaries-of-a-recordset.md)
