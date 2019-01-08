---
title: 가용성 그룹 (SQL Server)의 데이터베이스에 대 한 로그인 및 작업 관리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: d7da14d3-848c-44d4-8e49-d536a1158a61
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d8653161775a35e326a7ed85ed982f1cb75bee03
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53361496"
---
# <a name="management-of-logins-and-jobs-for-the-databases-of-an-availability-group-sql-server"></a>가용성 그룹의 데이터베이스에 대한 로그인 및 작업 관리(SQL Server)
  AlwaysOn 가용성 그룹의 모든 주 데이터베이스와 해당 보조 데이터베이스에서 동일한 사용자 로그인 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 작업 집합을 정기적으로 유지 관리해야 합니다. 로그인과 작업은 가용성 그룹에 대한 가용성 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 모든 인스턴스에서 재현되어야 합니다.  
  
-   **[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 작업**  
  
     원래 주 복제본을 호스팅하는 서버 인스턴스에서 원래 보조 복제본을 호스팅하는 서버 인스턴스로 관련 작업을 수동으로 복사해야 합니다. 주 데이터베이스에서만 즉, 로컬 복제본이 데이터베이스의 주 복제본일 때만 모든 데이터베이스에 대해 작업이 실행되도록 하는 논리를 각 관련 작업의 시작 부분에 추가해야 합니다.  
  
     가용성 그룹의 가용성 복제본을 호스팅하는 서버 인스턴스는 다른 테이프 드라이브 문자 등으로 다르게 구성될 수 있습니다. 각 가용성 복제본에 대한 작업 시 이러한 모든 차이점을 감안해야 합니다.  
  
     백업 작업은 [sys.fn_hadr_is_preferred_backup_replica](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql) 함수를 사용하여 가용성 그룹 백업 기본 설정에 따라 로컬 복제본이 기본 백업 복제본인지 여부를 확인합니다. [유지 관리 계획 마법사](../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md) 를 사용하여 만든 백업 작업은 이 함수를 사용합니다. 다른 백업 작업의 경우 백업 작업이 기본 복제본에서만 실행되도록 이 함수를 백업 작업의 조건으로 사용하는 것이 좋습니다. 자세한 내용은 참조 하세요. [ 활성 보조: 보조 복제본 (AlwaysOn 가용성 그룹)에 백업](availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)합니다.  
  
-   **로그인**  
  
     포함된 데이터베이스를 사용 중인 경우 데이터베이스에 포함된 사용자를 구성할 수 있습니다. 이러한 사용자에 대해서는 보조 복제본을 호스팅하는 서버 인스턴스에 대한 로그인을 만들 필요가 없습니다. 포함되지 않은 가용성 데이터베이스의 경우 가용성 복제본을 호스팅하는 서버 인스턴스에서 로그인 사용자를 만들어야 합니다. 자세한 내용은 [CREATE USER&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)를 참조하세요.  
  
     애플리케이션에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증 또는 로컬 Windows 로그인을 사용하는 경우 이 항목의 뒷부분에 나오는 [SQL Server 인증 또는 로컬 Windows 로그인을 사용하는 애플리케이션의 로그인](../../2014/database-engine/logins-and-jobs-for-availability-group-databases.md#SSauthentication)을 참조하십시오.  
  
    > [!NOTE]  
    >  SQL Server 로그인이 서버 인스턴스에서 정의되지 않았거나 잘못 정의되어 있는 데이터베이스 사용자는 이 인스턴스에 로그인할 수 없습니다. 이러한 사용자는 해당 서버 인스턴스에 있는 데이터베이스의 *분리된 사용자* 라고 합니다. 사용자가 지정된 서버 인스턴스에서 분리되어 있는 경우 언제든지 사용자 로그인을 설정할 수 있습니다. 자세한 내용은 [분리된 사용자 문제 해결&#40;SQL Server&#41;](../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)을 실행합니다.  
  
-   **추가 메타데이터**  
  
     로그인과 작업 외에도 지정된 가용성 그룹의 보조 복제본을 호스팅하는 각 서버 인스턴스에서 다시 만들어야 하는 정보가 있습니다. 예를 들어 서버 구성 설정, 자격 증명, 암호화된 데이터, 사용 권한, 복제 설정, Service Broker 애플리케이션, 트리거(서버 수준) 등을 다시 만들어야 할 수 있습니다. 자세한 내용은 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)을 참조하세요.  
  
##  <a name="SSauthentication"></a> SQL Server 인증 또는 로컬 Windows 로그인을 사용하는 응용 프로그램의 로그인  
 애플리케이션에서 SQL Server 인증 또는 로컬 Windows 로그인을 사용하는 경우 일치하지 않는 SID로 인해 원격 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에서 애플리케이션의 로그인이 확인되지 않을 수 있습니다. 일치하지 않는 SID로 인해 해당 로그인이 원격 서버 인스턴스에서 분리된 사용자가 됩니다. 이 문제는 애플리케이션이 장애 조치(Failover) 후 미러링된 데이터베이스 또는 로그 전달 데이터베이스에 연결하거나 백업에서 초기화된 복제 구독자 데이터베이스에 연결하는 경우에 발생할 수 있습니다.  
  
 이 문제를 방지하려면 원격 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에서 호스팅하는 데이터베이스를 사용하도록 애플리케이션을 설정할 때 예방 조치를 취하는 것이 좋습니다. 예방 조치에는 로컬 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 원격 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스로 로그인 및 암호를 전송하는 것이 포함됩니다. 이 문제를 방지하는 방법에 대한 자세한 내용은 KB 문서 918992([SQL Server 인스턴스 간에 로그인 및 암호를 전송하는 방법](https://support.microsoft.com/kb/918992/))를 참조하세요.  
  
> [!NOTE]  
>  이 문제는 다른 컴퓨터의 Windows 로컬 계정에 영향을 줍니다. 하지만 도메인 계정에서는 SID가 각 컴퓨터에서 동일하기 때문에 이러한 문제가 발생하지 않습니다.  
  
 자세한 내용은 [데이터베이스 미러링 및 로그 전달에서의 분리된 사용자](https://blogs.msdn.com/b/sqlserverfaq/archive/2009/04/13/orphaned-users-with-database-mirroring-and-log-shipping.aspx) (데이터베이스 엔진 블로그)를 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [로그인 만들기](../relational-databases/security/authentication-access/create-a-login.md)  
  
-   [Create a Database User](../relational-databases/security/authentication-access/create-a-database-user.md)입니다.  
  
-   [작업 만들기](../ssms/agent/create-a-job.md)  
  
-   [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [포함된 데이터베이스](../relational-databases/databases/contained-databases.md)   
 [작업 만들기](../ssms/agent/create-jobs.md)  
  
  
