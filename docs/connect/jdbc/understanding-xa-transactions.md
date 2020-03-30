---
title: XA 트랜잭션 이해 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 574e326f-0520-4003-bdf1-62d92c3db457
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e249bb515ca0a8b579e923e7d289fccd80ce6ef
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79286517"
---
# <a name="understanding-xa-transactions"></a>XA 트랜잭션 이해

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 Java Platform, Enterprise Edition/JDBC 2.0 분산 트랜잭션(옵션)을 지원합니다. [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) 클래스에서 가져온 JDBC 연결은 Java Platform, Enterprise Edition(Java EE) 애플리케이션 서버와 같은 표준 분산 트랜잭션 처리 환경에 참여할 수 있습니다.  

이 문서에서 XA는 확장 아키텍처를 나타냅니다.

> [!WARNING]  
> SQL용 Microsoft JDBC Driver 4.2 이상에서는 준비되지 않은 트랜잭션의 자동 롤백에 대한 기존 기능에 대해 새로운 제한 시간 옵션을 제공합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [준비되지 않은 트랜잭션의 자동 롤백에 대해 서버 쪽 제한 시간 설정 구성](../../connect/jdbc/understanding-xa-transactions.md#BKMK_ServerSide)을 참조하세요.  

## <a name="remarks"></a>설명

분산 트랜잭션을 구현하는 데 필요한 클래스는 다음과 같습니다.  
  
| 클래스                                              | 구현                      | Description                                       |
| -------------------------------------------------- | ------------------------------- | ------------------------------------------------- |
| com.microsoft.sqlserver.jdbc.SQLServerXADataSource | javax.sql.XADataSource          | 분산 연결용 클래스 팩터리입니다.    |
| com.microsoft.sqlserver.jdbc.SQLServerXAResource   | javax.transaction.xa.XAResource | 트랜잭션 관리자용 리소스 어댑터입니다. |
  
> [!NOTE]  
> XA 분산 트랜잭션 연결의 기본값은 커밋된 읽기 격리 수준입니다.  
  
## <a name="guidelines-and-limitations-when-using-xa-transactions"></a>XA 트랜잭션 사용과 관련된 지침 및 제한 사항  

다음은 밀접하게 결합된 트랜잭션에 적용되는 추가 지침입니다.  

- XA 트랜잭션을 MS DTC(Distributed Transaction Coordinator)와 함께 사용할 경우 MS DTC의 현재 버전이 밀접하게 결합된 XA 분기 동작을 지원하지 않습니다. 예를 들어 MS DTC에는 XID(XA 분기 트랜잭션 ID)와 MS DTC 트랜잭션 ID 간에 일 대 일 매핑이 있으며 느슨하게 연결된 XA 분기에서 수행되는 작업이 다른 작업과 격리됩니다.  
  
- 또한 MS DTC는 동일한 GTRID(전역 트랜잭션 ID)를 사용하는 여러 XA 분기가 단일 MS DTC 트랜잭션 ID에 매핑되는 긴밀하게 결합된 XA 분기를 지원합니다. 이러한 지원을 통해 밀접하게 결합된 XA 분기가 리소스 관리자에서 서로의 변경 내용을 확인할 수 있습니다(예: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]).
  
- [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) 플래그를 사용하면 애플리케이션에서 BQUAL(XA 분기 트랜잭션 ID)은 다르지만 GTRID(글로벌 트랜잭션 ID) 및 FormatID(형식 ID)는 동일한, 밀접하게 결합된 XA 트랜잭션을 사용할 수 있습니다. 이 기능을 사용하려면 XAResource.start 메서드의 flags 매개 변수에 [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)를 설정해야 합니다.
  
    ```java
    xaRes.start(xid, SQLServerXAResource.SSTRANSTIGHTLYCPLD);  
    ```  
  
## <a name="configuration-instructions"></a>구성 지침

MS DTC(Microsoft Distributed Transaction Coordinator)와 XA 데이터 원본을 함께 사용하여 분산 트랜잭션을 처리하려면 다음과 같은 단계가 필요합니다.  

