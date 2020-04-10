---
title: execute 메서드(java.lang.String, int[]) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.execute (javal.lang.String.int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc73d1c3-e756-43af-b1fc-ac438cbd0965
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7195d5c5bf4efb593e53dea6e5404cc8adb70830
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922126"
---
# <a name="execute-method-javalangstring-int"></a>execute 메서드(java.lang.String, int[])

  여러 결과를 반환할 수 있는 지정된 SQL 문을 실행하고 지정된 배열에 표시된 자동 생성 키를 검색에 사용할 수 있도록 해야 할지 여부를 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에 알립니다.

## <a name="syntax"></a>구문

```Java
public final boolean execute(
    java.lang.String sql,
    int[] columnIndexes)
```

#### <a name="parameters"></a>매개 변수
*sql*

SQL 문이 포함된 **문자열**입니다.

*columnIndexes*

자동 생성 키의 열 인덱스를 사용할 수 있도록 해야 하는지 여부를 나타내는 **int**의 배열입니다.

## <a name="return-value"></a>Return Value
첫 번째 결과가 결과 집합이면 **true**이고, 그렇지 않으면 **false**입니다.
  
## <a name="exceptions"></a>예외
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>설명
이 execute 메서드는 java.sql.Statement 인터페이스의 execute 메서드에 의해 지정됩니다.

## <a name="see-also"></a>참고 항목

[execute 메서드&#40;SQLServerStatement&#41;](./execute-method-sqlserverstatement.md)

[SQLServerStatement 멤버](./sqlserverstatement-members.md)

[SQLServerStatement 클래스](./sqlserverstatement-class.md)
