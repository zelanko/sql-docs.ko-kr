---
title: MSSQLSERVER_1418 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1418 (Database Engine error)
ms.assetid: 6e9c7241-0201-44e0-9f8b-b3c4e293f0f6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c8f238589f0f9b6641095a4ccb65a4665300a28b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68023170"
---
# <a name="mssqlserver_1418"></a>MSSQLSERVER_1418
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|1418|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBM_PARTNERNOTFOUND|  
|메시지 텍스트|서버 네트워크 주소 "%.*ls"에 연결할 수 없거나 주소가 없습니다. 네트워크 주소 이름을 확인하고 로컬과 원격 엔드포인트에 대한 포트가 작동하는지 확인하세요.|  
  
## <a name="explanation"></a>설명  
지정된 서버 네트워크 주소에 연결할 수 없거나 주소가 존재하지 않으므로 서버 네트워크 엔드포인트가 응답하지 않았습니다.  
  
> [!NOTE]  
> 기본적으로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 운영 체제에서는 모든 포트를 차단합니다.  
  
## <a name="user-action"></a>사용자 동작  
네트워크 주소 이름을 확인하고 명령을 다시 실행하십시오.  
  
두 파트너에서 모두 수정 동작이 필요할 수 있습니다. 예를 들어 주 서버 인스턴스에서 SET PARTNER를 실행할 때 이 메시지가 발생하면 미러 서버 인스턴스에서만 수정 동작을 하면 되는 것으로 메시지가 표시되지만 실제로 두 파트너에서 모두 수정 동작이 필요할 수 있습니다.  
  
### <a name="additional-corrective-actions"></a>추가 수정 동작  
  
-   미러 데이터베이스의 미러링 준비가 완료되었는지 확인합니다.  
  
-   미러 서버 인스턴스의 이름과 포트가 올바른지 확인합니다.  
  
-   대상 미러 서버 인스턴스에 방화벽이 설정되어 있지 않은지 확인합니다.  
  
-   주 서버 인스턴스에 방화벽이 설정되어 있지 않은지 확인합니다.  
  
-   **sys.database_mirroring_endpoints** 카탈로그 뷰의 **state** 또는 **state_desc** 열을 사용하여 파트너에서 엔드포인트가 시작되었는지 확인합니다. 엔드포인트가 시작되지 않았으면 ALTER ENDPOINT 문을 실행하여 시작합니다.  
  
-   주 서버 인스턴스가 해당 데이터베이스 미러링 엔드포인트에 할당된 포트에서 수신하고 있는지, 미러 서버 인스턴스가 해당 포트에서 수신하고 있는지 확인합니다. 자세한 내용은 이 항목의 뒤에 나오는 "포트 가용성 확인"을 참조하십시오. 파트너가 할당된 포트에서 수신하고 있지 않으면 다른 포트에서 수신하도록 데이터베이스 미러링 엔드포인트를 수정합니다.  
  
    > [!IMPORTANT]  
    > 보안이 잘못 구성된 경우 일반적인 설치 오류 메시지가 발생할 수 있습니다. 일반적으로 서버 인스턴스는 잘못된 연결 요청에 응답하지 않고 이를 삭제합니다. 호출자에게는 미러 데이터베이스가 없거나 상태가 잘못되었거나, 사용 권한이 올바르지 않는 등의 여러 가지 이유로 보안 구성 오류가 발생한 것처럼 표시될 수 있습니다.  
  
### <a name="using-the-error-log-file-for-diagnosis"></a>진단을 위해 오류 로그 파일 사용  
오류 로그 파일만 검사할 수 있는 경우가 있습니다. 이 경우 데이터베이스 미러링 엔드포인트의 TCP 포트에 대한 오류 메시지 26023이 오류 로그에 포함되어 있는지 확인합니다. 심각도 16인 이 오류는 데이터베이스 미러링 엔드포인트가 시작되지 않았음을 나타낼 것입니다. **sys.database_mirroring_endpoints**에서 엔드포인트 상태를 시작됨으로 표시하는 경우에도 이 메시지가 표시될 수 있습니다.  
  
발생한 문제를 해결한 후 주 서버에서 ALTER DATABASE *database_name* SET PARTNER 문을 다시 실행합니다.  
  
### <a name="verifying-port-availability"></a>포트 가용성 확인  
네트워크에서 데이터베이스 미러링 세션을 구성할 때는 각 서버 인스턴스의 데이터베이스 미러링 엔드포인트가 데이터베이스 미러링 프로세스에만 사용되도록 하세요. 데이터베이스 미러링 엔드포인트에 할당된 포트에서 다른 프로세스가 수신할 경우 다른 서버 인스턴스의 데이터베이스 미러링 프로세스에서 해당 엔드포인트에 연결할 수 없습니다.  
  
Windows 기반 서버가 수신하고 있는 모든 포트를 표시하려면 **netstat** 명령 프롬프트 유틸리티를 사용합니다. **netstat** 구문은 Windows 운영 체제의 버전에 따라 달라집니다. 자세한 내용은 해당 운영 체제 설명서를 참조하십시오.  
  
#### <a name="windows-server-2003-service-pack-1-sp1"></a>Windows Server 2003 서비스 팩 1(SP1)  
수신 포트와 해당 포트가 열려 있는 프로세스를 나열하려면 Windows 명령 프롬프트에서 다음 명령을 입력합니다.  
  
**netstat -abn**  
  
#### <a name="windows-server-2003-pre-sp1"></a>Windows Server 2003(SP1 이전)  
수신 포트와 해당 포트가 열려 있는 프로세스를 식별하려면 다음 단계를 따르십시오.  
  
1.  프로세스 ID를 확인합니다.  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 프로세스 ID를 확인하려면 해당 인스턴스에 연결한 후 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```  
    SELECT SERVERPROPERTY('ProcessID')   
    ```  
  
    자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "SERVERPROPERTY(Transact-SQL)"를 참조하십시오.  
  
2.  다음 **netstat** 명령의 출력과 프로세스 ID를 일치시킵니다.  
  
    **netstat -ano**  
  
## <a name="see-also"></a>참고 항목  
[ALTER ENDPOINT&#40;Transact-SQL&#41;](~/t-sql/statements/alter-endpoint-transact-sql.md)  
[데이터베이스 미러링 엔드포인트&#40;SQL Server&#41;](~/database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
[미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](~/database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
[SERVERPROPERTY&#40;Transact-SQL&#41;](~/t-sql/functions/serverproperty-transact-sql.md)  
[서버 네트워크 주소 지정&#40;데이터베이스 미러링&#41;](~/database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
[sys.database_mirroring_endpoints&#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
[데이터베이스 미러링 구성 문제 해결&#40;SQL Server&#41;](~/database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
