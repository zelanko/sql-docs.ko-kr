---
title: "SQL Server Audit(데이터베이스 엔진) | Microsoft 문서"
ms.custom: 
ms.date: 11/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- audit
helpviewer_keywords:
- SQL Server Audit
- audits [SQL Server], SQL Server Audit
ms.assetid: 0c1fca2e-f22b-4fe8-806f-c87806664f00
caps.latest.revision: 58
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f00c5db3574f21010e682f964d06f3c2b61a1d09
ms.openlocfilehash: 7852b00948b193a07e4ac38d1ace6135a63bc599
ms.contentlocale: ko-kr
ms.lasthandoff: 04/29/2017

---
# <a name="sql-server-audit-database-engine"></a>SQL Server Audit(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  *인스턴스 또는 개별 데이터베이스를* 감사 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] 할 때는 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]에서 발생하는 이벤트를 추적 및 기록합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit에서는 서버 수준 이벤트에 대한 서버 감사 사양과 데이터베이스 수준 이벤트에 대한 데이터베이스 감사 사양을 포함하는 서버 감사를 생성할 수 있습니다. 감사된 이벤트는 이벤트 로그 또는 감사 파일에 쓸 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 감사는 설치에 대한 정부 또는 표준 요구 사항에 따라 여러 개의 수준이 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit에서는 다양한 서버 및 데이터베이스 개체에 대한 감사를 사용 및 저장하거나 보는 데 필요한 도구와 프로세스를 제공합니다.  
  
 인스턴스별 서버 감사 동작 그룹을 기록할 수 있으며 데이터베이스별 데이터베이스 감사 동작 그룹 또는 데이터베이스 감사 동작을 기록할 수 있습니다. 감사 가능한 동작이 발생할 때마다 감사 이벤트가 발생합니다.  
  
 모든 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 서버 수준 감사를 지원합니다. [!INCLUDE[ssSQL15_md](../../../includes/sssql15-md.md)] SP1부터 모든 버전에서 데이터베이스 수준 감사를 지원합니다. 이전에는 데이터베이스 수준 감사가 Enterprise, Developer 및 Evaluation 버전에서만 지원되었습니다. 자세한 내용은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
> [!NOTE]  
>  이 항목의 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 적용됩니다.  [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]의 경우 [SQL 데이터베이스 감사 시작](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)을 참조하세요.  
  
## <a name="sql-server-audit-components"></a>SQL Server Audit 구성 요소  
 *감사* 는 특정 서버 동작 또는 데이터베이스 동작 그룹에 대한 여러 요소를 하나의 패키지로 결합한 것입니다. 보고서 정의가 그래픽 및 데이터 요소와 결합되어 보고서가 생성되는 것처럼 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit의 구성 요소가 결합되어 감사가 만들어집니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit에서는 감사를 만들기 위해 *확장 이벤트* 를 사용합니다. 확장 이벤트에 대한 자세한 내용은 [확장 이벤트](../../../relational-databases/extended-events/extended-events.md)를 참조하세요.  
  
### <a name="sql-server-audit"></a>SQL Server Audit  
 *SQL Server Audit* 개체는 사용자가 모니터링하려는 서버 또는 데이터베이스 수준 동작 및 동작 그룹에 대한 하나의 인스턴스를 수집합니다. 감사는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 수준으로 존재합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스별로 여러 개의 감사를 가질 수 있습니다.  
  
 감사를 정의할 때 결과 출력 위치를 지정하는데 이를 감사 대상이라고 합니다. 감사가 *비활성* 상태로 생성되면 동작을 자동으로 감사하지 않습니다. 감사가 활성화되면 감사 대상이 감사로부터 데이터를 수신합니다.  
  
