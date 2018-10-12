---
title: getAutoCommit 메서드 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: af1f67f4-f568-4e58-abcc-5c809a89b547
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba024f3ddafa4f4b0231774e244b145004d3bff3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662021"
---
# <a name="getautocommit-method-sqlserverconnection"></a>getAutoCommit 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체에 대한 현재 자동 커밋 모드를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getAutoCommit()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 자동 커밋 모드를 설정 하는 경우 **false** 없는 경우.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getAutoCommit 메서드는 java.sql.Connection 인터페이스의 getAutoCommit 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
