---
title: "여러 TCP 포트에서 수신 대기하도록 데이터베이스 엔진 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ports [SQL Server], multiple
- TDS
- listen on multiple ports
- endpoints [SQL Server], TDS
- adding ports
- tabular data stream
- multiple ports
ms.assetid: 8e955033-06ef-403f-b813-3d8241b62f1f
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7cde3b735d73b7e7a53948a67e77e7f7ca07da43
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
---
# <a name="configure-the-database-engine-to-listen-on-multiple-tcp-ports"></a>여러 TCP 포트에서 수신하도록 데이터베이스 엔진 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 항목에서는 SQL Server 구성 관리자를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 여러 TCP 포트로 수신하도록 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 을 구성하는 방법에 대해 설명합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 TCP/IP가 설정된 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 IP 주소와 TCP 포트 번호로 구성된 연결 지점에서 들어오는 연결을 수신합니다. 다음 절차에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 추가 TCP 포트에서 수신할 수 있도록 TDS(Tabular Data Stream) 끝점을 만듭니다.  
  
 두 번째 TDS 끝점을 만드는 이유는 다음과 같습니다.  
  
-   특정 서브넷 상에서 로컬 클라이언트 컴퓨터의 기본 끝점에 대한 액세스를 제한하도록 방화벽을 구성하여 보안을 향상시킵니다. 방화벽이 인터넷에 노출시키는 새로운 끝점을 만들고 이 끝점에 대한 연결 권한을 해당 서버 지원 팀으로만 제한하여 지원 팀이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 인터넷으로 액세스할 수 있도록 유지합니다.  
  
-   NUMA(Non-Uniform Memory Access)를 사용할 때 특정 프로세서에 대한 연결의 선호도를 설정합니다.  
  
 TDS 끝점 구성은 실행 순서에 관계없이 다음 단계들로 구성됩니다.  
  
-   TCP 포트에 대한 TDS 끝점을 만들고 적합한 경우 기본 끝점에 대한 액세스를 복원합니다.  
  
-   원하는 서버 보안 주체에 끝점에 대한 액세스를 부여합니다.  
  
-   선택한 IP 주소에 대한 TCP 포트 번호를 지정합니다.  
  
 기본 Windows 방화벽 설정 방법과 데이터베이스 엔진, Analysis Services, Reporting Services 및 Integration Services에 영향을 주는 TCP 포트에 대한 설명은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-create-a-tds-endpoint"></a>TDS 끝점을 만들려면  
  
-   다음 문을 실행하여 서버에서 사용 가능한 모든 TCP 주소에 대해 포트 1500의 **CustomConnection** 이라는 끝점을 만듭니다.  
  
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
  
 새로운 [!INCLUDE[tsql](../../includes/tsql-md.md)] 끝점을 만들 때 **public** 에 대한 연결 권한은 기본 TDS 끝점에 대해 취소됩니다. **public** 그룹에 대한 액세스에 기본 끝점이 필요한 경우 `GRANT CONNECT ON ENDPOINT::[TSQL Default TCP] to [public];` 문을 사용하여 이 권한을 다시 적용합니다.  
  
#### <a name="to-grant-access-to-the-endpoint"></a>끝점에 액세스를 부여하려면  
  
-   다음 문을 실행하여 **CustomConnection** 끝점에 대한 액세스를 회사 도메인의 SQLSupport 그룹에 부여합니다.  
  
    ```  
    GRANT CONNECT ON ENDPOINT::[CustomConnection] to [corp\SQLSupport] ;  
    GO  
    ```  
  
#### <a name="to-configure-the-sql-server-database-engine-to-listen-on-an-additional-tcp-port"></a>추가 TCP 포트로 수신하도록 SQL Server 데이터베이스 엔진을 구성하려면  
  
1.  SQL Server 구성 관리자에서 **SQL Server 네트워크 구성**을 확장한 다음, *****<instance_name>에 대한 프로토콜*을 클릭합니다.  
  
2.  *****<instance_name>에 대한 프로토콜*을 확장한 다음, **TCP/IP**를 클릭합니다.  
  
3.  오른쪽 창에서 설정하려는 해제된 각 IP 주소를 마우스 오른쪽 단추로 클릭한 다음 **설정**을 클릭합니다.  
  
4.  **IPAll**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
5.  **TCP 포트** 상자에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 수신하려는 포트를 쉼표로 구분하여 입력합니다. 이 예제에서는 기본 포트 1433이 나열된 경우 **,1500** 을 입력하여 상자에 **1433,1500**이 표시되도록 한 다음 **확인**을 클릭합니다.  
  
    > [!NOTE]  
    >  모든 IP 주소에 대한 포트를 설정하지 않으려면 원하는 주소에 대해서만 속성 상자에서 추가 포트로 구성하세요. 그런 다음 콘솔 창에서 **TCP/IP**를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭한 다음 **모두 수신합니다** 상자에서 **아니요**를 선택합니다.  
  
6.  왼쪽 창에서 **SQL Server 서비스**를 클릭하고  
  
7.  오른쪽 창에서 *SQL Server***<instance_name>*을 마우스 오른쪽 단추로 클릭한 다음, **다시 시작**을 클릭합니다.  
  
     [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 다시 시작하면 오류 로그에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 수신 중인 포트 목록이 표시됩니다.  
  
#### <a name="to-connect-to-the-new-endpoint"></a>새 끝점에 연결하려면  
  
-   다음 문을 실행하여 ACCT 서버에서 SQL Server의 기본 인스턴스에 대한 **CustomConnection** 끝점에 신뢰할 수 있는 연결을 사용하여 연결합니다. 이때 사용자는 [corp\SQLSupport] 그룹의 멤버인 것으로 가정합니다.  
  
    ```  
    sqlcmd -SACCT,1500  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [DROP ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/drop-endpoint-transact-sql.md)   
 [GRANT 끝점 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)   
 [NUMA 노드에 TCP IP 포트 매핑&#40;SQL Server&#41;](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)  
  
  
