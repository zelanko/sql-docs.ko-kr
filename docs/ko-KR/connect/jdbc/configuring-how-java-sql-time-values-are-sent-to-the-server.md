---
title: Java.sql.Time 값이 서버에 전송 방법 구성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af4a3ebfb0ad5f9b425650d163390e39d05408a4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>java.sql.Time 값을 서버에 보내는 방식 구성
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Java.sql.Time 개체 또는 java.sql.Types.TIME JDBC 형식을 사용 하 여 매개 변수를 설정 하는 경우 java.sql.Time 값을 서버에 보내는 방식을 구성할 수 있습니다. 으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **시간** 형식 또는 **datetime** 유형입니다.  
  
 이 시나리오는 다음 메서드 중 하나를 사용할 때 적용됩니다.  
  
-   [SQLServerCallableStatement.registerOutParameter (int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int.md)  
  
-   [SQLServerCallableStatement.registerOutParameter (int, int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int-int.md)  
  
-   [SQLServerCallableStatement.setTime](../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setTime](../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)  
  
-   [SQLServerCallableStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)  
  
 사용 하 여 java.sql.Time 값을 보내는 방식을 구성할 수는 **sendTimeAsDatetime** 연결 속성입니다. 자세한 내용은 참조 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md)합니다.  
  
 값을 프로그래밍 방식으로 수정할 수 있습니다는 **sendTimeAsDatetime** 연결 속성에 [SQLServerDataSource.setSendTimeAsDatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)합니다.  
  
 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 이전의 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] 지원 하지 않습니다는 **시간** 데이터 형식이 있으므로 일반적으로 java.sql.Time을 사용 하 여 응용 프로그램 저장 java.sql.Time 값을 **datetime** 또는 **smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식입니다.  
  
 사용 하려는 경우는 **datetime** 및 **smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 설정 해야 java.sql.Time 값을 작업할 때의 데이터 형식에는 **sendTimeAsDatetime** 연결 속성을 **true**합니다. 사용 하려는 경우는 **시간** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식의 경우 java.sql.Time 값을 사용으로 설정 해야는 **sendTimeAsDatetime** 연결 속성을 **false**.  
  
 때 데이터 형식이 매개 변수에 java.sql.Time 값을 보내는 저장할 수도 기본 날짜가 날짜도 java.sql.Time 값을 보내는 하는 여부에 따라 다른는 수는 **datetime** (1/1/1970) 또는 **시간** (1/1/1900) 값입니다. 데이터를 보낼 때의 데이터 변환에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 참조 [를 사용 하 여 날짜 및 시간 데이터](http://go.microsoft.com/fwlink/?LinkID=145211)합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0에서는 **sendTimeAsDatetime** 은 기본적으로 true입니다. 이후 릴리스에서 **sendTimeAsDatetime** 연결 속성이 기본적으로 false로 설정할 수 있습니다.  
  
 응용 프로그램의 기본값에 관계 없이 예상 대로 작동 합니다. 계속 하려면는 **sendTimeAsDatetime** 연결 속성을 할 수 있습니다.  
  
-   작업할 경우 java.sql.Time을 사용 하 여는 **시간** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식입니다.  
  
-   작업할 경우 java.sql.Timestamp를 사용 하 여는 **datetime**, **smalldatetime**, 및 **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식입니다.  
  
Note 암호화 된 열에 시간 형식으로 날짜/시간 변환 지원 하지 않으므로 해당 sendTimeAsDatetime 암호화 된 열에 대해 false 이어야 합니다. SQL Server 용 Microsoft JDBC Driver 6.0부터, SQLServerConnection 클래스에 set/get sendTimeAsDatetime 속성의 값을 다음 두 가지 메서드가 있습니다.

```
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
