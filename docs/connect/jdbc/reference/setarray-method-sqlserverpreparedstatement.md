---
title: setTime 메서드(SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setArray
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b7fb66d4-6a42-43d0-ba68-8514816917cb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1fd6a0b0b0e60543beb6a943d80d5cf0cf40c7b5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811621"
---
# <a name="setarray-method-sqlserverpreparedstatement"></a>setArray 메서드(SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수 번호를 지정된  개체로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setArray(int i,  
                           java.sql.Array x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *i*  
  
 매개 변수 번호를 나타내는 **int**입니다.  
  
 *x*  
  
 배열 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 setTime 메서드는 java.sql.PreparedStatement 인터페이스의 setTime 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
