---
title: getConnection 메서드 (SQLServerPooledConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPooledConnection.getConnection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 05bdb61f-26e8-480f-a1c1-1e46a8ed4b70
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 590fca2fcf97929755faa3633b257849b3fd7030
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687428"
---
# <a name="getconnection-method-sqlserverpooledconnection"></a>getConnection 메서드(SQLServerPooledConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) 개체가 나타내는 실제 연결에 대한 개체 핸들을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Connection getConnection()  
```  
  
## <a name="return-value"></a>반환 값  
 연결 개체입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 이 getConnection 메서드는 javax.sql.PooledConnection 인터페이스의 getConnection 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerPooledConnection 메서드](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [SQLServerPooledConnection 멤버](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [SQLServerPooledConnection 클래스](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  
