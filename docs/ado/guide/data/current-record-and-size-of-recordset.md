---
title: 레코드 집합의 현재 레코드 및 크기 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925690"
---
# <a name="current-record-and-size-of-recordset"></a>현재 레코드 및 레코드 집합의 크기
이 섹션에서는 JScript 코드 예제의 샘플 **레코드 집합** 에서 커서의 현재 위치를 찾아 [레코드 집합을 반환](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)하는 방법에 대해 설명 합니다.  
  
## <a name="current-record"></a>현재 레코드  
 데이터 집합의 현재 레코드는 **레코드 집합** 개체의 커서 위치가 가리키는에 해당 합니다. 레코드 집합 **개체를** 호출 하 여 데이터 원본에서 **레코드**집합 개체를 반환 하는 경우 ( **예를**들어 **connection. namedcommand** 및 **connection**을 포함 하 여) 커서는 첫 번째 레코드를 가리키도록 설정 **됩니다.** 샘플 데이터 집합에서 초기 현재 레코드는 "열혈 삼촌 Bob의 유기적 Dried 배" 항목입니다.  
  
## <a name="size-of-recordset"></a>레코드 집합의 크기  
 **레코드 집합** 개체의 크기를 확인 하려면 **레코드 집합. RecordCount** 속성의 값을 가져옵니다. 이 값은 레코드 **집합**의 레코드 수를 나타내는 정수 (long)입니다. Microsoft SQL Server 용 OLEDB 공급자에서 데이터 집합이 반환 되는 경우이 값은 반환 되는 행 수를 제공 합니다. 닫힌 **레코드 집합** 에서 **RecordCount** 속성을 읽으면 오류가 발생 합니다.  
  
 레코드 수를 확인할 수 없으면 속성의 값은-1입니다.  
  
 또한 **RecordCount** 속성의 값은 공급자의 기능과 사용 되는 커서의 형식에 따라 달라 집니다. 앞 으로만 이동 가능한 커서의 경우 값은-1입니다. 정적 또는 키 집합 커서의 경우 값은 **레코드 집합** 개체에 반환 되는 실제 레코드 수입니다. 동적 커서의 경우 값은 데이터 원본에 따라-1 또는 실제 레코드 수입니다.  
  
 **Recordcount** 를 지 원하는 커서는 더 어렵게 작동 해야 하므로 커서에서 **recordcount**를 지원 하지 않는 것 보다 컴퓨팅 전력이 더 필요 합니다. 레코드 수를 알 필요가 없는 경우 다른 커서 유형을 사용 하 여 응용 프로그램의 성능을 향상 시킬 수 있습니다. 특히 대량의 데이터 집합을 처리 해야 하는 경우에 유용 합니다.  
  
 경우에 따라 공급자나 커서는 먼저 데이터 소스에서 모든 레코드를 인출 하지 않고 **RecordCount** 값을 확인할 수 없습니다. 정확한 계산을 위해 **레코드 집합**을 호출 합니다. **레코드 집합인 RecordCount**를 호출 하기 전의 **MoveLast** 메서드.  
  
 [JScript 코드 예제](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md) 를 사용 하 여 가져온 샘플 **레코드 집합** 개체는 앞 으로만 이동 가능한 커서를 사용 하므로이 개체의 **RecordCount** 를 호출 하면 항상-1이 반환 됩니다. **레코드 집합**을 호출 하는 코드 줄을 변경 하는 경우 **Open** 메서드 다음 예제와 같이 **RecordCount** 속성은 인출 된 레코드의 실제 수를 반환 합니다.  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 이는 [SQL Server 용 Microsoft OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) 를 사용 하는 정적 커서는 **RecordCount**를 지원 하기 때문입니다. 이 예제에서는 5 개의 레코드가 있으며이에 따라 **RecordCount** 는 5 값을 생성 해야 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
 [레코드 집합의 경계](../../../ado/guide/data/boundaries-of-a-recordset.md)
