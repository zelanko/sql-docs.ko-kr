---
title: XA 트랜잭션 이해 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 574e326f-0520-4003-bdf1-62d92c3db457
caps.latest.revision: 80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a78fdb7edae90289d64d4c7fdf74ac3a12d4b115
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853048"
---
# <a name="understanding-xa-transactions"></a>XA 트랜잭션 이해
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Java platform, Enterprise Edition/JDBC 2.0 옵션 분산된 트랜잭션 지원을 제공 합니다. 가져온 JDBC 연결은 [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) 클래스 표준 분산된 트랜잭션 처리 Java Platform, Enterprise Edition (Java EE) 응용 프로그램 서버와 같은 환경에에서 참여할 수 있습니다.  
  
> [!WARNING]  
>  Microsoft JDBC Driver 4.2 (이상) SQL 준비 되지 않은 트랜잭션의 자동 롤백에 대 한 기존 기능에 대 한 새 제한 시간 옵션을 포함 합니다. 참조 [준비 되지 않은 트랜잭션의 자동 롤백에 대 한 서버 쪽 제한 시간 설정을 구성](../../connect/jdbc/understanding-xa-transactions.md#BKMK_ServerSide) 대 한 자세한 내용은이 항목의 뒷부분 합니다.  
  
## <a name="remarks"></a>주의  
 분산 트랜잭션을 구현하는 데 필요한 클래스는 다음과 같습니다.  
  
|클래스|구현|Description|  
|-----------|----------------|-----------------|  
|com.microsoft.sqlserver.jdbc.SQLServerXADataSource|javax.sql.XADataSource|분산 연결용 클래스 팩터리입니다.|  
|com.microsoft.sqlserver.jdbc.SQLServerXAResource|javax.transaction.xa.XAResource|트랜잭션 관리자용 리소스 어댑터입니다.|  
  
> [!NOTE]  
>  XA 분산 트랜잭션 연결의 기본값은 커밋된 읽기 격리 수준입니다.  
  
## <a name="guidelines-and-limitations-when-using-xa-transactions"></a>XA 트랜잭션 사용과 관련된 지침 및 제한 사항  
 다음은 밀접하게 결합된 트랜잭션에 적용되는 추가 지침입니다.  
  
-   XA 트랜잭션을 MS DTC(Microsoft Distributed Transaction Coordinator)와 함께 사용할 경우 MS DTC의 현재 버전이 밀접하게 결합된 XA 분기 동작을 지원하지 않습니다. 예를 들어 MS DTC에는 XID(XA 분기 트랜잭션 ID)와 MS DTC 트랜잭션 ID 간에 일 대 일 매핑이 있으며 느슨하게 연결된 XA 분기에서 수행되는 작업이 다른 작업과 격리됩니다.  
  
     제공 하는 핫픽스 [MSDTC 및 밀접 하 게 결합 된 트랜잭션에서](http://support.microsoft.com/kb/938653) 에서 지원할 수 있도록 동일한 ID GTRID (전역 트랜잭션)를 여러 개의 XA 분기가 있는 밀접 하 게 결합 된 XA 분기 단일 MS DTC 트랜잭션 ID에 매핑됩니다. 이러한 지원을 통해 밀접 하 게 연결된 하는 여러 개의 XA 분기가 같은 리소스 관리자에서 변경 서로 내용을 확인할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
-   A [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) 플래그를 사용 하면 bqual XA 분기 트랜잭션 Id () 다르지만 동일한 전역 트랜잭션 ID GTRID () 및 (formatid 형식) id 하 게 결합 된 XA 트랜잭션을 응용 프로그램을 사용할 수 있습니다. 이 기능을 사용 하려면 설정 해야 합니다는 [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) XAResource.start 메서드의 flags 매개 변수에서:  
  
    ```  
    xaRes.start(xid, SQLServerXAResource.SSTRANSTIGHTLYCPLD);  
    ```  
  
## <a name="configuration-instructions"></a>구성 지침  
 MS DTC(Microsoft Distributed Transaction Coordinator)와 XA 데이터 원본을 함께 사용하여 분산 트랜잭션을 처리하려면 다음과 같은 단계가 필요합니다.  
  
> [!NOTE]  
>  JDBC 분산 트랜잭션 구성 요소는 JDBC 드라이버 설치의 xa 디렉터리에 있습니다. 이 구성 요소에는 xa_install.sql 및 sqljdbc_xa.dll 파일이 포함됩니다.  
  
### <a name="running-the-ms-dtc-service"></a>MS DTC 서비스 실행  
 MS DTC 서비스를 표시 해야 **자동** 때 실행 되 고 있는지 확인 하려면 서비스 관리자에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 서비스를 시작 합니다. XA 트랜잭션에 대해 MS DTC를 활성화하려면 다음 단계를 따릅니다.  
  
 Windows Vista 이상:  
  
1.  클릭는 **시작** 단추, 입력 **dcomcnfg** 시작에서 **검색** 상자의 하 고 enter 키를 눌러 열려는 **구성 요소 서비스**합니다. 에 %windir%\system32\comexp.msc를 입력할 수도 있습니다는 **검색 시작** 상자를 열려면 **구성 요소 서비스**합니다.  
  
2.  구성 요소 서비스, 컴퓨터, 내 컴퓨터를 확장한 다음 Distributed Transaction Coordinator를 확장합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **로컬 DTC** 선택한 후 **속성**합니다.  
  
4.  클릭는 **보안** 탭에 **로컬 DTC 속성** 대화 상자.  
  
5.  선택 된 **XA 트랜잭션 사용** 확인란을 선택한 다음 클릭 **확인**합니다. 이렇게 하면 MS DTC 서비스가 다시 시작됩니다.  
  
6.  클릭 **확인** 를 다시 여 **속성** 대화 상자를 닫은 다음 **구성 요소 서비스**합니다.  
  
7.  중지 한 다음 다시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 되도록를 MS DTC 변경 내용과 동기화 되도록 하십시오.  
  
### <a name="configuring-the-jdbc-distributed-transaction-components"></a>JDBC 분산 트랜잭션 구성 요소 구성  
 다음과 같은 단계를 통해 JDBC 드라이버 분산 트랜잭션 구성 요소를 구성할 수 있습니다.  
  
1.  JDBC 드라이버 설치 디렉터리에서의 Binn 디렉터리에 있는 새 sqljdbc_xa.dll을 복사 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 분산 트랜잭션에 참여 하는 컴퓨터입니다.  
  
    > [!NOTE]  
    >  XA 트랜잭션을 32 비트를 사용할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], x86에 있는 sqljdbc_xa.dll을 사용 하 여 폴더, 경우에도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] x64에 설치 된 프로세서. XA 트랜잭션을 64 비트를 사용할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 는 x64 프로세서를 x64에 있는 sqljdbc_xa.dll을 사용 하 여 폴더입니다.  
  
