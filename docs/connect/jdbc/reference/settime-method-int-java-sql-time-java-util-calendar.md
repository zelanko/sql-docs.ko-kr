---
description: setTime 메서드(int, java.sql.Time, java.util.Calendar)
title: setTime 메서드(int, java.sql.Time, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setTime (int, java.sql.Time, java.lang.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 79ff6eef-6ad7-4e33-95be-c2d552c65546
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5bc53fbdb8eaf2cd4667967f7e7665b389652ac8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462705"
---
# <a name="settime-method-int-javasqltime-javautilcalendar"></a>setTime 메서드(int, java.sql.Time, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 시간 및 달력 값으로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setTime(int n,  
                          java.sql.Time x,  
                          java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *n*  
  
 매개 변수 번호를 나타내는 **int**입니다.  
  
 *x*  
  
 Time 개체입니다.  
  
 *cal*  
  
 Calendar 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setTime 메서드는 java.sql.PreparedStatement 인터페이스의 setTime 메서드에 의해 지정됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0부터 이 메서드의 동작은 **sendTimeAsDatetime** 연결 속성([연결 속성 설정](../../../connect/jdbc/setting-the-connection-properties.md)) 및 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)에 의해 수정됩니다.  
  
 자세한 내용은 [java.sql.Time 값을 서버에 보내는 방식 구성](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [setTime 메서드&#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