### <a name="server-audit-specification"></a>서버 감사 사양  
 *서버 감사 사양* 개체는 감사에 속해 있습니다. 서버 감사 사양과 감사는 모두 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 범위에서 생성되므로 감사당 하나의 서버 감사 사양을 만들 수 있습니다.  
  
 서버 감사 사양은 확장 이벤트 기능에 의해 발생되는 수많은 서버 수준 동작 그룹을 수집합니다. *감사 동작 그룹* 을 서버 감사 사양에 추가할 수 있습니다. 감사 동작 그룹은 미리 정의된 동작 그룹이며 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]에서 발생하는 원자성 이벤트입니다. 이러한 동작은 감사로 전달되어 대상에 기록됩니다.  
  
 서버 수준 감사 동작 그룹 및 감사 동작은 [SQL Server 감사 동작 그룹 및 동작](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)항목에 설명되어 있습니다.  
  
### <a name="database-audit-specification"></a>데이터베이스 감사 사양  
 *데이터베이스 감사 사양* 개체도 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit에 속해 있습니다. 감사의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스당 하나의 데이터베이스 감사 사양을 만들 수 있습니다.  
  
 데이터베이스 감사 사양은 확장 이벤트 기능에 의해 발생되는 데이터베이스 수준 감사 동작을 수집합니다. 감사 동작 그룹 또는 감사 이벤트를 데이터베이스 감사 사양에 추가할 수 있습니다. *감사 이벤트* 는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 엔진이 감사할 수 있는 원자성 동작이고, *감사 동작 그룹* 은 미리 정의된 동작 그룹입니다. 둘 다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스 범위에 존재합니다. 이러한 동작은 감사로 전달되어 대상에 기록됩니다. 시스템 뷰와 같은 서버 범위 개체는 사용자 데이터베이스 감사 사양에 포함하지 마십시오.  
  
 데이터베이스 수준 감사 동작 그룹 및 감사 동작은 [SQL Server 감사 동작 그룹 및 동작](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)항목에 설명되어 있습니다.  
  
### <a name="target"></a>대상  
 감사의 결과는 파일, Windows 보안 이벤트 로그 또는 Windows 응용 프로그램 이벤트 로그 형태로 대상에 전달됩니다. 로그를 정기적으로 검토 및 보관하여 대상에 추가 레코드를 작성할 공간이 충분한지를 확인해야 합니다.  
  
