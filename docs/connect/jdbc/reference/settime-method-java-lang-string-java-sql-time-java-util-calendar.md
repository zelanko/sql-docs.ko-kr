---
title: setTime 메서드를 시간 및 일정 값으로 Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setTime (java.lang.String, java.lang.Time, java.lang.Calendar))
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ca08fea8-ee1a-49e4-a973-2923d325df79
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e0a493492c581150809fee6e3707cf770960462
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972528"
---
# <a name="settime-method-javalangstring-javasqltime-javautilcalendar"></a>setTime 메서드(java.lang.String, java.sql.Time, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 시간 및 달력 값으로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setTime(java.lang.String sCol,  
                    java.sql.Time x,  
                    java.util.Calendar c)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
 *x*  
  
 시간 개체입니다.  
  
 *c*  
  
 일정 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 setTime 메서드는 java.sql.CallableStatement 인터페이스의 setTime 메서드에 의해 지정됩니다.  
  
 JDBC 드라이버 3.0부터이 메서드의 동작은 **sendTimeAsDatetime** connection 속성 ([연결 속성 설정](../../../connect/jdbc/setting-the-connection-properties.md))에 의해 수정 됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [SQLServerDataSource. setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 자세한 내용은 [java. 시간 값을 서버로 보내는 방법 구성](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [setTime 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
