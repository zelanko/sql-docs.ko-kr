---
title: 데이터베이스 미러링 (JDBC) 사용 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4ff59218-0d3b-4274-b647-9839c4955865
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4478c2799ddc23ce647c607466e0206f72ccf7b3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47638647"
---
# <a name="using-database-mirroring-jdbc"></a>데이터베이스 미러링(JDBC) 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

데이터베이스 미러링은 데이터베이스 가용성과 데이터 중복을 증가시키기 위한 기본적인 소프트웨어 솔루션입니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서는 데이터베이스 미러링을 암시적으로 지원하므로 데이터베이스에 대해 이 드라이버를 구성한 경우 개발자가 임의의 코드를 작성하거나 별도의 조치를 취할 필요가 없습니다.

데이터베이스 단위로 구현되는 데이터베이스 미러링은 대기 서버에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로덕션 데이터베이스의 복사본을 보관합니다. 이 서버는 데이터베이스 미러링 세션의 구성 및 상태에 따라 핫 대기 서버나 웜 대기 서버가 됩니다. 핫 대기 서버에서는 커밋된 트랜잭션의 손실 없이 신속한 장애 조치가 가능하며, 웜 대기 서버에서는 데이터가 손실될 수 있는 강제 서비스를 지원합니다.

프로덕션 데이터베이스는 _주_ 데이터베이스, 대기 복사본은 _미러_ 데이터베이스라고 부릅니다. 주 데이터베이스 및 미러 데이터베이스는 별도의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 개별 인스턴스(서버 인스턴스)에 있어야 하며, 가능한 한 별도의 컴퓨터에 있어야 합니다.

주 서버라고 부르는 프로덕션 서버 인스턴스는 미러 서버라고 부르는 대기 서버 인스턴스와 통신합니다. 주 서버 및 미러 서버는 데이터베이스 미러링 세션 내에서 파트너 역할을 합니다. 주 서버가 실패하면 미러 서버가 _장애 조치(failover)_ 라는 프로세스를 통해 자신의 데이터베이스를 주 데이터베이스로 만듭니다. 예를 들어 서로 파트너 관계인 Partner_A와 Partner_B 서버가 있는데, 처음에 주 데이터베이스는 주 서버인 Partner_A에 상주하고 미러 데이터베이스는 미러 서버인 Partner_B에 상주한다고 가정합니다. Partner_A가 오프라인이 된 경우 Partner_B에 있는 데이터베이스가 장애 조치(Failover)되어 현재 주 데이터베이스가 될 수 있습니다. Partner_A가 미러링 세션에 다시 참여하면 Partner_A는 미러 서버가 되고 그 데이터베이스가 미러 데이터베이스가 됩니다.

Partner_A 서버가 회복할 수 없는 손상을 입은 경우 Partner_C 서버를 온라인으로 만들어 현재 주 서버인 Partner_B의 미러 서버 역할을 맡길 수 있습니다. 그러나 이 시나리오에서 연결 문자열 속성이 데이터베이스 미러링 구성에 사용된 새로운 서버 이름으로 업데이트되려면 클라이언트 응용 프로그램에 프로그래밍 논리가 포함되어야 합니다. 논리가 포함되지 않은 경우 서버 연결이 끊어질 수 있습니다.

대체 데이터베이스 미러링 구성은 성능 및 데이터 안전 수준이 다르며 지원되는 장애 조치(Failover) 형태도 다릅니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "데이터베이스 미러링 개요"를 참조하세요.

## <a name="programming-considerations"></a>프로그래밍 고려 사항

주 데이터베이스 서버가 실패하면 클라이언트 응용 프로그램에서 API 호출에 대한 응답으로 오류를 받게 되는데, 이는 데이터베이스 연결이 끊어졌다는 의미입니다. 이러한 경우 커밋되지 않은 데이터베이스 변경 내용이 손실되고 현재 트랜잭션은 롤백됩니다. 또한 응용 프로그램에서는 연결을 종료하거나 데이터 원본 개체를 해제한 후 다시 연결을 시도해야 합니다. 연결 시 클라이언트가 연결 문자열이나 데이터 원본 개체를 수정할 필요 없이 새로운 연결이 현재 주 서버 역할을 하고 있는 미러 데이터베이스로 투명하게 리디렉션됩니다.

