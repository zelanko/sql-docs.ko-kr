---
title: "setObject 메서드 (int, java.lang.Object) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerPreparedStatement.setObject (int, java.lang.Object)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 61f19faa-3006-4a1c-974c-55951e3b3000
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2116f0662e21e4cb38d60560a680e90e6b2321d9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

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
 *인덱스*  
  
 **int** 매개 변수 수를 나타내는입니다.  
  
 *obj*  
  
 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setObject 메서드는 java.sql.PreparedStatement 인터페이스의 setObject 메서드에 의해 지정 됩니다.  
  
 이 setObject 메서드를 호출 하기 전에 응용 프로그램 다음 방법 중 하나를 사용 하 여 지정된 된 매개 변수를 설정할 수 있습니다.  
  
-   집합\<유형 > SQLServerPreparedStatement 클래스 또는 SQLServerCallableStatement 클래스의 메서드  
  
-   SQLServerPreparedStatement 클래스 또는 SQLServerCallableStatement 클래스의 setNull 메서드  
  
-   [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) SQLServerCallableStatement 클래스의 메서드  
  
 이러한 경우 매개 변수 형식은 자동으로 설정됩니다. 응용 프로그램에서 obj 값 NULL로이 setObject 메서드를 호출할 경우 드라이버는 매개 변수 형식의 이전에 호출 된 메서드에 설정 된 이라고 가정 합니다.  
  
 Obj 값 NULL이 고 해당 매개 변수에 대 한 형식 정보를 확인할 수 있습니다 하는 경우이 setObject 메서드 지정된 된 매개 변수는 데이터베이스에 보내기 전에 CHAR 변환 합니다.  
  
 부터는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0에서는이 메서드의 동작은 의해 수정 되는 **sendTimeAsDatetime** 연결 속성 ([연결 속성을 설정할](../../../connect/jdbc/setting-the-connection-properties.md)) 및 [ SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)합니다.  
  
 자세한 내용은 참조 [구성 방법을 java.sql.Time 값에는 서버에 보내집니다](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setObject 메서드 &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

