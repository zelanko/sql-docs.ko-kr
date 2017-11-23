---
title: "prepareStatement 메서드 (java.lang.String) | Microsoft Docs"
ms.custom: 
ms.date: 02/07/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerConnection.prepareStatement (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: e825765c-eb55-4800-951b-f3495da36641
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cbf8bdbb869f4a82133918d579f7dfc1fd23d3d0
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="preparestatement-method-javalangstring"></a>prepareStatement 메서드(java.lang.String)

만듭니다는 [SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md) 보내는 개체를 데이터베이스에 대 한 SQL 문을 매개 변수화 합니다.

## <a name="syntax"></a>구문

```
public java.sql.PreparedStatement prepareStatement(java.lang.String sql)
```

#### <a name="parameters"></a>매개 변수
*sql*

A **문자열** SQL 문을 포함 합니다.

## <a name="return-value"></a>반환 값
PreparedStatement 개체입니다.

## <a name="exceptions"></a>예외  
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>주의
이 prepareStatement 메서드는 java.sql.Connection 인터페이스의 prepareStatement 메서드에 의해 지정 됩니다.

## <a name="see-also"></a>관련 항목:

[prepareStatement 메서드 &#40; SQLServerConnection &#41;](./preparestatement-method-sqlserverconnection.md)

[SQLServerConnection 멤버](./sqlserverconnection-members.md)

[SQLServerConnection 클래스](./sqlserverconnection-class.md)
