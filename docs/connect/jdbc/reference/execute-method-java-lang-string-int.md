---
title: "execute 메서드 (java.lang.String, int[]) | Microsoft Docs"
ms.custom: 
ms.date: 02/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.execute (javal.lang.String.int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc73d1c3-e756-43af-b1fc-ac438cbd0965
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 50cb9686b883ac0a4d682e7ea28f1dba40257c7e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="execute-method-javalangstring-int"></a>execute 메서드(java.lang.String, int[])

  여러 결과 및 신호를 반환할 수 있는 지정된 된 SQL 문을 실행 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion-md.md)] 지정된 된 배열에 표시 되는 자동 생성 키 수 있도록 검색에 사용할 수 있습니다.

## <a name="syntax"></a>구문

```Java
public final boolean execute(
    java.lang.String sql,
    int[] columnIndexes)
```

#### <a name="parameters"></a>매개 변수
*sql*

A **문자열** SQL 문이 들어 있는입니다.

*columnIndexes*

배열을 **int**s 사용 가능 해야 하는 자동 생성 키의 열 인덱스를 나타내는입니다.

## <a name="return-value"></a>반환 값
**true 이면** 첫 번째 결과가 결과 집합이 면 합니다. 그렇지 않으면 **false**입니다.
  
## <a name="exceptions"></a>예외
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>주의
이 execute 메서드는 java.sql.Statement 인터페이스의 execute 메서드에 의해 지정 됩니다.

## <a name="see-also"></a>관련 항목:

[방법 &#40; 실행 SQLServerStatement &#41;](./execute-method-sqlserverstatement.md)

[SQLServerStatement 멤버](./sqlserverstatement-members.md)

[SQLServerStatement 클래스](./sqlserverstatement-class.md)

