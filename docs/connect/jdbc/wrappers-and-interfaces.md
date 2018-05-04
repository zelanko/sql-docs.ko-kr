---
title: 래퍼 및 인터페이스 | Microsoft Docs
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
ms.assetid: 27fc9b72-9f21-4728-abcb-5c015f28a6ab
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1cee557293ccc5949977f0d3a9225ba0ea3d018d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="wrappers-and-interfaces"></a>래퍼 및 인터페이스
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 에 관련 된 JDBC API에 대 한 확장에 액세스는 클래스의 프록시를 만들 수 있는 지원 인터페이스 및 수 있는 래퍼는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 프록시 인터페이스를 통해 합니다.  
  
## <a name="wrappers"></a>래퍼  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] java.sql.Wrapper 인터페이스를 지원 합니다. 관련 된 JDBC API에 확장에 액세스할 수는 메커니즘을 제공 하는이 인터페이스는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 프록시 인터페이스를 통해 합니다.  
  
 두 메서드를 정의 하는 java.sql.Wrapper 인터페이스: **isWrapperFor** 및 **unwrap**합니다. **isWrapperFor** 메서드는 지정 된 입력된 개체가이 인터페이스를 구현 하는지 확인 합니다. **unwrap** 에 대 한 액세스를 허용 하려면이 인터페이스를 구현 하는 개체를 반환 하는 메서드는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 특정 메서드.  
  
 **isWrapperFor** 및 **unwrap** 메서드는 다음과 같이 노출 됩니다.  
  
-   [isWrapperFor 메서드 &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)  
  
-   [unwrap 메서드 &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)  
  
-   [isWrapperFor 메서드 &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)  
  
-   [unwrap 메서드 &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)  
  
-   [isWrapperFor 메서드 &#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)  
  
-   [unwrap 메서드 &#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)  
  
-   [isWrapperFor 메서드 &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)  
  
-   [unwrap 메서드 &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)  
  
-   [isWrapperFor 메서드 &#40;SQLServerStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)  
  
-   [unwrap 메서드 &#40;SQLServerStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)  
  
-   [isWrapperFor 메서드 &#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)  
  
-   [unwrap 메서드 &#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)  
  
## <a name="interfaces"></a>인터페이스  
 부터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0에서는 인터페이스는 관련된 클래스의 드라이버 관련 메서드에 액세스할 수 있는 응용 프로그램 서버에 사용할 수 있습니다. 응용 프로그램 서버를 노출 하는 프록시를 만들고 여 클래스를 래핑할 수는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]-인터페이스에서 특정 기능입니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 있는 인터페이스를 지원는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 관련 메서드와 상수가 응용 프로그램 서버 클래스의 프록시를 만들 수 있도록 합니다.  
  
 인터페이스는 표준 드라이버 특정 기능에 액세스에 대해 래핑 해제할 또는 일반 되 면 동일한 개체를 사용할 수 있도록 Java 인터페이스에서 파생 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 기능입니다.  
  
 다음 인터페이스가 추가되었습니다.  
  
-   [ISQLServerCallableStatement](../../connect/jdbc/reference/isqlservercallablestatement-interface.md)  
  
-   [ISQLServerConnection](../../connect/jdbc/reference/isqlserverconnection-interface.md)  
  
-   [ISQLServerDataSource](../../connect/jdbc/reference/isqlserverdatasource-interface.md)  
  
-   [ISQLServerPreparedStatement](../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
-   [ISQLServerResultSet](../../connect/jdbc/reference/isqlserverresultset-interface.md)  
  
-   [ISQLServerStatement](../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>Description  
 이 샘플에 액세스 하는 방법을 보여 줍니다는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]-DataSource 개체에서 특정 함수입니다. 응용 프로그램 서버에서이 데이터 원본 클래스 래핑 되었습니다. JDBC 드라이버 관련 함수나 상수에 액세스 하려면 unwrap ISQLServerDataSource 인터페이스 데이터 원본의 수 있으며이 인터페이스에서 선언 된 함수를 사용 하 여 키를 누릅니다.  
  
### <a name="code"></a>코드  
  
```  
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
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
