---
title: registerOutParameter 메서드(int, int, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.registerOutParameter (int, int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3eb5c384-6751-4d50-be23-0c2ccc35593c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e661a6ed2dbc3f6503ca566ea8052edde735e415
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804831"
---
# <a name="registeroutparameter-method-int-int-javalangstring"></a>registerOutParameter 메서드(int, int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 서수 위치의 OUT 매개 변수를 지정된 JDBC 형식 및 형식 이름으로 등록합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void registerOutParameter(int index,  
                                 int sqlType,  
                                 java.lang.String typeName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *index*  
  
 매개 변수의 서수 위치를 나타내는 **int**입니다.  
  
 *sqlType*  
  
 java.sql.Types에 정의된 JDBC 형식 코드입니다.  
  
 *typeName*  
  
 정규화된 SQL 형식 이름이 들어 있는 **문자열**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 registerOutParameter 메서드는 java.sql.CallableStatement 인터페이스의 registerOutParameter 메서드에 의해 지정 됩니다.  
  
 부터는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0 때 *sqlType* 는이 메서드의 동작은 수정자 java.sql.types.time 형식이 합니다 **sendTimeAsDatetime** 연결 속성 ([연결 속성 설정](../../../connect/jdbc/setting-the-connection-properties.md)) 및 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)합니다.  
  
 자세한 내용은 [어떻게 구성 java.sql.Time 값을 서버로 전송 됩니다](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [registerOutParameter 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