2.  데이터베이스 스크립트 xa_install.sql을 실행 합니다. 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 분산 트랜잭션에 참여 하는 인스턴스입니다. 이 스크립트는 sqljdbc_xa.dll에서 호출하는 확장 저장 프로시저를 설치합니다. 이 확장 저장된 프로시저 분산된 트랜잭션 및 XA 지원을 구현에 대 한는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]합니다. 관리자 권한으로이 스크립트를 실행 해야 합니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스.  
  
3.  특정 사용자에게 JDBC 드라이버를 통해 분산 트랜잭션에 참여할 권한을 부여하려면 해당 사용자를 SqlJDBCXAUser 역할에 추가합니다.  
  
 각에 하나의 sqljdbc_xa.dll 어셈블리 버전만 구성할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스마다 한 번에 있습니다. 응용 프로그램은 동일 하 게 연결 하는 데 서로 다른 버전의 JDBC 드라이버를 사용 해야 할 수도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] XA 연결을 사용 하 여 인스턴스. 이 경우 최신 JDBC 드라이버에 오는 sqljdbc_xa.dll를에 설치 해야는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스.  
  
 Sqljdbc_xa.dll의 버전에 현재 설치 되었는지 확인 하는 방법은 세 가지가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스:  
  
1.  로그 디렉터리를 엽니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 분산 트랜잭션에 참여 하는 컴퓨터입니다. 선택 하 고 엽니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "ERRORLOG" 파일입니다. "ERRORLOG" 파일에서 "Using 'SQLJDBC_XA.dll' version ..." 구를 검색합니다.  
  