연결을 처음 설정하는 경우 주 서버는 장애 조치(failover) 파트너의 ID를 장애 조치 발생 시 사용할 클라이언트로 보냅니다. 응용 프로그램이 실패한 주 서버와 초기 연결을 설정하려는 경우 클라이언트는 장애 조치(failover) 파트너의 ID를 모릅니다. failoverPartner 연결 문자열 속성 및 [setFailoverPartner](../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) 데이터 원본 메서드(옵션)는 클라이언트가 본인의 장애 조치(failover) 파트너의 ID를 지정할 수 있게 허용하여 클라이언트가 이러한 시나리오에 대처할 수 있도록 합니다. 클라이언트 속성은 이 시나리오에만 사용되며, 주 서버를 사용할 수 있는 경우에는 사용되지 않습니다.

> [!NOTE]  
> 연결 문자열이나 데이터 원본 개체에 failoverPartner를 지정한 경우 databaseName 속성도 설정해야 하며 그렇지 않은 경우 예외가 발생합니다. failoverPartner 및 databaseName을 명시적으로 지정하지 않으면 응용 프로그램은 원래 데이터베이스 서버가 실패할 때 장애 조치를 시도하지 않습니다. 즉, 인식된 리디렉션은 failoverPartner 및 databaseName을 명시적으로 지정하는 연결에만 작동합니다. FailoverPartner 및 기타 연결 문자열 속성에 대 한 자세한 내용은 참조 하십시오 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)합니다.

클라이언트가 제공한 장애 조치(failover) 파트너 서버가 지정된 데이터베이스에 대한 장애 조치(failover) 파트너 역할을 하는 서버를 참조하지 않고 참조된 서버/데이터베이스가 미러링 배열로 되어 있는 경우 해당 서버에서 연결을 거부합니다. [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 클래스에서 [getFailoverPartner](../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md) 메서드를 제공하지만 이 메서드는 연결 문자열이나 setFailoverPartner 메서드에 지정된 장애 조치(failover) 파트너의 이름만을 반환합니다. 현재 사용 중인 실제 장애 조치(failover) 파트너의 이름을 검색하려면 다음과 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용합니다.

```sql
SELECT m.mirroring_role_DESC, m.mirroring_state_DESC,  
m.mirroring_partner_instance FROM sys.databases as db,  
sys.database_mirroring AS m WHERE db.name = 'MirroringDBName'  
AND db.database_id = m.database_id  
```

> [!NOTE]  
> 미러링 데이터베이스의 이름을 사용하려면 이 문을 변경해야 합니다.

첫 번째 연결 시도가 실패한 경우 연결 문자열을 업데이트하거나 재시도 전략을 세우기 위해 파트너 정보를 캐싱하는 문제도 고려해야 합니다.

## <a name="example"></a>예제

다음 예에서는 주 서버에 첫 번째 연결을 시도합니다. 연결이 실패하고 예외가 발생하는 경우 새로운 주 서버로 승격된 적이 있었던 미러 서버로 연결을 시도합니다. 연결 문자열에서 failoverPartner 속성을 사용합니다.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class ClientFailover {
    public static void main(String[] args) {

        String connectionUrl = "jdbc:sqlserver://serverA:1433;"
                + "databaseName=AdventureWorks;integratedSecurity=true;"
                + "failoverPartner=serverB";

        // Establish the connection to the principal server.
        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement();) {
            System.out.println("Connected to the principal server.");

            // Note that if a failover of serverA occurs here, then an
            // exception will be thrown and the failover partner will
            // be used in the first catch block below.

            // Execute a SQL statement that inserts some data.

            // Note that the following statement assumes that the
            // TestTable table has been created in the AdventureWorks
            // sample database.
            stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");
        }
        catch (SQLException se) {
            System.out.println("Connection to principal server failed, " + "trying the mirror server.");
            // The connection to the principal server failed,
            // try the mirror server which may now be the new
            // principal server.
            try (Connection con = DriverManager.getConnection(connectionUrl);
                    Statement stmt = con.createStatement();) {
                System.out.println("Connected to the new principal server.");
                stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");
            }
            // Handle any errors that may have occurred.
            catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

## <a name="see-also"></a>참고 항목

[JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
