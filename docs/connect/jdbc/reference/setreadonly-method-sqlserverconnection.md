---
title: setReadOnly 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setReadOnly
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bd11fd50-f092-43a0-a6bc-c63e70cff8da
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6ff943c74c4366a2be2266782e3f44296a4bf49
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920716"
---
# <a name="setreadonly-method-sqlserverconnection"></a>setReadOnly 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC 드라이버에서 데이터베이스 최적화를 수행하기 위한 힌트로 사용할 수 있도록 이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체를 읽기 전용 모드로 설정합니다.  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 이 메서드가 지원되지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setReadOnly(boolean readOnly)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *readOnly*  
  
 연결을 읽기 전용으로 하려면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setReadOnly 메서드는 java.sql.Connection 인터페이스의 setReadOnly 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
