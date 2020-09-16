---
description: prepareStatement 메서드(java.lang.String)
title: prepareStatement 메서드(java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e825765c-eb55-4800-951b-f3495da36641
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f9cec12d2443e84ef3334e19253a64ff60fea1c9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432865"
---
# <a name="preparestatement-method-javalangstring"></a>prepareStatement 메서드(java.lang.String)

데이터베이스로 매개 변수가 있는 SQL 문을 보내기 위한 [SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md) 개체를 만듭니다.

## <a name="syntax"></a>구문

```
public java.sql.PreparedStatement prepareStatement(java.lang.String sql)
```

#### <a name="parameters"></a>매개 변수
*sql*

SQL 문이 포함된 **String**입니다.

## <a name="return-value"></a>반환 값
PreparedStatement 개체입니다.

## <a name="exceptions"></a>예외  
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>설명
이 prepareStatement 메서드는 java.sql.Connection 인터페이스의 prepareStatement 메서드에 의해 지정됩니다.

## <a name="see-also"></a>참고 항목

[prepareStatement 메서드 &#40;SQLServerConnection&#41;](./preparestatement-method-sqlserverconnection.md)

[SQLServerConnection 멤버](./sqlserverconnection-members.md)

[SQLServerConnection 클래스](./sqlserverconnection-class.md)