> [!IMPORTANT]  
>  허가 받은 사용자는 Windows 응용 프로그램 이벤트 로그에 대해 읽기/쓰기 작업이 가능합니다. 응용 프로그램 이벤트 로그는 Windows 보안 이벤트 로그보다 낮은 권한을 요구하므로 Windows 보안 이벤트 로그보다 보안 수준이 낮습니다.  
  
 Windows 보안 로그에 대한 쓰기 작업을 수행하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정을 **보안 감사 생성** 정책에 추가해야 합니다. 기본적으로 이 정책에는 로컬 시스템, 로컬 서비스 및 네트워크 서비스 등이 포함됩니다. 이 설정은 보안 정책 스냅인(secpol.msc)을 사용하여 구성할 수 있습니다. 또한 **성공** 및 **실패** 모두에 대한 **감사 개체 액세스**보안 정책을 설정해야 합니다. 이 설정은 보안 정책 스냅인(secpol.msc)을 사용하여 구성할 수 있습니다. [!INCLUDE[wiprlhext](../../../includes/wiprlhext-md.md)] 또는 Windows Server 2008의 경우 감사 정책 프로그램( **AuditPol.exe** )을 사용하여 명령줄에서 더욱 세부적인**응용 프로그램 생성**정책을 설정할 수 있습니다. Windows 보안 로그의 쓰기를 설정하는 단계에 대한 자세한 내용은 [보안 로그에 SQL Server 감사 이벤트 쓰기](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)를 참조하세요. Auditpol.exe 프로그램에 대한 자세한 내용은 기술 자료 문서 921469, [그룹 정책을 사용하여 세부 보안 감사를 구성하는 방법](http://support.microsoft.com/kb/921469/)을 참조하세요. Windows 이벤트 로그는 Windows 운영 체제에 전반적으로 적용됩니다. Windows 이벤트 로그에 대한 자세한 내용은 [이벤트 뷰어 개요(Event Viewer Overview)](http://go.microsoft.com/fwlink/?LinkId=101455)를 참조하십시오. 감사에 대해 보다 정확한 권한이 필요하다면 이진 파일 대상을 사용하십시오.  
  
 감사 정보를 파일에 저장할 때 변조를 방지하기 위해 다음과 같은 방법으로 파일 위치에 대한 액세스를 제한할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정에는 읽기 및 쓰기 권한이 있어야 합니다.  
  
-   Audit Administrators에게는 일반적으로 읽기 및 쓰기 권한이 필요합니다. 이 경우에는 Audit Administrators가 감사 파일을 다른 공유에 복사하고 백업하는 등의 감사 파일에 대한 관리 작업을 위한 Windows 계정이라고 가정합니다.  
  
-   감사 파일을 읽을 권한이 있는 Audit Readers에게는 읽기 권한이 있어야 합니다.  
  
 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 이 파일에 쓰고 있는 경우라도 권한이 있는 Windows 사용자라면 감사 파일을 읽을 수 있습니다. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 은 파일을 배타적으로 잠그지 않으므로 다른 사용자가 읽기 작업을 수행할 수 있습니다.  
  
 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 이 파일에 액세스할 수 있으므로 CONTROL SERVER 권한이 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인은 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 을 사용하여 감사 파일에 액세스할 수 있습니다. 감사 파일을 읽고 있는 사용자를 기록하려면 master.sys.fn_get_audit_file에 감사를 정의합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 통해 감사 파일에 액세스한 CONTROL SERVER 권한을 가진 로그인이 기록됩니다.  
  
 Audit Administrator가 보관 등의 목적으로 파일을 다른 위치에 복사한 경우에는 새 위치에 대한 ACL을 다음과 같은 권한으로 축소해야 합니다.  
  
-   Audit Administrator - 읽기 / 쓰기  
  
-   Audit Reader - 읽기  
  
 Audit Administrators 또는 Audit Readers만 액세스할 수 있는 별도의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스(예: [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)]인스턴스)에서 감사 보고서를 생성하는 것이 좋습니다. 보고 작업을 위해 별도의 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 인스턴스를 사용하면 권한이 없는 사용자가 감사 레코드에 액세스하는 것을 방지할 수 있습니다.  
  
 Windows BitLocker 드라이브 암호화 또는 Windows 파일 시스템 암호화를 사용하여 감사 파일이 저장되는 폴더를 암호화하면 권한이 없는 액세스를 추가로 방지할 수 있습니다.  
  
 대상에 작성된 감사 레코드에 대한 자세한 내용은 [SQL Server Audit Records](../../../relational-databases/security/auditing/sql-server-audit-records.md)를 참조하십시오  
  
## <a name="overview-of-using-sql-server-audit"></a>SQL Server Audit 사용 개요  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 을 사용하여 감사를 정의할 수 있습니다. 감사가 생성되고 활성화되면 대상이 항목을 받습니다.  
  
 Windows에서 **이벤트 뷰어** 유틸리티를 사용하여 Windows 이벤트 로그를 읽을 수 있습니다. 파일 대상의 경우 **의** 로그 파일 뷰어 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 [fn_get_audit_file](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md) 함수를 사용하여 대상 파일을 읽을 수 있습니다.  
  
 감사를 만들고 사용하는 일반적인 프로세스는 다음과 같습니다.  
  
1.  감사를 만들고 대상을 정의합니다.  
  
2.  감사에 매핑될 서버 감사 사양 또는 데이터베이스 감사 사양을 만들고 감사 사양을 활성화합니다.  
  
3.  감사를 활성화합니다.  
  
4.  Windows **이벤트 뷰어**, **로그 파일 뷰어**또는 fn_get_audit_file 함수를 사용하여 감사 이벤트를 읽습니다.  
  
 자세한 내용은 [Create a Server Audit and Server Audit Specification](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md) 및 [Create a Server Audit and Database Audit Specification](../../../relational-databases/security/auditing/create-a-server-audit-and-database-audit-specification.md)를 참조하세요.  
  