> [!NOTE]  
> JDBC 분산 트랜잭션 구성 요소는 JDBC 드라이버 설치의 xa 디렉터리에 있습니다. 이 구성 요소에는 xa_install.sql 및 sqljdbc_xa.dll 파일이 포함됩니다.  

> [!NOTE]  
> SQL Server 2019 공개 미리 보기 CTP 2.0부터 JDBC XA 분산 트랜잭션 구성 요소는 SQL Server 엔진에 포함되며 시스템 저장 프로시저를 사용하여 사용하거나 사용하지 않도록 설정할 수 있습니다.
> JDBC 드라이버를 사용하여 XA 분산 트랜잭션을 수행하는 데 필요한 구성 요소를 사용하도록 설정하려면 다음 저장 프로시저를 실행합니다.
>
> EXEC sp_sqljdbc_xa_install
>
> 이전에 설치된 구성 요소를 사용하지 않도록 설정하려면 다음 저장 프로시저를 실행합니다.
>
> EXEC sp_sqljdbc_xa_uninstall

### <a name="running-the-ms-dtc-service"></a>MS DTC 서비스 실행

MS DTC 서비스는 서비스 관리자에서 **자동**으로 표시하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 시작할 때 자동으로 실행되도록 해야 합니다. XA 트랜잭션에 대해 MS DTC를 활성화하려면 다음 단계를 따릅니다.  
  
Windows Vista 이상:  
  
1. **시작** 단추를 클릭하고 **검색** 시작 상자에 **dcomcnfg**를 입력한 다음, ENTER를 눌러 **구성 요소 서비스**를 엽니다. **StartSearch** 상자에 %windir%\system32\comexp.msc를 입력하여 **구성 요소 서비스**를 열 수도 있습니다.  
  
2. 구성 요소 서비스, 컴퓨터, 내 컴퓨터를 확장한 다음 Distributed Transaction Coordinator를 확장합니다.  
  
3. **로컬 DTC**를 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.  
  
4. **로컬 DTC 속성** 대화 상자의 **보안** 탭을 클릭합니다.  
  
5. **XA 트랜잭션 사용** 확인란을 선택하고 **확인**을 클릭합니다. 이렇게 하면 MS DTC 서비스가 다시 시작됩니다.
  
6. **확인**을 다시 클릭하여 **속성** 대화 상자를 닫은 후 **구성 요소 서비스**를 닫습니다.  
  
7. 중지한 다음, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작하여 MS DTC 변경 내용과 동기화되도록 합니다.  

### <a name="configuring-the-jdbc-distributed-transaction-components"></a>JDBC 분산 트랜잭션 구성 요소 구성  

다음과 같은 단계를 통해 JDBC 드라이버 분산 트랜잭션 구성 요소를 구성할 수 있습니다.  
  
1. JDBC 드라이버 설치 디렉터리에 있는 새 sqljdbc_xa.dll을 분산 트랜잭션에 참여할 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터의 Binn 디렉터리에 복사합니다.  
  
    > [!NOTE]  
    > 32비트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 XA 트랜잭션을 사용할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 x64 프로세서에 설치되었더라도 x86 폴더에 있는 sqljdbc_xa.dll을 사용합니다. x64 프로세서의 64비트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 XA 트랜잭션을 사용할 경우 x64 폴더에 있는 sqljdbc_xa.dll을 사용합니다.  
  
2. 분산 트랜잭션에 참여할 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 데이터베이스 스크립트 xa_install.sql을 실행합니다. 이 스크립트는 sqljdbc_xa.dll에서 호출하는 확장 저장 프로시저를 설치합니다. 이 확장 저장 프로시저는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에 대한 분산 트랜잭션 및 XA 지원을 구현합니다. 이 스크립트를 실행하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 관리자 권한이 필요합니다.  
  
3. 특정 사용자에게 JDBC 드라이버를 통해 분산 트랜잭션에 참여할 권한을 부여하려면 해당 사용자를 SqlJDBCXAUser 역할에 추가합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스마다 한 번에 하나의 sqljdbc_xa.dll 어셈블리 버전만 구성할 수 있습니다. 애플리케이션에서 여러 버전의 JDBC 드라이버를 사용하여 XA 연결을 통해 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결해야 하는 경우가 있을 수 있습니다. 이 경우 최신 JDBC 드라이버와 함께 제공되는 sqljdbc_xa.dll을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 설치해야 합니다.  
  
