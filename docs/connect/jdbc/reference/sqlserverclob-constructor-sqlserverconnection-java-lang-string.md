---
title: SQLServerClob 생성자 (SQLServerConnection, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.SQLServerClob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7058f4f7-ef3e-4d62-90d1-79299708b1eb
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 86d57a9b750c037df64005b9f55b099d5b3bca82
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverclob-constructor-sqlserverconnection-javalangstring"></a>SQLServerClob 생성자(SQLServerConnection, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  새 인스턴스를 초기화는 [SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md) 지정 되 면 클래스는 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체와 데이터의 문자열입니다.  
  
> [!NOTE]  
>  JDBC 드라이버 버전 2.0에서는 이 메서드가 사용되지 않습니다. 대신를 사용 하 여는 [createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerClob 생성자](../../../connect/jdbc/reference/sqlserverclob-constructors.md)   
 [SQLServerClob 멤버](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 클래스](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