## <a name="considerations"></a>고려 사항  
 감사 시작 도중에 오류가 발생하면 서버가 시작되지 않습니다. 이 경우 명령줄에서 **–f** 옵션을 사용하면 서버를 시작할 수 있습니다.  
  
 감사에 대해 ON_FAILURE=SHUTDOWN이 지정되어 있어 감사 오류 발생 시 서버가 종료되거나 시작되지 않으면 MSG_AUDIT_FORCED_SHUTDOWN 이벤트가 로그에 기록됩니다. 종료는 이 설정을 처음 발견할 때 발생하므로 이벤트는 한 번만 기록됩니다. 이 이벤트는 종료를 발생시킨 감사 오류 메시지 이후에 기록됩니다. 관리자는 단일 사용자 모드에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] –m **플래그를 사용하여** 를 시작함으로써 감사로 인한 종료를 무시할 수 있습니다. 단일 사용자 모드에서 시작하면 ON_FAILURE=SHUTDOWN이 지정된 모든 감사를 해당 세션에서 ON_FAILURE=CONTINUE로 실행되도록 다운그레이드할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] –m **플래그를 사용하여** 를 시작하면 MSG_AUDIT_SHUTDOWN_BYPASSED 메시지가 오류 로그에 기록됩니다.  
  
 서비스 시작 옵션에 대한 자세한 내용은 [데이터베이스 엔진 서비스 시작 옵션](../../../database-engine/configure-windows/database-engine-service-startup-options.md)을 참조하세요.  
  
### <a name="attaching-a-database-with-an-audit-defined"></a>감사가 정의된 데이터베이스 연결  
 감사 사양이 있고 서버에 존재하지 않는 GUID를 지정하는 데이터베이스를 연결하면 *분리된* 감사 사양이 발생합니다. 서버 인스턴스에 GUID가 일치하는 감사가 없으므로 감사 이벤트가 기록되지 않습니다. 이 상황을 해결하려면 ALTER DATABASE AUDIT SPECIFICATION 명령을 사용하여 분리된 감사 사양을 기존의 서버 감사에 연결합니다. 또는 CREATE SERVER AUDIT 명령을 사용하여 지정된 GUID를 가진 새 서버 감사를 만듭니다.  
  
 감사 사양이 정의된 데이터베이스를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit를 지원하지 않는 다른 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (예: [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)] )에 연결할 수 있지만 이때 감사 이벤트는 기록되지 않습니다.  
  
### <a name="database-mirroring-and-sql-server-audit"></a>데이터베이스 미러링 및 SQL Server Audit  
 데이터베이스 감사 사양이 정의되어 있고 데이터베이스 미러링을 사용하는 데이터베이스는 데이터베이스 감사 사양을 포함합니다. 미러링된 SQL 인스턴스에서 올바르게 작동하려면 다음 항목을 구성해야 합니다.  
  
-   데이터베이스 감사 사양을 활성화하여 감사 레코드를 작성할 수 있도록 하려면 미러 서버에 동일한 GUID를 가진 감사가 있어야 합니다. 이러한 감사는 CREATE AUDIT WITH GUID**=***\<원본 서버 감사의 GUID*> 명령을 사용하여 구성할 수 있습니다.  
  
-   이진 파일 대상의 경우 미러 서버 서비스 계정에 감사 내역이 작성될 위치에 대한 적절한 권한이 있어야 합니다.  
  
-   Windows 이벤트 로그 대상의 경우 미러 서버가 위치한 컴퓨터의 보안 정책이 보안 또는 응용 프로그램 이벤트 로그에 대한 서비스 계정 액세스를 허용해야 합니다.  
  
### <a name="auditing-administrators"></a>감사 관리자  
 **sysadmin** 고정 서버 역할의 멤버는 각 데이터베이스에서 **dbo** 사용자로 식별됩니다. 관리자 작업을 감사하기 위해서는 **dbo** 사용자의 작업을 감사합니다.  
  
