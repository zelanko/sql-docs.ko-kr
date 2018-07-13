---
title: 단일 사용자 모드로 SQL Server 시작 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- starting SQL Server, single-user mode
- single-user mode [SQL Server]
ms.assetid: 72eb4fc1-7af4-4ec6-9e02-11a69e02748e
caps.latest.revision: 35
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5ba40d074b8782d4a0a34bd3e8e91cc27609a02b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185270"
---
# <a name="start-sql-server-in-single-user-mode"></a>단일 사용자 모드로 SQL Server 시작
  특정 상황에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시작 옵션 -m **을 사용하여**의 인스턴스를 단일 사용자 모드로 시작해야 합니다. 예를 들어 서버 구성 옵션을 변경하거나 손상된 master 데이터베이스 또는 다른 시스템 데이터베이스를 복구하려고 할 수도 있습니다. 두 가지 동작 모두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 단일 사용자 모드로 시작해야 합니다.  
  
 단일 사용자 모드로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 시작하면 컴퓨터에서 로컬 Administrators 그룹의 모든 멤버가 sysadmin 고정 서버 역할의 멤버로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있습니다. 자세한 내용은 [시스템 관리자가 잠겨 있는 경우 SQL Server에 연결](connect-to-sql-server-when-system-administrators-are-locked-out.md)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 단일 사용자 모드로 시작할 경우 다음에 유의하십시오.  
  
-   사용자 한 명만 서버에 연결할 수 있습니다.  
  
-   CHECKPOINT 프로세스는 실행되지 않습니다. 기본적으로 서버 시작 시 자동 실행됩니다.  
  
> [!NOTE]  
>  단일 사용자 모드로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 중단하십시오. 그렇지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스에서 해당 연결을 사용하므로 연결이 차단됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 단일 사용자 모드로 시작할 경우 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 수 있습니다. 개체 탐색기의 일부 작업에는 둘 이상의 연결이 필요하므로 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 개체 탐색기가 실패할 수도 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 단일 사용자 모드로 관리하려면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 의 쿼리 편집기를 통해서만 연결하여 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]문을 실행하거나 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)를 사용하세요.  
  
 **sqlcmd** 와 함께 **-m** 옵션을 사용하거나 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]을 사용할 경우 지정한 클라이언트 응용 프로그램에 대한 연결 수를 제한할 수 있습니다. 예를 들어 **-m"sqlcmd"** 는 연결 수를 단일 연결로 제한하며 이 경우 연결은 자신을 **sqlcmd** 클라이언트 프로그램으로 인식해야 합니다. 단일 사용자 모드에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 시작하며 알 수 없는 클라이언트 응용 프로그램에서 사용 가능한 유일한 연결을 사용할 경우 이 옵션을 사용합니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 쿼리 편집기를 통해 연결하려면 **-m"Microsoft SQL Server Management Studio - 쿼리"** 를 사용합니다.  
  
> [!IMPORTANT]  
>  이 옵션을 보안 용도로는 사용하지 마십시오. 클라이언트 응용 프로그램에서 클라이언트 응용 프로그램 이름을 제공하므로 연결 문자열의 일부로 잘못된 이름을 제공할 수 있습니다.  
  
## <a name="note-for-clustered-installations"></a>클러스터형 설치에 대한 참고 사항  
 클러스터 환경에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 단일 사용자 모드로 시작되면 클러스터 리소스 dll이 사용 가능한 모든 연결을 사용하므로 서버에 대한 다른 연결은 차단됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 이 상태이고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 리소스가 그룹에 영향을 주도록 구성되어 있는 경우 온라인으로 이 리소스를 가져오려고 하면 SQL 리소스가 다른 노드로 장애 조치(failover)될 수 있습니다.  
  
 이 문제를 해결하려면 다음 절차를 따릅니다.  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고급 속성에서 –m 시작 매개 변수를 제거합니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스를 오프라인 상태로 만듭니다.  
  
3.  이 그룹의 현재 소유자 노드에서 명령 프롬프트를 열고  
    net start MSSQLSERVER /m 명령을 실행합니다.  
  
4.  클러스터 관리자 또는 장애 조치(failover) 클러스터 관리 콘솔에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스가 여전히 오프라인 상태인지 확인합니다.  
  
5.  이제 SQLCMD -E -S\<servername> 명령을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하고 필요한 작업을 수행합니다.  
  
6.  작업이 완료되면 명령 프롬프트를 닫고 클러스터 관리자를 통해 SQL 및 기타 리소스를 다시 온라인 상태로 만듭니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트 서비스 시작, 중지 또는 일시 중지](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)   
 [데이터베이스 관리자를 위한 진단 연결](diagnostic-connection-for-database-administrators.md)   
 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)   
 [CHECKPOINT&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/checkpoint-transact-sql)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [데이터베이스 엔진 서비스 시작 옵션](database-engine-service-startup-options.md)  
  
  
