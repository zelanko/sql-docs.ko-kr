---
title: setBigDecimal 메서드(SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setBigDecimal
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 860f86db-d840-401a-a5c2-cd22e8cc1e4e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d232b5c103c43d9a8856982fd084e460bb521c6e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66764854"
---
# <a name="setbigdecimal-method-sqlserverpreparedstatement"></a>setBigDecimal 메서드(SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수 번호를 지정된 BigDecimal 개체로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setBigDecimal(int n,  
                                java.math.BigDecimal x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *n*  
  
 매개 변수 번호를 나타내는 **int**입니다.  
  
 *x*  
  
 BigDecimal 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 setBigDecimal 메서드는 java.sql.PreparedStatement 인터페이스의 setBigDecimal 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