## <a name="creating-and-managing-audits-with-transact-sql"></a>Transact-SQL로 감사 생성 및 관리  
 DDL 문, 동적 관리 뷰/함수 및 카탈로그 뷰를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit의 모든 측면을 구현할 수 있습니다.  
  
### <a name="data-definition-language-statements"></a>데이터 정의 언어 문  
 다음 DDL 문을 사용하여 감사 사양을 생성, 변경 및 삭제할 수 있습니다.  
  
|||  
|-|-|  
|[ALTER AUTHORIZATION](../../../t-sql/statements/alter-authorization-transact-sql.md)|[CREATE SERVER AUDIT](../../../t-sql/statements/create-server-audit-transact-sql.md)|  
|[ALTER DATABASE AUDIT SPECIFICATION](../../../t-sql/statements/alter-database-audit-specification-transact-sql.md)|[CREATE SERVER AUDIT SPECIFICATION](../../../t-sql/statements/create-server-audit-specification-transact-sql.md)|  
|[ALTER SERVER AUDIT](../../../t-sql/statements/alter-server-audit-transact-sql.md)|[DROP DATABASE AUDIT SPECIFICATION](../../../t-sql/statements/drop-database-audit-specification-transact-sql.md)|  
|[ALTER SERVER AUDIT SPECIFICATION](../../../t-sql/statements/alter-server-audit-specification-transact-sql.md)|[DROP SERVER AUDIT](../../../t-sql/statements/drop-server-audit-transact-sql.md)|  
|[CREATE DATABASE AUDIT SPECIFICATION](../../../t-sql/statements/create-database-audit-specification-transact-sql.md)|[DROP SERVER AUDIT SPECIFICATION](../../../t-sql/statements/drop-server-audit-specification-transact-sql.md)|  
  
### <a name="dynamic-views-and-functions"></a>동적 뷰 및 함수  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit에 사용할 수 있는 동적 뷰 및 함수를 나열합니다.  
  
|동적 뷰 및 함수|Description|  
|---------------------------------|-----------------|  
|[sys.dm_audit_actions](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)|감사 로그에 보고할 수 있는 모든 감사 동작 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit의 일부로 구성할 수 있는 모든 감사 동작 그룹에 대한 행을 반환합니다.|  
|[sys.dm_server_audit_status](../../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)|감사의 현재 상태에 대한 정보를 제공합니다.|  
|[sys.dm_audit_class_type_map](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)|감사 로그의 class_type 필드를 sys.dm_audit_actions의 class_desc 필드에 매핑하는 테이블을 반환합니다.|  
|[fn_get_audit_file](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)|서버 감사에 의해 생성된 감사 파일로부터 정보를 반환합니다.|  
  
### <a name="catalog-views"></a>카탈로그 뷰  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit에 사용할 수 있는 카탈로그 뷰를 나열합니다.  
  
