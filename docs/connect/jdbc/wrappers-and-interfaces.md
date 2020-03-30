---
title: 래퍼 및 인터페이스 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 27fc9b72-9f21-4728-abcb-5c015f28a6ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3a74f5ccd8a36527dd7c37fc02150d11be632ba9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69025578"
---
# <a name="wrappers-and-interfaces"></a>래퍼 및 인터페이스

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 클래스의 프록시를 만들 수 있는 인터페이스와 프록시 인터페이스를 통해 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]와 관련된 JDBC API에 대한 확장에 액세스할 수 있도록 하는 래퍼를 지원합니다.

## <a name="wrappers"></a>래퍼

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 java.sql.Wrapper 인터페이스를 지원합니다. 이 인터페이스는 프록시 인터페이스를 통해 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]와 관련된 JDBC API에 대한 확장에 액세스할 수 있는 메커니즘을 제공합니다.

**IsWrapperFor** 인터페이스는 두 메서드인 및 **래핑**해제를 정의 합니다. **isWrapperFor** 메서드는 지정된 입력 개체가 이 인터페이스를 구현하는지 확인합니다. **unwrap** 메서드는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 관련 메서드에 액세스할 수 있도록 이 인터페이스를 구현하는 개체를 반환합니다.

**isWrapperFor** 및 **unwrap** 메서드는 다음과 같이 공개됩니다.

- [isWrapperFor 메서드&#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)

- [unwrap 메서드&#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)

- [isWrapperFor 메서드&#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)

- [unwrap 메서드&#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)

- [isWrapperFor 메서드&#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)

- [unwrap 메서드&#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)

- [isWrapperFor 메서드&#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)

- [unwrap 메서드&#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)

- [isWrapperFor 메서드&#40;SQLServerStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)

- [unwrap 메서드&#40;SQLServerStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)

- [isWrapperFor 메서드&#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)

- [unwrap 메서드&#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)

## <a name="interfaces"></a>인터페이스

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0부터 애플리케이션 서버는 인터페이스를 사용하여 관련 클래스의 드라이버 관련 메서드에 액세스할 수 있습니다. 애플리케이션 서버는 프록시를 만들고 인터페이스에서 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 관련 기능을 노출하여 클래스를 래핑할 수 있습니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 애플리케이션 서버가 클래스의 프록시를 만들 수 있도록 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 관련 메서드와 상수가 있는 인터페이스를 지원합니다.

인터페이스는 표준 Java 인터페이스에서 파생되므로 드라이버 관련 기능이나 제네릭 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 기능에 액세스하기 위해 래핑 해제되면 동일한 개체를 사용할 수 있습니다.

다음 인터페이스가 추가되었습니다.

- [ISQLServerCallableStatement](../../connect/jdbc/reference/isqlservercallablestatement-interface.md)

- [ISQLServerConnection](../../connect/jdbc/reference/isqlserverconnection-interface.md)

- [ISQLServerDataSource](../../connect/jdbc/reference/isqlserverdatasource-interface.md)

- [ISQLServerPreparedStatement](../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)

- [ISQLServerResultSet](../../connect/jdbc/reference/isqlserverresultset-interface.md)

- [ISQLServerStatement](../../connect/jdbc/reference/isqlserverstatement-interface.md)

## <a name="example"></a>예제

### <a name="description"></a>Description

이 샘플에서는 DataSource 개체에서 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 관련 함수에 액세스하는 방법을 보여 줍니다. 이 DataSource 클래스는 애플리케이션 서버에 의해 래핑되었을 수 있습니다. JDBC 드라이버 관련 함수나 상수에 액세스하려면 데이터 원본을 ISQLServerDataSource 인터페이스로 래핑 해제하고 이 인터페이스에서 선언된 함수를 사용할 수 있습니다.

### <a name="code"></a>코드

```java
import javax.sql.*;  
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  

public class UnWrapTest {  
   public static void main(String[] args) {  
      // This is a test.  This DataSource object could be something from an appserver
      // which has wrapped the real SQLServerDataSource with its own wrapper  
      SQLServerDataSource ds = new SQLServerDataSource();  
      checkSendStringParametersAsUnicode(ds);  
   }  

   // Unwrap to the ISQLServerDataSource interface to access the getSendStringParametersAsUnicode function  
   static void checkSendStringParametersAsUnicode(DataSource ds) {  
      try {  
         final ISQLServerDataSource sqlServerDataSource = ds.unwrap(ISQLServerDataSource.class);  
         boolean sendStringParametersAsUnicode = sqlServerDataSource.getSendStringParametersAsUnicode();  

         System.out.println("Send string as parameter value is:-" + sendStringParametersAsUnicode);  

      } catch (SQLException sqlE) {  
         System.out.println("Exception:-" + sqlE);  
      }  
   }  
}  
```

## <a name="see-also"></a>참고 항목

[JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
