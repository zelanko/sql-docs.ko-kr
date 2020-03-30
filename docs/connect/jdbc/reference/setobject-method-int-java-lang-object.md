---
title: setObject 메서드(int, java.lang.Object) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setObject (int, java.lang.Object)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 61f19faa-3006-4a1c-974c-55951e3b3000
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e4ab210a30080472a777d151695a04ec49ff1041
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67973385"
---
# <a name="setobject-method-int-javalangobject"></a>setObject 메서드(int, java.lang.Object)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 개체를 사용하여 지정된 매개 변수의 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setObject(int index,  
                            java.lang.Object obj)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *index*  
  
 매개 변수 번호를 나타내는 **int**입니다.  
  
 *obj*  
  
 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setObject 메서드는 java.sql.PreparedStatement 인터페이스의 setObject 메서드에 의해 지정됩니다.  
  
 이 setObject 메서드를 호출하기 전에 애플리케이션에서 다음 메서드 중 하나를 사용하여 지정된 매개 변수를 설정할 수도 있습니다.  
  
-   SQLServerPreparedStatement 클래스 또는 SQLServerCallableStatement 클래스의 set\<Type> 메서드  
  
-   SQLServerPreparedStatement 클래스 또는 SQLServerCallableStatement 클래스의 setNull 메서드  
  
-   SQLServerCallableStatement 클래스의 [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 메서드  
  
 이러한 경우 매개 변수 형식은 자동으로 설정됩니다. 애플리케이션에서 obj 값 NULL을 사용하여 이 setObject 메서드를 호출할 경우 드라이버에서는 매개 변수 형식을 이전에 호출한 메서드에 의해 설정된 형식으로 가정합니다.  
  
 obj 값이 NULL이고 해당 매개 변수에 대한 형식 정보를 판별할 수 없는 경우 이 setObject 메서드는 지정된 매개 변수를 데이터베이스로 보내기 전에 CHAR로 변환합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0부터 이 메서드의 동작은 **sendTimeAsDatetime** 연결 속성([연결 속성 설정](../../../connect/jdbc/setting-the-connection-properties.md)) 및 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)에 의해 수정됩니다.  
  
 자세한 내용은 [java.sql.Time 값을 서버에 보내는 방식 구성](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [setObject 메서드&#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