|카탈로그 뷰|Description|  
|-------------------|-----------------|  
|[sys.database_ audit_specifications](../../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)|서버 인스턴스에 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit의 데이터베이스 감사 사양 정보를 포함합니다.|  
|[sys.database_audit_specification_details](../../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)|서버 인스턴스에 있는 모든 데이터베이스에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit의 데이터베이스 감사 사양 정보를 포함합니다.|  
|[sys.server_audits](../../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)|서버 인스턴스에 있는 각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit에 대해 하나의 행을 포함합니다.|  
|[sys.server_audit_specifications](../../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)|서버 인스턴스에 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit의 서버 감사 사양 정보를 포함합니다.|  
|[sys.server_audit_specifications_details](../../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)|서버 인스턴스에 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit의 서버 감사 사양 세부 정보(동작)를 포함합니다.|  
|[sys.server_file_audits](../../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)|서버 인스턴스에 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit의 파일 감사 유형에 대한 확장 정보를 저장합니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit의 기능과 명령마다 필요한 사용 권한이 있습니다.  
  
 서버 감사나 서버 감사 사양을 생성, 변경 또는 삭제하려면 서버 보안 주체에 ALTER ANY SERVER AUDIT 또는 CONTROL SERVER 권한이 있어야 합니다. 데이터베이스 감사 사양을 생성, 변경 또는 삭제하려면 데이터베이스 보안 주체에 ALTER ANY DATABASE AUDIT 권한이나 데이터베이스에 대한 ALTER 또는 CONTROL 권한이 있어야 합니다. 또한 데이터베이스에 연결할 수 있는 권한이나 ALTER ANY SERVER AUDIT 또는 CONTROL SERVER 권한이 보안 주체에 있어야 합니다.  
  
 VIEW ANY DEFINITION 권한이 있으면 서버 수준 감사 뷰 보기 권한이 제공되고, VIEW DEFINITION 권한이 있으면 데이터베이스 수준 감사 뷰 보기 권한이 제공됩니다. 이러한 권한을 거부하면 보안 주체에게 ALTER ANY SERVER AUDIT 또는 ALTER ANY DATABASE AUDIT 권한이 있더라도 카탈로그 뷰 보기 기능이 재정의됩니다.  
  
 권한 및 사용 권한을 부여하는 방법은 [GRANT&#40;Transact-SQL&#41;](../../../t-sql/statements/grant-transact-sql.md)를 참조하세요.  
  
> [!CAUTION]  
>  sysadmin 역할의 보안 주체는 모든 감사 구성 요소를 변경할 수 있으며 db_owner 역할의 보안 주체는 데이터베이스의 감사 사양을 변경할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit는 감사 사양을 만들거나 변경하는 로그온에 ALTER ANY DATABASE AUDIT 이상의 권한이 있는지 확인합니다. 하지만 데이터베이스를 연결할 때는 이를 확인하지 않습니다. 모든 데이터베이스 감사 사양을 sysadmin 또는 db_owner 역할의 보안 주체만큼만 신뢰할 수 있다고 간주해야 합니다.  
  
## <a name="related-tasks"></a>관련 태스크  
 [서버 감사 및 서버 감사 사양 만들기](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
 [서버 감사 및 데이터베이스 감사 사양 만들기](../../../relational-databases/security/auditing/create-a-server-audit-and-database-audit-specification.md)  
  
 [SQL Server 감사 로그 보기](../../../relational-databases/security/auditing/view-a-sql-server-audit-log.md)  
  
 [보안 로그에 SQL Server 감사 이벤트 쓰기](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)  
  
## <a name="topics-closely-related-to-auditing"></a>감사 관련 항목  
 [서버 속성&#40;보안 페이지&#41;](../../../database-engine/configure-windows/server-properties-security-page.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 로그인 감사를 설정하는 방법에 대해 설명합니다. 감사 레코드는 Windows 응용 프로그램 로그에 저장됩니다.  
  
 [c2 audit mode 서버 구성 옵션](../../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 C2 보안 정책 준수 감사 모드에 대해 설명합니다.  
  
 [Security Audit 이벤트 범주&#40;SQL Server Profiler&#41;](../../../relational-databases/event-classes/security-audit-event-category-sql-server-profiler.md)  
 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]에서 사용할 수 있는 감사 이벤트에 대해 설명합니다. 자세한 내용은 [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md)를 참조하세요.  
  
 [SQL 추적](../../../relational-databases/sql-trace/sql-trace.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로파일러를 사용하지 않고 사용자의 응용 프로그램 내에서 SQL 추적을 사용하여 수동으로 추적을 만드는 방법에 대해 설명합니다.  
  
 [DDL 트리거](../../../relational-databases/triggers/ddl-triggers.md)  
 DDL(데이터 정의 언어) 트리거를 사용하여 데이터베이스 변경 내용을 추적할 수 있는 방법에 대해 설명합니다.  
  
 [Microsoft TechNet: SQL Server TechCenter: SQL Server 2005 보안 및 보호](http://go.microsoft.com/fwlink/?LinkId=101152)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 보안에 대한 최신 정보를 제공합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 감사 동작 그룹 및 동작](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)   
 [SQL Server 감사 기록](../../../relational-databases/security/auditing/sql-server-audit-records.md)  
  
  