현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 설치되어 있는 sqljdbc_xa.dll 버전은 다음 세 가지 방법으로 확인할 수 있습니다.
  
1. 분산 트랜잭션에 참여할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터의 LOG 디렉터리를 엽니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "ERRORLOG" 파일을 선택하여 엽니다. "ERRORLOG" 파일에서 "Using 'SQLJDBC_XA.dll' version ..." 구를 검색합니다.  
  
2. 분산 트랜잭션에 참여할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터의 Binn 디렉터리를 엽니다. sqljdbc_xa.dll 어셈블리를 선택합니다.

    - Windows Vista 이상: sqljdbc_xa.dll을 마우스 오른쪽 단추로 클릭한 다음 속성을 선택합니다. 그런 다음, **세부 정보** 탭을 클릭합니다. **파일 버전** 필드에는 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 설치되어 있는 sqljdbc_xa.dll 버전이 표시됩니다.  
  
3. 다음 섹션의 코드 예제에서와 같이 로깅 기능을 설정합니다. 출력 로그 파일에서 "Server XA DLL version:..." 구를 검색합니다.  

### <a name="configuring-server-side-timeout-settings-for-automatic-rollback-of-unprepared-transactions"></a><a name="BKMK_ServerSide"></a> 준비되지 않은 트랜잭션의 자동 롤백에 대해 서버 쪽 제한 시간 설정을 구성합니다.  

