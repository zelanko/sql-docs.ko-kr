---
title: closeUnreferencedPreparedStatementHandles 메서드 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.closeUnreferencedPreparedStatementHandles
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7256475421b8666e28eaaf03f3ff4cb9768aa289
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955608"
---
# <a name="closeunreferencedpreparedstatementhandles-method-sqlserverconnection"></a>closeUnreferencedPreparedStatementHandles 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 보류 중인 삭제 된 준비 문이 실행 될 때까지 준비 취소 요청을 강제로 실행 합니다.

## <a name="syntax"></a>구문  
  
```  
  
public void closeUnreferencedPreparedStatementHandles()  
```  


## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  

## <a name="remarks"></a>Remarks  
 이 메서드는 JDBC 드라이버 버전 6.4 및 이후 버전에서 사용할 수 있습니다.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
