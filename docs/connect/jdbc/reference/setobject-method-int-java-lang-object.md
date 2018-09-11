---
title: setObject 메서드 (int, java.lang.Object) | Microsoft Docs
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
- SQLServerPreparedStatement.setObject (int, java.lang.Object)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 61f19faa-3006-4a1c-974c-55951e3b3000
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cac0013c8867bce46dc9fd8ebbae9d0b0c487259
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785001"
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
  
## <a name="remarks"></a>Remarks  
 이 setObject 메서드는 java.sql.PreparedStatement 인터페이스의 setObject 메서드에 의해 지정 됩니다.  
  
 이 setObject 메서드를 호출하기 전에 응용 프로그램에서 다음 메서드 중 하나를 사용하여 지정된 매개 변수를 설정할 수도 있습니다.  
  
-   SQLServerPreparedStatement 클래스 또는 SQLServerCallableStatement 클래스의 set\<Type> 메서드  
  
-   SQLServerPreparedStatement 클래스 또는 SQLServerCallableStatement 클래스의 setNull 메서드  
  
-   합니다 [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) SQLServerCallableStatement 클래스의 메서드  
  
 이러한 경우 매개 변수 형식은 자동으로 설정됩니다. 응용 프로그램에서 obj 값 NULL을 사용하여 이 setObject 메서드를 호출할 경우 드라이버에서는 매개 변수 형식을 이전에 호출한 메서드에 의해 설정된 형식으로 가정합니다.  
  
 obj 값이 NULL이고 해당 매개 변수에 대한 형식 정보를 판별할 수 없는 경우 이 setObject 메서드는 지정된 매개 변수를 데이터베이스로 보내기 전에 CHAR로 변환합니다.  
  
 부터는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0에서는이 메서드는 수정자를 **sendTimeAsDatetime** 연결 속성 ([연결 속성 설정](../../../connect/jdbc/setting-the-connection-properties.md)) 및 [ SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)합니다.  
  
 자세한 내용은 [어떻게 구성 java.sql.Time 값을 서버로 전송 됩니다](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [setObject 메서드&#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
