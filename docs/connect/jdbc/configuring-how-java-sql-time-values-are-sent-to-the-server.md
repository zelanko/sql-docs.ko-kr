---
title: java.sql.Time 값을 서버에 보내는 방식 구성 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 49925570b878bc442e10ab89e3eb9ef6694232d5
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797521"
---
# <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>java.sql.Time 값을 서버에 보내는 방식 구성
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  java.sql.Time 개체 또는 java.sql.Types.TIME JDBC 형식을 사용하여 매개 변수를 설정하는 경우 java.sql.Time 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **time** 형식 또는 **datetime** 형식으로 서버에 보내는 방식을 구성할 수 있습니다.  
  
 이 시나리오는 다음 메서드 중 하나를 사용할 때 적용됩니다.  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int.md)  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int-int.md)  
  
-   [SQLServerCallableStatement.setTime](../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setTime](../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)  
  
-   [SQLServerCallableStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)  
  
 **sendTimeAsDatetime** 연결 속성을 사용하여 java.sql.Time 값을 보내는 방식을 구성할 수 있습니다. 자세한 내용은 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)을 참조하세요.  
  
 [SQLServerDataSource.setSendTimeAsDatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)을 사용하여 **sendTimeAsDatetime** 연결 속성의 값을 프로그래밍 방식으로 수정할 수 있습니다.  
  
 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전의 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] 지원 하지 않습니다는 **시간** 데이터 형식, 일반적으로 java.sql.Time을 사용 하 여 응용 프로그램 저장 java.sql.Time 값으로 **datetime** 또는**smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다.  
  
 사용 하려는 경우는 **날짜/시간** 하 고 **smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정 해야 java.sql.Time 값을 사용 하 여 작업 하는 경우 데이터 형식에는 **sendTimeAsDatetime** 연결 속성을 **true**합니다. 사용 하려는 경우는 **시간** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식의 경우 설정 해야 java.sql.Time 값을 사용 합니다 **sendTimeAsDatetime** 연결 속성을 **false**.  
  
 날짜도 저장할 수 있는 데이터 형식의 매개 변수에 java.sql.Time 값을 보낼 시 java.sql.Time 값을 **datetime**(1/1/1970) 값으로 보내는지 아니면 **time**(1/1/1900) 값으로 보내는지에 따라 기본 날짜가 달라지므로 주의해야 합니다. 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 보낼 때의 데이터 변환에 대한 자세한 내용은 [날짜 및 시간 데이터 사용](https://go.microsoft.com/fwlink/?LinkID=145211)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0 **sendTimeAsDatetime** 은 기본적으로 true입니다. 후속 릴리스에서는 **sendTimeAsDatetime** 연결 속성이 기본적으로 false로 설정될 수 있습니다.  
  
 애플리케이션이 **sendTimeAsDatetime** 연결 속성의 기본값에 관계없이 계속해서 예상대로 작동하도록 하려면 다음과 같이 하면 됩니다.  
  
-   **time**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 사용하여 작업할 경우 java.sql.Time을 사용합니다.  
  
-   작업할 경우 java.sql.Timestamp를 사용 합니다 **날짜/시간**를 **smalldatetime**, 및 **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다.  
  
암호화 된 열에는 시간에서 날짜/시간 변환을 지원 하지 않습니다 SendTimeAsDatetime 암호화 된 열에 대해 false 이어야 합니다. SQL Server 용 Microsoft JDBC Driver 6.0부터 SQLServerConnection 클래스에 다음 두 가지 방법 sendTimeAsDatetime 속성의 값을 설정 및 가져오기

```java
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
