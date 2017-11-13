---
title: "Azure SQL 데이터베이스에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 49645b1f-39b1-4757-bda1-c51ebc375c34
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a6115941051862c9979db90b1aa8a58ac3c9b220
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-to-an-azure-sql-database"></a>Azure SQL 데이터베이스에 연결
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  사용 하는 경우이 항목에서는 문제를 설명는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 에 연결 하는 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]합니다. 에 연결 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]를 참조 하세요.  
  
-   [SQL Azure 데이터베이스](http://go.microsoft.com/fwlink/?LinkID=202490)  
  
-   [방법: JDBC를 사용 하 여 SQL Azure에 연결](http://msdn.microsoft.com/library/gg715284.aspx)  
  
-   [Java에서 SQL Azure를 사용 하 여](http://msdn.microsoft.com/library/windowsazure/hh749029(VS.103).aspx)

-   [Azure Active Directory 인증을 사용하여 연결](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)  
  
## <a name="details"></a>세부 정보  
 에 연결할 때는 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]를 호출 하려면 master 데이터베이스에 연결 해야 **SQLServerDatabaseMetaData.getCatalogs**합니다.  
 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]사용자 데이터베이스에서 카탈로그의 전체 집합을 반환을 지원 하지 않습니다. **SQLServerDatabaseMetaData.getCatalogs** 는 sys.databases 보기를 사용 하 여 카탈로그를 가져옵니다. 권한 설명을 참조 하십시오 [sys.databases (SQL Azure 데이터베이스)](http://go.microsoft.com/fwlink/?LinkId=217396) 이해 하려면 **SQLServerDatabaseMetaData.getCatalogs** 동작에는 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]합니다.  
  
 연결이 삭제됨  
 에 연결할 때는 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], 일정 한 비활성 기간 후 (예: 방화벽) 네트워크 구성 요소에서 유휴 연결을 종료할 수 있습니다. 유휴 연결에는  
  
-   네트워크 장치에서 연결을 삭제할 수 있는 TCP 계층에서 유휴 연결(Idle at the TCP layer) 및  
  
-   SQL Azure 게이트웨이에서 유휴 여기서 TCP **keepalive** (연결 TCP 쪽에서 유휴 상태 아님)을 구축한 발생 가능성이 있으 나 30 분간 활성 쿼리가 없는 합니다. 이 시나리오에서 게이트웨이가 TDS 연결이 30분간 유휴 상태이고 연결을 종료됨을 결정합니다.  
  
 네트워크 구성 요소에서 유휴 연결을 삭제하지 않도록 하려면 드라이버가 로드된 운영 체제에서 다음 레지스트리 설정(또는 Windows가 아닌 경우 이에 해당하는 설정)을 설정해야 합니다.  
  
|레지스트리 설정|권장 값|  
|----------------------|-----------------------|  
|HKEY_LOCAL_MACHINE \ 시스템 \ CurrentControlSet \ 서비스 \ t c \ 매개 변수 \ KeepAliveTime|30000|  
|HKEY_LOCAL_MACHINE \ 시스템 \ CurrentControlSet \ 서비스 \ t c \ 매개 변수 \ KeepAliveInterval|1000|  
|HKEY_LOCAL_MACHINE \ 시스템 \ CurrentControlSet \ 서비스 \ t c \ 매개 변수 \ TcpMaxDataRetransmissions|10|  
  
 그런 다음 레지스트리 설정을 적용하기 위해 컴퓨터를 다시 시작해야 합니다.  
  
 Windows 실행 시 이 작업을 수행하기 위해 Azure는 시작 태스크를 생성하여 레지스트리 키를 추가합니다.  예를 들어 다음과 같은 시작 태스크를 서비스 정의 파일에 추가합니다.  
  
```  
<Startup>  
    <Task commandLine="AddKeepAlive.cmd" executionContext="elevated" taskType="simple">  
    </Task>  
</Startup>  
```  
  
 그런 다음 프로젝트에 AddKeepAlive.cmd 파일을 추가합니다. "출력 디렉터리로 복사" 설정을 항상 복사로 설정합니다. 다음은 예제 AddKeepAlive.cmd 파일입니다.  
  
```  
if exist keepalive.txt goto done  
time /t > keepalive.txt  
REM Workaround for JDBC keep alive on SQL Azure  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveTime /t REG_DWORD /d 30000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveInterval /t REG_DWORD /d 1000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v TcpMaxDataRetransmissions /t REG_DWORD /d 10 >> keepalive.txt  
shutdown /r /t 1  
:done  
```  
  
 연결 문자열에서 서버 이름을 사용자 ID에 추가  
 4.0 버전 이전는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에 연결할 때는 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], 연결 문자열에 사용자 Id에 서버 이름을 추가 해야 합니다. user@servername)을 입력합니다. 4.0 버전부터는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 추가할 필요가 없게 되었습니다 @servername 을 연결 문자열에 사용자 Id입니다.  
  
 암호화 사용에 hostNameInCertificate 설정 필요  
 에 연결할 때는 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]를 지정 해야 **hostNameInCertificate** 지정 하는 경우 **암호화 = true**합니다. (서버 이름이 연결 문자열의 경우 *shortName*. *domainName*로 설정 된 **hostNameInCertificate** 속성을 \*. *domainName*.)  
  
 예를 들어  
  
```  
jdbc:sqlserver://abcd.int.mscds.com;databaseName= myDatabase;user=myName;password=myPassword;encrypt=true;hostNameInCertificate= *.int.mscds.com;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  

