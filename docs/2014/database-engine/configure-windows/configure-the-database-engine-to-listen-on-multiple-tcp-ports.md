---
title: 여러 TCP 포트에서 수신 대기하도록 데이터베이스 엔진 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ports [SQL Server], multiple
- TDS
- listen on multiple ports
- endpoints [SQL Server], TDS
- adding ports
- tabular data stream
- multiple ports
ms.assetid: 8e955033-06ef-403f-b813-3d8241b62f1f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c5f3c354a36f5a3a62120ecc40a815420393648c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62811547"
---
# <a name="configure-the-database-engine-to-listen-on-multiple-tcp-ports"></a>여러 TCP 포트에서 수신하도록 데이터베이스 엔진 구성
  이 항목에서는 SQL Server 구성 관리자를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 여러 TCP 포트로 수신하도록 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 을 구성하는 방법에 대해 설명합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 TCP/IP가 설정된 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 IP 주소와 TCP 포트 번호로 구성된 연결 지점에서 들어오는 연결을 수신합니다. 다음 절차에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 추가 TCP 포트에서 수신할 수 있도록 TDS(Tabular Data Stream) 엔드포인트를 만듭니다.  
  
 두 번째 TDS 엔드포인트를 만드는 이유는 다음과 같습니다.  
  
-   특정 서브넷 상에서 로컬 클라이언트 컴퓨터의 기본 엔드포인트에 대한 액세스를 제한하도록 방화벽을 구성하여 보안을 향상시킵니다. 방화벽이 인터넷에 노출시키는 새로운 엔드포인트를 만들고 이 엔드포인트에 대한 연결 권한을 해당 서버 지원 팀으로만 제한하여 지원 팀이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 인터넷으로 액세스할 수 있도록 유지합니다.  
  
-   NUMA(Non-Uniform Memory Access)를 사용할 때 특정 프로세서에 대한 연결의 선호도를 설정합니다.  
  
 TDS 엔드포인트 구성은 실행 순서에 관계없이 다음 단계들로 구성됩니다.  
  
-   TCP 포트에 대한 TDS 엔드포인트를 만들고 적합한 경우 기본 엔드포인트에 대한 액세스를 복원합니다.  
  
-   원하는 서버 보안 주체에 엔드포인트에 대한 액세스를 부여합니다.  
  
-   선택한 IP 주소에 대한 TCP 포트 번호를 지정합니다.  
  
 기본 Windows 방화벽 설정 방법과 데이터베이스 엔진, Analysis Services, Reporting Services 및 Integration Services에 영향을 주는 TCP 포트에 대한 설명은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-create-a-tds-endpoint"></a>TDS 엔드포인트를 만들려면  
  
-   다음 문을 실행하여 서버에서 사용 가능한 모든 TCP 주소에 대해 포트 1500의 **CustomConnection** 이라는 엔드포인트를 만듭니다.  
  
    ```  
    USE master;  
    GO  
    CREATE ENDPOINT [CustomConnection]  
    STATE = STARTED  
    AS TCP  
       (LISTENER_PORT = 1500, LISTENER_IP =ALL)  
    FOR TSQL() ;  
    GO  
    ```  
  
 새로운 [!INCLUDE[tsql](../../includes/tsql-md.md)] 엔드포인트를 만들 때 **public** 에 대한 연결 권한은 기본 TDS 엔드포인트에 대해 취소됩니다. **public** 그룹에 대한 액세스에 기본 엔드포인트가 필요한 경우 `GRANT CONNECT ON ENDPOINT::[TSQL Default TCP] to [public];` 문을 사용하여 이 권한을 다시 적용합니다.  
  
#### <a name="to-grant-access-to-the-endpoint"></a>엔드포인트에 액세스를 부여하려면  
  
-   다음 문을 실행하여 **CustomConnection** 엔드포인트에 대한 액세스를 회사 도메인의 SQLSupport 그룹에 부여합니다.  
  
    ```  
    GRANT CONNECT ON ENDPOINT::[CustomConnection] to [corp\SQLSupport] ;  
    GO  
    ```  
  
#### <a name="to-configure-the-sql-server-database-engine-to-listen-on-an-additional-tcp-port"></a>추가 TCP 포트로 수신하도록 SQL Server 데이터베이스 엔진을 구성하려면  
  
1.  SQL Server 구성 관리자에서 **SQL Server 네트워크 구성**을 확장한 다음 _<instance_name>_**에 대한 프로토콜**을 클릭합니다.  
  
2.  _<instance_name>_**에 대한 프로토콜**을 확장한 다음 **TCP/IP**를 클릭합니다.  
  
3.  오른쪽 창에서 설정하려는 해제된 각 IP 주소를 마우스 오른쪽 단추로 클릭한 다음 **설정**을 클릭합니다.  
  
4.  **IPAll**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
5.  **TCP 포트** 상자에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 수신하려는 포트를 쉼표로 구분하여 입력합니다. 예제에서는 기본 포트 1433이 나열 된 경우 입력 `,1500` 상자에서 읽고 있으므로 `1433,1500`를 클릭 하 고 **확인**합니다.  
  
    > [!NOTE]  
    >  모든 IP 주소에 대한 포트를 설정하지 않으려면 원하는 주소에 대해서만 속성 상자에서 추가 포트로 구성하세요. 그런 다음 콘솔 창에서 **TCP/IP**를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭한 다음 **모두 수신합니다** 상자에서 **아니요**를 선택합니다.  
  
6.  왼쪽 창에서 **SQL Server 서비스**를 클릭하고  
  
7.  오른쪽 창에서 **SQL Server**_<instance_name>_ 을 마우스 오른쪽 단추로 클릭한 다음 **다시 시작**을 클릭합니다.  
  
     [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 다시 시작하면 오류 로그에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 수신 중인 포트 목록이 표시됩니다.  
  
#### <a name="to-connect-to-the-new-endpoint"></a>새 엔드포인트에 연결하려면  
  
-   다음 문을 실행하여 ACCT 서버에서 SQL Server의 기본 인스턴스에 대한 **CustomConnection** 엔드포인트에 신뢰할 수 있는 연결을 사용하여 연결합니다. 이때 사용자는 [corp\SQLSupport] 그룹의 멤버인 것으로 가정합니다.  
  
    ```  
    sqlcmd -SACCT,1500  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [CREATE ENDPOINT&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)   
 [DROP ENDPOINT&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-endpoint-transact-sql)   
 [GRANT 엔드포인트 사용 권한&#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql)   
 [NUMA 노드에 TCP IP 포트 매핑&#40;SQL Server&#41;](map-tcp-ip-ports-to-numa-nodes-sql-server.md)  
  
  