2.  Binn 디렉터리를 엽니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 분산 트랜잭션에 참여 하는 컴퓨터입니다. Sqljdbc_xa.dll 어셈블리를 선택 합니다.  
  
    -   Windows Vista 이상의 경우 sqljdbc_xa.dll을 마우스 오른쪽 단추로 클릭한 다음 속성을 선택합니다. 클릭는 **세부 정보** 탭 합니다. **파일 버전** 필드에 현재 설치 되어 있는 sqljdbc_xa.dll 버전이 표시는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스.  
  
3.  다음 섹션의 코드 예제에서와 같이 로깅 기능을 설정합니다. 출력 로그 파일에서 "Server XA DLL version:..." 구를 검색합니다.  
  
###  <a name="BKMK_ServerSide"></a> 준비 되지 않은 트랜잭션의 자동 롤백에 대 한 서버 쪽 제한 시간 설정 구성  
  
> [!WARNING]  
>  이 서버 쪽 옵션은 새 Microsoft JDBC Driver 4.2 (또는 이상) for SQL Server. 업데이트된 동작을 가져오려면 서버의 sqljdbc_xa.dll이 업데이트되어야 합니다. 클라이언트 쪽 제한 시간 설정에 대 한 자세한 내용은 참조 하십시오. [xaresource.settransactiontimeout ()](http://docs.oracle.com/javase/8/docs/api/javax/transaction/xa/XAResource.html)합니다.  
  
 분산 트랜잭션의 제한 시간 동작을 제어하는 두 가지 레지스트리 설정(DWORD 값)이 있습니다.  
  
-   **XADefaultTimeout** 초 단위로: 사용자 제한 시간을 지정 하지 않을 때 사용할 기본 제한 시간 값입니다. 기본값은 0입니다.  
  
-   **XAMaxTimeout** 초 단위로: 사용자가 설정할 수 있는 시간 제한의 최대값입니다. 기본값은 0입니다.  
  
 이러한 설정은 SQL Server 인스턴스와 관련되며 다음 레지스트리 키 아래에 만들어야 합니다.  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL\<**버전**>.\< *instance_name*> \XATimeout  
  
> [!NOTE]  
>  64 비트 컴퓨터에서 실행 중인 32 비트 SQL Server에 대 한 레지스트리 설정을 만들어야 다음 키 아래: HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Microsoft SQL Server\MSSQL\<버전 >. < c e _ > \ \ XATimeout  
  
 제한 시간 값은 트랜잭션이 시작되고 제한 시간이 만료되는 경우 SQL Server에 의해 롤백될 때 각 트랜잭션에 대해 설정됩니다. 제한 시간을 이러한 레지스트리 설정 및 사용자가 XAResource.setTransactionTimeout()을 통해 지정한 설정에 따라 결정됩니다. 이러한 제한 시간 값이 해석되는 방식에 대한 몇 가지 예제는 다음과 같습니다.  
  
-   XADefaultTimeout = 0, XAMaxTimeout = 0  
  
     기본 제한 시간 없음이 사용되고 최대 제한 시간 없음이 클라이언트에 적용됨을 의미합니다. 이 경우 클라이언트에서 XAResource.setTransactionTimeout을 사용하여 제한 시간을 설정하는 경우에만 트랜잭션의 제한 시간이 설정됩니다.  
  
-   XADefaultTimeout = 60, XAMaxTimeout = 0  
  
     클라이언트에서 제한 시간을 지정하지 않는 경우 모든 트랜잭션의 제한 시간이 60초가 됨을 의미합니다. 클라이언트에서 제한 시간을 지정하면 해당 제한 시간 값이 사용됩니다. 최대 제한 시간 값 없음이 적용됩니다.  
  
-   XADefaultTimeout = 30, XAMaxTimeout = 60  
  
     클라이언트에서 제한 시간을 지정하지 않는 경우 모든 트랜잭션의 제한 시간이 30초가 됨을 의미합니다. 클라이언트에서 제한 시간을 지정하면 60초(최대값)보다 작은 경우에 한해 클라이언트의 제한 시간이 사용됩니다.  
  
-   XADefaultTimeout = 0, XAMaxTimeout = 30  
  
     클라이언트에서 제한 시간을 지정하지 않는 경우 모든 트랜잭션의 제한 시간이 30초(최대값)가 됨을 의미합니다. 클라이언트에서 제한 시간을 지정하면 30초(최대값)보다 작은 경우에 한해 클라이언트의 제한 시간이 사용됩니다.  
  
### <a name="upgrading-sqljdbcxadll"></a>sqljdbc_xa.dll 업그레이드  
 새 버전의 JDBC 드라이버를 설치할 때 서버에서 sqljdbc_xa.dll을 업그레이드하기 위해 새 버전의 sqljdbc_xa.dll을 사용해야 합니다.  
  
> [!IMPORTANT]  
>  유지 관리 창에 있는 동안 또는 프로세스에 MS DTC 트랜잭션이 없을 때 sqljdbc_xa.dll을 업그레이드해야 합니다.  
  
1.  사용 하 여 sqljdbc_xa.dll을 언로드합니다는 [!INCLUDE[tsql](../../includes/tsql_md.md)] 명령 **DBCC sqljdbc_xa (FREE)** 합니다.  
  
2.  JDBC 드라이버 설치 디렉터리에서의 Binn 디렉터리에 있는 새 sqljdbc_xa.dll을 복사 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 분산 트랜잭션에 참여 하는 컴퓨터입니다.  
  
     sqljdbc_xa.dll의 확장 프로시저가 호출되면 새 DLL이 로드됩니다. 다시 시작할 필요가 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 새 정의 로드할 수 있습니다.  
  
### <a name="configuring-the-user-defined-roles"></a>사용자 정의 역할 구성  
 특정 사용자에게 JDBC 드라이버를 통해 분산 트랜잭션에 참여할 권한을 부여하려면 해당 사용자를 SqlJDBCXAUser 역할에 추가합니다. 예를 들어, 다음을 사용 하 여 [!INCLUDE[tsql](../../includes/tsql_md.md)] 이름이 'shelby' (SQL 표준 로그인 사용자 이름이 'shelby')는 사용자를 SqlJDBCXAUser 역할에 추가 하는 코드:  
  
```  
USE master  
GO  
EXEC sp_grantdbaccess 'shelby', 'shelby'  
GO  
EXEC sp_addrolemember [SqlJDBCXAUser], 'shelby'  
```  
  
 SQL 사용자 정의 역할은 데이터베이스별로 정의합니다. 보안을 위해 고유한 역할을 만들려면 각 데이터베이스마다 역할을 정의하고 각 데이터베이스의 방식대로 사용자를 추가해야 합니다. SqlJDBCXAUser 역할은 master에 상주하는 SQL JDBC 확장 저장 프로시저에 대한 액세스 권한을 부여하는 데 사용되므로 master 데이터베이스에서만 정의할 수 있습니다. 먼저 개별 사용자에게 master에 대한 액세스 권한을 부여한 다음 master 데이터베이스에 로그인된 상태에서 SqlJDBCXAUser 역할에 대한 액세스 권한을 부여해야 합니다.  
  
## <a name="example"></a>예제  
  
```  
import java.net.Inet4Address;  
import java.sql.*;  
import java.util.Random;  
import javax.transaction.xa.*;  
import javax.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  
  
public class testXA {  
  
   public static void main(String[] args) throws Exception {  
  
      // Create variables for the connection string.  
      String prefix = "jdbc:sqlserver://";  
      String serverName = "localhost";  
      int portNumber = 1433;  
      String databaseName = "AdventureWorks";   
      String user = "UserName";   
      String password = "*****";  
      String connectionUrl = prefix + serverName + ":" + portNumber  
         + ";databaseName=" + databaseName + ";user=" + user + ";password=" + password;  
  
      try {  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         Connection con = DriverManager.getConnection(connectionUrl);  
  
         // Create a test table.  
         Statement stmt = con.createStatement();  
         try {  
            stmt.executeUpdate("DROP TABLE XAMin");   
         }  
         catch (Exception e) {  
         }  
         stmt.executeUpdate("CREATE TABLE XAMin (f1 int, f2 varchar(max))");  
         stmt.close();  
         con.close();  
  
         // Create the XA data source and XA ready connection.  
         SQLServerXADataSource ds = new SQLServerXADataSource();  
         ds.setUser(user);  
         ds.setPassword(password);  
         ds.setServerName(serverName);  
         ds.setPortNumber(portNumber);  
         ds.setDatabaseName(databaseName);  
         XAConnection xaCon = ds.getXAConnection();  
         con = xaCon.getConnection();  
  
         // Get a unique Xid object for testing.  
         XAResource xaRes = null;  
         Xid xid = null;  
         xid = XidImpl.getUniqueXid(1);  
  
         // Get the XAResource object and set the timeout value.  
         xaRes = xaCon.getXAResource();  
         xaRes.setTransactionTimeout(0);  
  
         // Perform the XA transaction.  
         System.out.println("Write -> xid = " + xid.toString());  
         xaRes.start(xid,XAResource.TMNOFLAGS);  
         PreparedStatement pstmt =   
         con.prepareStatement("INSERT INTO XAMin (f1,f2) VALUES (?, ?)");  
         pstmt.setInt(1,1);  
         pstmt.setString(2,xid.toString());  
         pstmt.executeUpdate();  
  
         // Commit the transaction.  
         xaRes.end(xid,XAResource.TMSUCCESS);  
         xaRes.commit(xid,true);  
  
         // Cleanup.  
         con.close();  
         xaCon.close();  
  
         // Open a new connection and read back the record to verify that it worked.  
         con = DriverManager.getConnection(connectionUrl);  
         ResultSet rs = con.createStatement().executeQuery("SELECT * FROM XAMin");  
         rs.next();  
         System.out.println("Read -> xid = " + rs.getString(2));  
         rs.close();  
         con.close();  
      }   
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
  
class XidImpl implements Xid {  
  
   public int formatId;  
   public byte[] gtrid;  
   public byte[] bqual;  
   public byte[] getGlobalTransactionId() {return gtrid;}  
   public byte[] getBranchQualifier() {return bqual;}  
   public int getFormatId() {return formatId;}  
  
   XidImpl(int formatId, byte[] gtrid, byte[] bqual) {  
      this.formatId = formatId;  
      this.gtrid = gtrid;  
      this.bqual = bqual;  
   }  
  
   public String toString() {  
      int hexVal;  
      StringBuffer sb = new StringBuffer(512);  
      sb.append("formatId=" + formatId);  
      sb.append(" gtrid(" + gtrid.length + ")={0x");  
      for (int i=0; i<gtrid.length; i++) {  
         hexVal = gtrid[i]&0xFF;  
         if ( hexVal < 0x10 )  
            sb.append("0" + Integer.toHexString(gtrid[i]&0xFF));  
         else  
            sb.append(Integer.toHexString(gtrid[i]&0xFF));  
         }  
         sb.append("} bqual(" + bqual.length + ")={0x");  
         for (int i=0; i<bqual.length; i++) {  
            hexVal = bqual[i]&0xFF;  
            if ( hexVal < 0x10 )  
               sb.append("0" + Integer.toHexString(bqual[i]&0xFF));  
            else  
               sb.append(Integer.toHexString(bqual[i]&0xFF));  
         }  
         sb.append("}");  
         return sb.toString();  
      }  
  
      // Returns a globally unique transaction id.  
      static byte [] localIP = null;  
      static int txnUniqueID = 0;  
      static Xid getUniqueXid(int tid) {  
  
      Random rnd = new Random(System.currentTimeMillis());  
      txnUniqueID++;  
      int txnUID = txnUniqueID;  
      int tidID = tid;  
      int randID = rnd.nextInt();  
      byte[] gtrid = new byte[64];  
      byte[] bqual = new byte[64];  
      if ( null == localIP) {  
         try {  
            localIP = Inet4Address.getLocalHost().getAddress();  
         }  
         catch ( Exception ex ) {  
            localIP =  new byte[] { 0x01,0x02,0x03,0x04 };  
         }  
      }  
      System.arraycopy(localIP,0,gtrid,0,4);  
      System.arraycopy(localIP,0,bqual,0,4);  
  
      // Bytes 4 -> 7 - unique transaction id.  
      // Bytes 8 ->11 - thread id.  
      // Bytes 12->15 - random number generated by using seed from current time in milliseconds.  
      for (int i=0; i<=3; i++) {  
         gtrid[i+4] = (byte)(txnUID%0x100);  
         bqual[i+4] = (byte)(txnUID%0x100);  
         txnUID >>= 8;  
         gtrid[i+8] = (byte)(tidID%0x100);  
         bqual[i+8] = (byte)(tidID%0x100);  
         tidID >>= 8;  
         gtrid[i+12] = (byte)(randID%0x100);  
         bqual[i+12] = (byte)(randID%0x100);  
         randID >>= 8;  
      }  
      return new XidImpl(0x1234, gtrid, bqual);  
   }  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 트랜잭션 수행](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
