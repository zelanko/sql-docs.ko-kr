---
title: "데이터베이스 미러링 (JDBC) 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4ff59218-0d3b-4274-b647-9839c4955865
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cdc263be0e8283ed1d71630a61f4e3d60406edc8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-database-mirroring-jdbc"></a>데이터베이스 미러링(JDBC) 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  데이터베이스 미러링은 데이터베이스 가용성과 데이터 중복을 증가시키기 위한 기본적인 소프트웨어 솔루션입니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 개발자 하지 않아도 모든 코드를 작성 하거나 데이터베이스에 대해 구성 된 경우 다른 조치를 취할 수 있도록 데이터베이스 미러링의에서는 암시적으로 지원 합니다.  
  
 복사본을 유지 하는 데이터베이스 미러링은 데이터베이스 단위로 구현 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 프로덕션 서버의 데이터베이스를 대기 합니다. 이 서버는 데이터베이스 미러링 세션의 구성 및 상태에 따라 핫 대기 서버나 웜 대기 서버가 됩니다. 핫 대기 서버에서는 커밋된 트랜잭션의 손실 없이 신속한 장애 조치가 가능하며, 웜 대기 서버에서는 데이터가 손실될 수 있는 강제 서비스를 지원합니다.  
  
 프로덕션 데이터베이스 라고는 *주* 데이터베이스와 대기 복사본 라고는 *미러* 데이터베이스입니다. 주 데이터베이스와 미러 데이터베이스의 개별 인스턴스에 있어야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] (서버 인스턴스) 가능한 경우 별도 컴퓨터에 있어야 합니다.  
  
 주 서버라고 부르는 프로덕션 서버 인스턴스는 미러 서버라고 부르는 대기 서버 인스턴스와 통신합니다. 주 서버 및 미러 서버는 데이터베이스 미러링 세션 내에서 파트너 역할을 합니다. 주 서버가 실패 하는 경우 미러 서버 라는 프로세스를 통해 주 데이터베이스에 해당 데이터베이스를 만들 수 *장애 조치*합니다. 예를 들어 서로 파트너 관계인 Partner_A와 Partner_B 서버가 있는데, 처음에 주 데이터베이스는 주 서버인 Partner_A에 상주하고 미러 데이터베이스는 미러 서버인 Partner_B에 상주한다고 가정합니다. Partner_A가 오프라인이 된 경우 Partner_B에 있는 데이터베이스가 장애 조치(Failover)되어 현재 주 데이터베이스가 될 수 있습니다. Partner_A가 미러링 세션에 다시 참여하면 Partner_A는 미러 서버가 되고 그 데이터베이스가 미러 데이터베이스가 됩니다.  
  
 Partner_A 서버가 회복할 수 없는 손상을 입은 경우 Partner_C 서버를 온라인으로 만들어 현재 주 서버인 Partner_B의 미러 서버 역할을 맡길 수 있습니다. 그러나 이 시나리오에서 연결 문자열 속성이 데이터베이스 미러링 구성에 사용된 새로운 서버 이름으로 업데이트되려면 클라이언트 응용 프로그램에 프로그래밍 논리가 포함되어야 합니다. 논리가 포함되지 않은 경우 서버 연결이 끊어질 수 있습니다.  
  
 대체 데이터베이스 미러링 구성은 성능 및 데이터 안전 수준이 다르며 지원되는 장애 조치(Failover) 형태도 다릅니다. 자세한 내용은 "데이터베이스 미러링 개요"의 참조 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="programming-considerations"></a>프로그래밍 고려 사항  
 주 데이터베이스 서버가 실패하면 클라이언트 응용 프로그램에서 API 호출에 대한 응답으로 오류를 받게 되는데, 이는 데이터베이스 연결이 끊어졌다는 의미입니다. 이러한 경우 커밋되지 않은 데이터베이스 변경 내용이 손실되고 현재 트랜잭션은 롤백됩니다. 또한 응용 프로그램에서는 연결을 종료하거나 데이터 원본 개체를 해제한 후 다시 연결을 시도해야 합니다. 이미 연결된 상태에서 클라이언트는 연결 문자열이나 데이터 원본 개체를 수정할 필요 없이 새로운 연결을 현재 주 서버 역할을 하고 있는 미러 데이터베이스로 위치를 변경합니다.  
  
 연결을 처음 설정하는 경우 주 서버는 장애 조치(failover) 파트너의 ID를 장애 조치 발생 시 사용할 클라이언트로 보냅니다. 응용 프로그램이 실패한 주 서버와 초기 연결을 설정하려는 경우 클라이언트는 장애 조치(failover) 파트너의 ID를 모릅니다. 클라이언트가이 시나리오에서는 failoverPartner 연결 문자열 속성으로 대처할 수 있도록 하 고 선택적으로 [setFailoverPartner](../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) 데이터 원본 메서드를 클라이언트가 장애 조치의 id를 지정 하는 데 사용 파트너에 게 고유 합니다. 클라이언트 속성은 이 시나리오에만 사용되며, 주 서버를 사용할 수 있을 경우에는 사용되지 않습니다.  
  
