---
title: executeUpdate 메서드 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeUpdate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 91ecb1cd-001d-4ac9-9ae8-5db05c3c2959
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d3a976f9e953729be7b9f993139a7603fe8444cc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804858"
---
# <a name="executeupdate-method-javalangstring"></a>executeUpdate 메서드(java.lang.String)

INSERT, UPDATE, MERGE 또는 DELETE 문과 같은 지정된 SQL 문이나 SQL DDL 문 같이 아무 것도 반환하지 않는 SQL 문을 실행합니다.

## <a name="syntax"></a>구문

```
public final int executeUpdate(java.lang.String sql)
```

#### <a name="parameters"></a>매개 변수
*sql*

SQL 문이 포함된 **문자열**입니다.

## <a name="return-value"></a>반환 값
영향을 받는 행 수를 나타내는 **int**이며, DDL 문을 사용하는 경우에는 0입니다.

## <a name="exceptions"></a>예외
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Remarks
이 executeUpdate 메서드는 java.sql.PreparedStatement 인터페이스의 executeUpdate 메서드에 의해 지정 됩니다.

SQLServerPreparedStatement 개체에 대한 SQL 문은 개체가 만들어질 때 지정되므로 이 메서드를 호출하면 예외가 발생합니다.

## <a name="see-also"></a>참고 항목

[executeUpdate 메서드 &#40;SQLServerPreparedStatement&#41;](./executeupdate-method-sqlserverpreparedstatement.md)

[SQLServerPreparedStatement 멤버](./sqlserverpreparedstatement-members.md)

[SQLServerPreparedStatement 클래스](./sqlserverpreparedstatement-class.md)