> [!WARNING]  
> 이 서버 쪽 옵션은 SQL Server용 Microsoft JDBC Driver 4.2 이상의 새로운 기능입니다. 업데이트된 동작을 가져오려면 서버의 sqljdbc_xa.dll이 업데이트되어야 합니다. 클라이언트 쪽 시간 제한 설정에 대한 자세한 내용은 [XAResource.setTransactionTimeout()](https://docs.oracle.com/javase/8/docs/api/javax/transaction/xa/XAResource.html)을 참조하세요.  

분산 트랜잭션의 제한 시간 동작을 제어하는 두 가지 레지스트리 설정(DWORD 값)이 있습니다.  
  
- **XADefaultTimeout**(초): 사용자가 제한 시간을 지정하지 않는 경우 사용할 기본 제한 시간 값입니다. 기본값은 0입니다.  
  
- **XAMaxTimeout**(초): 사용자가 설정할 수 있는 최대 제한 시간 값입니다. 기본값은 0입니다.  
  
이러한 설정은 SQL Server 인스턴스와 관련되며 다음 레지스트리 키 아래에 만들어야 합니다.  

```bash
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL<version>.<instance_name>\XATimeout  
```

> [!NOTE]  
> 64비트 컴퓨터에서 실행되는 32비트 SQL Server의 경우 다음 키 아래에 레지스트리 설정을 만들어야 합니다. `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Microsoft SQL Server\MSSQL<version>.<instance_name>\XATimeout`
  
시간 제한 값은 트랜잭션이 시작될 때 각 트랜잭션에 대해 설정되며, 시간 제한이 만료되면 SQL Server에서 트랜잭션을 롤백합니다. 제한 시간을 이러한 레지스트리 설정 및 사용자가 XAResource.setTransactionTimeout()을 통해 지정한 설정에 따라 결정됩니다. 이러한 제한 시간 값이 해석되는 방식에 대한 몇 가지 예제는 다음과 같습니다.  
  
- `XADefaultTimeout = 0`, `XAMaxTimeout = 0`
  
     기본 제한 시간 없음이 사용되고 최대 제한 시간 없음이 클라이언트에 적용됨을 의미합니다. 이 경우 클라이언트에서 XAResource.setTransactionTimeout을 사용하여 제한 시간을 설정하는 경우에만 트랜잭션의 제한 시간이 설정됩니다.  
  
- `XADefaultTimeout = 60`, `XAMaxTimeout = 0`
  
     클라이언트에서 시간 제한을 지정하지 않는 경우 모든 트랜잭션의 시간 제한이 60초가 됨을 의미합니다. 클라이언트에서 제한 시간을 지정하면 해당 제한 시간 값이 사용됩니다. 최대 제한 시간 값 없음이 적용됩니다.  
  
- `XADefaultTimeout = 30`, `XAMaxTimeout = 60`
  
     클라이언트에서 시간 제한을 지정하지 않는 경우 모든 트랜잭션의 시간 제한이 30초가 됨을 의미합니다. 클라이언트에서 시간 제한을 지정하면 60초(최댓값)보다 작은 경우에 한해 클라이언트의 시간 제한이 적용됩니다.  
  
- `XADefaultTimeout = 0`, `XAMaxTimeout = 30`
  
     클라이언트에서 제한 시간을 지정하지 않는 경우 모든 트랜잭션의 제한 시간이 30초(최대값)가 됨을 의미합니다. 클라이언트에서 시간 제한을 지정하면 30초(최댓값)보다 작은 경우에 한해 클라이언트의 시간 제한이 적용됩니다.  
  
### <a name="upgrading-sqljdbc_xadll"></a>sqljdbc_xa.dll 업그레이드

새 버전의 JDBC 드라이버를 설치할 때 서버에서 sqljdbc_xa.dll을 업그레이드하기 위해 새 버전의 sqljdbc_xa.dll을 사용해야 합니다.  
  
> [!IMPORTANT]  
> 유지 관리 창에 있는 동안 또는 MS DTC 트랜잭션을 진행하지 않을 때 sqljdbc_xa.dll을 업그레이드해야 합니다.
  
1. [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령 **DBCC sqljdbc_xa(무료)** 를 사용하여 sqljdbc_xa.dll을 언로드합니다.  
  
2. JDBC 드라이버 설치 디렉터리에 있는 새 sqljdbc_xa.dll을 분산 트랜잭션에 참여할 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터의 Binn 디렉터리에 복사합니다.  
  
    sqljdbc_xa.dll의 확장 프로시저가 호출되면 새 DLL이 로드됩니다. 새 정의를 로드하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작할 필요가 없습니다.  
  
### <a name="configuring-the-user-defined-roles"></a>사용자 정의 역할 구성

특정 사용자에게 JDBC 드라이버를 통해 분산 트랜잭션에 참여할 권한을 부여하려면 해당 사용자를 SqlJDBCXAUser 역할에 추가합니다. 예를 들어 다음과 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 사용하여 이름이 'shelby'(SQL 표준 로그인 사용자 이름)인 사용자를 SqlJDBCXAUser 역할에 추가합니다.  

```sql
USE master  
GO  
EXEC sp_grantdbaccess 'shelby', 'shelby'  
GO  
EXEC sp_addrolemember [SqlJDBCXAUser], 'shelby'  
```

SQL 사용자 정의 역할은 데이터베이스별로 정의합니다. 보안을 위해 고유한 역할을 만들려면 각 데이터베이스마다 역할을 정의하고 각 데이터베이스의 방식대로 사용자를 추가해야 합니다. SqlJDBCXAUser 역할은 master에 상주하는 SQL JDBC 확장 저장 프로시저에 대한 액세스 권한을 부여하는 데 사용되므로 master 데이터베이스에서만 정의할 수 있습니다. 먼저 개별 사용자에게 master에 대한 액세스 권한을 부여한 다음, master 데이터베이스에 로그인된 상태에서 SqlJDBCXAUser 역할에 대한 액세스 권한을 부여해야 합니다.  

## <a name="example"></a>예제  

```java
import java.net.Inet4Address;
import java.sql.*;
import java.util.Random;
import javax.sql.XAConnection;
import javax.transaction.xa.*;
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

        String connectionUrl = prefix + serverName + ":" + portNumber + ";databaseName=" + databaseName + ";user="
                + user + ";password=" + password;

        Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement()) {
            stmt.executeUpdate("CREATE TABLE XAMin (f1 int, f2 varchar(max))");

        }
        // Create the XA data source and XA ready connection.
        SQLServerXADataSource ds = new SQLServerXADataSource();
        ds.setUser(user);
        ds.setPassword(password);
        ds.setServerName(serverName);
        ds.setPortNumber(portNumber);
        ds.setDatabaseName(databaseName);

        XAConnection xaCon = ds.getXAConnection();
        try (Connection con = xaCon.getConnection()) {

            // Get a unique Xid object for testing.
            XAResource xaRes = null;
            Xid xid = null;
            xid = XidImpl.getUniqueXid(1);

            // Get the XAResource object and set the timeout value.
            xaRes = xaCon.getXAResource();
            xaRes.setTransactionTimeout(0);

            // Perform the XA transaction.
            System.out.println("Write -> xid = " + xid.toString());
            xaRes.start(xid, XAResource.TMNOFLAGS);
            PreparedStatement pstmt = con.prepareStatement("INSERT INTO XAMin (f1,f2) VALUES (?, ?)");
            pstmt.setInt(1, 1);
            pstmt.setString(2, xid.toString());
            pstmt.executeUpdate();

            // Commit the transaction.
            xaRes.end(xid, XAResource.TMSUCCESS);
            xaRes.commit(xid, true);
        }
        xaCon.close();

        // Open a new connection and read back the record to verify that it worked.
        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT * FROM XAMin")) {
            rs.next();
            System.out.println("Read -> xid = " + rs.getString(2));
            stmt.executeUpdate("DROP TABLE XAMin");
        }
    }
}


class XidImpl implements Xid {

    public int formatId;
    public byte[] gtrid;
    public byte[] bqual;

    public byte[] getGlobalTransactionId() {
        return gtrid;
    }

    public byte[] getBranchQualifier() {
        return bqual;
    }

    public int getFormatId() {
        return formatId;
    }

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
        for (int i = 0; i < gtrid.length; i++) {
            hexVal = gtrid[i] & 0xFF;
            if (hexVal < 0x10)
                sb.append("0" + Integer.toHexString(gtrid[i] & 0xFF));
            else
                sb.append(Integer.toHexString(gtrid[i] & 0xFF));
        }
        sb.append("} bqual(" + bqual.length + ")={0x");
        for (int i = 0; i < bqual.length; i++) {
            hexVal = bqual[i] & 0xFF;
            if (hexVal < 0x10)
                sb.append("0" + Integer.toHexString(bqual[i] & 0xFF));
            else
                sb.append(Integer.toHexString(bqual[i] & 0xFF));
        }
        sb.append("}");
        return sb.toString();
    }

    // Returns a globally unique transaction id.
    static byte[] localIP = null;
    static int txnUniqueID = 0;

    static Xid getUniqueXid(int tid) {

        Random rnd = new Random(System.currentTimeMillis());
        txnUniqueID++;
        int txnUID = txnUniqueID;
        int tidID = tid;
        int randID = rnd.nextInt();
        byte[] gtrid = new byte[64];
        byte[] bqual = new byte[64];
        if (null == localIP) {
            try {
                localIP = Inet4Address.getLocalHost().getAddress();
            } catch (Exception ex) {
                localIP = new byte[] {0x01, 0x02, 0x03, 0x04};
            }
        }
        System.arraycopy(localIP, 0, gtrid, 0, 4);
        System.arraycopy(localIP, 0, bqual, 0, 4);

        // Bytes 4 -> 7 - unique transaction id.
        // Bytes 8 ->11 - thread id.
        // Bytes 12->15 - random number generated by using seed from current time in milliseconds.
        for (int i = 0; i <= 3; i++) {
            gtrid[i + 4] = (byte) (txnUID % 0x100);
            bqual[i + 4] = (byte) (txnUID % 0x100);
            txnUID >>= 8;
            gtrid[i + 8] = (byte) (tidID % 0x100);
            bqual[i + 8] = (byte) (tidID % 0x100);
            tidID >>= 8;
            gtrid[i + 12] = (byte) (randID % 0x100);
            bqual[i + 12] = (byte) (randID % 0x100);
            randID >>= 8;
        }
        return new XidImpl(0x1234, gtrid, bqual);
    }
}

```

## <a name="see-also"></a>참고 항목  

[JDBC 드라이버로 트랜잭션 수행](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