> [!NOTE]  
>  연결 문자열이나 데이터 원본 개체에 failoverPartner를 지정한 경우 databaseName 속성도 설정해야 하며 그렇지 않은 경우 예외가 발생합니다. failoverPartner 및 databaseName을 명시적으로 지정하지 않으면 응용 프로그램은 원래 데이터베이스 서버가 실패할 때 장애 조치를 시도하지 않습니다. 즉, 인식된 리디렉션은 failoverPartner 및 databaseName을 명시적으로 지정하는 연결에만 작동합니다. FailoverPartner 및 기타 연결 문자열 속성에 대 한 자세한 내용은 참조 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md)합니다.  
  
 클라이언트가 제공한 장애 조치(failover) 파트너 서버가 지정된 데이터베이스에 대한 장애 조치(failover) 파트너 역할을 하는 서버를 참조하지 않고 참조된 서버/데이터베이스가 미러링 배열로 되어 있는 경우 해당 서버에서 연결을 거부합니다. 하지만 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 클래스를 제공는 [getFailoverPartner](../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md) 메서드,이 메서드는 연결 문자열에 지정 된 장애 조치 파트너의 이름을 반환 또는 setFailoverPartner 메서드입니다. 현재 사용 중인 실제 장애 조치 파트너의 이름을 가져오려면 다음을 사용 하 여 [!INCLUDE[tsql](../../includes/tsql_md.md)] 문:  
  
```  
SELECT m.mirroring_role_DESC, m.mirroring_state_DESC,  
m.mirroring_partner_instance FROM sys.databases as db,  
sys.database_mirroring AS m WHERE db.name = 'MirroringDBName'  
AND db.database_id = m.database_id  
```  
  
> [!NOTE]  
>  미러링 데이터베이스의 이름을 사용하려면 이 문을 변경해야 합니다.  
  
 첫 번째 연결 시도가 실패한 경우 연결 문자열을 업데이트하거나 재시도 전략을 세우기 위해 파트너 정보를 캐싱하는 문제도 고려해야 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 주 서버에 첫 번째 연결을 시도합니다. 연결이 실패하고 예외가 발생하는 경우 새로운 주 서버로 승격된 적이 있었던 미러 서버로 연결을 시도합니다. 연결 문자열에서 failoverPartner 속성을 사용합니다.  
  
```  
import java.sql.*;  
  
public class clientFailover {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://serverA:1433;" +  
         "databaseName=AdventureWorks;integratedSecurity=true;" +  
         "failoverPartner=serverB";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
  
      try {  
         // Establish the connection to the principal server.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
         System.out.println("Connected to the principal server.");  
  
         // Note that if a failover of serverA occurs here, then an  
         // exception will be thrown and the failover partner will  
         // be used in the first catch block below.  
  
         // Create and execute an SQL statement that inserts some data.  
         stmt = con.createStatement();  
  
         // Note that the following statement assumes that the   
         // TestTable table has been created in the AdventureWorks  
         // sample database.  
         stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");  
      }  
  
      // Handle any errors that may have occurred.  
      catch (SQLException se) {  
         try {  
            // The connection to the principal server failed,  
            // try the mirror server which may now be the new  
            // principal server.  
            System.out.println("Connection to principal server failed, " +  
            "trying the mirror server.");  
            con = DriverManager.getConnection(connectionUrl);  
            System.out.println("Connected to the new principal server.");  
            stmt = con.createStatement();  
            stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");  
         }  
         catch (Exception e) {  
            e.printStackTrace();  
         }  
      }  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
      // Close the JDBC objects.  
      finally {  
         if (stmt != null) try { stmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  

