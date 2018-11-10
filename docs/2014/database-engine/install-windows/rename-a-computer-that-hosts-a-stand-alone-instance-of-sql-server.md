---
title: SQL Server의 독립 실행형 인스턴스를 호스팅하는 컴퓨터 이름 바꾸기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- remote login errors [SQL Server]
- standalone computer names [SQL Server]
- names [SQL Server], standalone instances of SQL Server
- renaming standalone instances of SQL Server
- sysservers system table
- removing remote logins
- deleting remote logins
- dropping remote logins
ms.assetid: bbaf1445-b8a2-4ebf-babe-17d8cf20b037
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e4e8026d5611b2f48ff622dd0b45e21a5f2c9c13
ms.sourcegitcommit: 87f29b23d5ab174248dab5d558830eeca2a6a0a4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51018908"
---
# <a name="rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server"></a>SQL Server의 독립 실행형 인스턴스를 호스팅하는 컴퓨터 이름 바꾸기
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 컴퓨터의 이름을 변경하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시작 시 새 이름이 인식됩니다. 컴퓨터 이름을 다시 설정하기 위해 설치 프로그램을 다시 실행할 필요는 없습니다. 대신 다음 단계를 사용하여 sys.servers에 저장되고 @@SERVERNAME 시스템 함수로 보고되는 시스템 메타데이터를 업데이트합니다. @@SERVERNAME을 사용하거나 sys.servers에서 서버 이름을 쿼리하는 응용 프로그램 및 원격 연결에 대해 변경된 컴퓨터 이름을 반영하도록 시스템 메타데이터를 업데이트합니다.  
  
 다음 단계는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 이름 변경 작업에 사용할 수 없습니다. 이 단계는 인스턴스 이름에서 컴퓨터 이름에 해당하는 부분을 변경하는 경우에만 사용할 수 있습니다. 예를 들어 Instance1이라는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 호스팅하는 MB1이라는 컴퓨터의 이름을 다른 이름(예: MB2)으로 변경할 수 있습니다. 그러나 이름에서 인스턴스에 해당하는 Instance1은 변경되지 않고 유지됩니다. 이 예제의 경우 \\\\*ComputerName*\\*InstanceName* 은 \\\MB1\Instance1에서 \\\MB2\Instance1로 변경됩니다.  
  
 **시작하기 전 주의 사항**  
  
 이름 바꾸기 프로세스를 시작하기 전에 다음 정보를 검토하십시오.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터의 일부인 경우 컴퓨터의 이름을 바꾸는 프로세스는 독립 실행형 인스턴스를 호스팅하는 컴퓨터의 이름을 바꾸는 프로세스와 다릅니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 복제와 함께 로그 전달을 사용하는 경우를 제외하고 복제에 관련된 컴퓨터의 이름 바꾸기를 지원하지 않습니다. 주 컴퓨터가 영구적으로 손실되면 로그 전달의 보조 컴퓨터 이름을 바꿀 수 있습니다. 자세한 내용은 [로그 전달 및 복제&#40;SQL Server&#41;](../log-shipping/log-shipping-and-replication-sql-server.md)를 참조하세요.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 사용하도록 구성된 컴퓨터의 이름을 바꾸면 컴퓨터 이름이 변경된 후 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 사용하지 못할 수 있습니다. 자세한 내용은 [보고서 서버 컴퓨터 이름 바꾸기](../../reporting-services/report-server/rename-a-report-server-computer.md)를 참조하세요.  
  
-   데이터베이스 미러링을 사용하도록 구성된 컴퓨터의 이름을 바꾸는 경우 이름 바꾸기 작업을 수행하기 전에 데이터베이스 미러링을 해제한 다음 데이터베이스 미러링을 새 컴퓨터 이름으로 다시 설정해야 합니다. 데이터베이스 미러링의 메타데이터는 새로운 컴퓨터 이름을 반영하도록 자동으로 업데이트되지 않습니다. 다음 단계에 따라 시스템 메타데이터를 업데이트하십시오.  
  
-   컴퓨터 이름에 대해 하드 코딩된 참조를 사용하는 Windows 그룹을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하는 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 수 없습니다. 이는 이름 바꾸기 후 Windows 그룹이 기존 컴퓨터 이름을 지정하는 경우에 발생할 수 있습니다. 이름 바꾸기 작업 후 Windows 그룹이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 연결되도록 하려면 새 컴퓨터 이름을 지정하도록 Windows 그룹을 업데이트해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버를 다시 시작하면 새 컴퓨터 이름을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 수 있습니다. @@SERVERNAME에서 로컬 서버 인스턴스의 업데이트된 이름을 반환하도록 하려면 시나리오에 적용되는 다음 절차를 직접 실행해야 합니다. 업데이트하는 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스를 호스팅하는지 아니면 명명된 인스턴스를 호스팅하는지 여부에 따라 사용할 절차가 달라집니다.  
  
### <a name="to-rename-a-computer-that-hosts-a-stand-alone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>다음의 독립 실행형 인스턴스를 호스트하는 컴퓨터의 이름을 바꾸려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스를 호스팅하는 컴퓨터의 이름이 바뀐 경우 다음 절차를 실행합니다.  
  
    ```  
    sp_dropserver <old_name>;  
    GO  
    sp_addserver <new_name>, local;  
    GO  
    ```  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 다시 시작합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 명명된 인스턴스를 호스팅하는 컴퓨터의 이름이 바뀐 경우 다음 절차를 실행합니다.  
  
    ```  
    sp_dropserver <old_name\instancename>;  
    GO  
    sp_addserver <new_name\instancename>, local;  
    GO  
    ```  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 다시 시작합니다.  
  
## <a name="after-the-renaming-operation"></a>이름 바꾸기 작업을 실행한 후  
 컴퓨터의 이름이 변경되면 이전 컴퓨터 이름을 사용하던 모든 연결은 새 이름을 사용하여 연결되어야 합니다.  
  
#### <a name="to-verify-that-the-renaming-operation-has-completed-successfully"></a>이름 바꾸기 작업이 성공적으로 완료되었는지 여부를 확인하려면  
  
-   @@SERVERNAME 또는 sys.servers에서 정보를 선택합니다. @@SERVERNAME 함수에서 새 이름을 반환하고, sys.servers 테이블에 새 이름이 표시됩니다. 다음 예제에서는 @@SERVERNAME의 사용을 보여 줍니다.  
  
    ```  
    SELECT @@SERVERNAME AS 'Server Name';  
    ```  
  
## <a name="additional-considerations"></a>기타 고려 사항  
 **원격 로그인** - 컴퓨터에서 원격 로그인을 사용하는 경우 **sp_dropserver** 를 실행하면 다음과 유사한 오류가 발생할 수 있습니다.  
  
 `Server: Msg 15190, Level 16, State 1, Procedure sp_dropserver, Line 44 There are still remote logins for the server 'SERVER1'.`  
  
 오류를 해결하려면 이 서버에 대한 원격 로그인을 삭제해야 합니다.  
  
#### <a name="to-drop-remote-logins"></a>원격 로그인을 삭제하려면  
  
-   기본 인스턴스의 경우 다음 프로시저를 실행합니다.  
  
    ```  
    sp_dropremotelogin old_name;  
    GO  
    ```  
  
-   명명된 인스턴스의 경우 다음 프로시저를 실행합니다.  
  
    ```  
    sp_dropremotelogin old_name\instancename;  
    GO  
    ```  
  
 **연결된 서버 구성** - 연결된 서버 구성은 컴퓨터 이름 바꾸기 작업의 영향을 받습니다. `sp_addlinkedserver` 또는 `sp_setnetname`을 사용하여 컴퓨터 이름 참조를 업데이트해야 합니다. 자세한 내용은 [sp_addlinkedserver&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql) 또는 [sp_setnetname&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-setnetname-transact-sql)을 참조하세요.  
  
 **클라이언트 별칭** - 명명된 파이프를 사용하는 클라이언트 별칭은 컴퓨터 이름 바꾸기 작업의 영향을 받습니다. 예를 들어 명명된 파이프 프로토콜을 사용하여 SRVR1을 가리키는 "PROD_SRVR"이라는 별칭을 만든 경우 파이프 이름은 `\\SRVR1\pipe\sql\query`와 같습니다. 컴퓨터의 이름을 바꾸면 명명된 파이프의 경로가 더 이상 유효하지 않습니다. 명명된 파이프에 대한 자세한 내용은 [명명된 파이프를 사용하여 유효한 연결 문자열 만들기](http://go.microsoft.com/fwlink/?LinkId=111063)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 2014 설치](../../database-engine/install-windows/install-sql-server.md)  
  
  
