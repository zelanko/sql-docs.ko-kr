---
title: SQLServerClob 생성자(SQLServerConnection, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.SQLServerClob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7058f4f7-ef3e-4d62-90d1-79299708b1eb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a454567f031d935b6bfcdd8d5d32a6d2bead380f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803139"
---
# <a name="sqlserverclob-constructor-sqlserverconnection-javalangstring"></a>SQLServerClob 생성자(SQLServerConnection, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체 및 데이터의 문자열이 지정된 경우 [SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md) 클래스의 새 인스턴스를 초기화합니다.  
  
> [!NOTE]  
>  JDBC 드라이버 버전 2.0에서는 이 메서드가 사용되지 않습니다. 대신 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md) 메서드를 사용합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public SQLServerClob(SQLServerConnection connection,  
                     java.lang.String data)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *연결*  
  
 SQLServerConnection 개체입니다.  
  
 *data*  
  
 CLOB 데이터입니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerClob 생성자](../../../connect/jdbc/reference/sqlserverclob-constructors.md)   
 [SQLServerClob 멤버](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 클래스](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
