---
title: getWarnings 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getWarnings
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 15af39bf-6285-44cc-a021-7341e7a055c4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b57d4a5f49bd292ea76ab0047b8ddf871aed6c08
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812881"
---
# <a name="getwarnings-method-sqlserverconnection"></a>getWarnings 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체에 대한 호출에서 보고된 첫 번째 경고를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.SQLWarning getWarnings()  
```  
  
## <a name="return-value"></a>반환 값  
 SQLWarning 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getWarnings 메서드는 java.sql.Connection 인터페이스의 getWarnings 메서드에 의해 지정 됩니다.  
  
 이후의 경고는 첫 번째 SQLWarning에 연결 되며 getNextWarning 메서드를 사용 하 여 호출 합니다. 닫혀 있는 연결에 대해 호출될 경우에는 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
