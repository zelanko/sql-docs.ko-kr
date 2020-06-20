---
title: SQL Server 2014에서 지원 되지 않는 데이터베이스 엔진 기능 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- VIA protocol
- unsupported features [SQL Server]
- SQL Mail
- discontinued functionality [SQL Server]
- RESTORE WITH DBO_ONLY
- BACKUP WITH PASSWORD
- user instances enabled
- BACKUP WITH MEDIAPASSWORD
- AWE
- SQL-DMO
- '*= and =*'
- 80 compatibility levels
- COMPUTE BY
- user instance timeout
- sp_dropalias
- COMPUTE
- WITH APPEND
- sys.database_principal_aliases
- sp_dboption
- DATABASEPROPERTY
- FASTFIRSTROW hint
- SET DISABLE_DEF_CNST_CHK
ms.assetid: d686cdf0-d11d-4dba-9ec8-de1a5f189f25
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 14924dedee04345c593683752baff4161c8d270d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933154"
---
# <a name="discontinued-database-engine-functionality-in-sql-server-2014"></a>SQL Server 2014에서 지원되지 않는 데이터베이스 엔진 기능
  이 항목에서는 [!INCLUDE[ssDE](../includes/ssde-md.md)] 에서 더 이상 사용할 수 없는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]기능에 대해 설명합니다.  
  
## <a name="discontinued-features-in-sssql14"></a><a name="SQL14"></a>에서 지원 되지 않는 기능[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 다음 표에는 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]에서 제거된 기능이 나와 있습니다.  
  
|Category|지원되지 않는 기능|대체 기능|  
|--------------|--------------------------|-----------------|  
|호환성 수준|호환성 수준 90|데이터베이스를 호환성 수준 100 이상으로 설정해야 합니다. 호환성 수준이 100 미만인 데이터베이스가 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]로 업그레이드될 때 데이터베이스의 호환성 수준은 업그레이드 작업 중 100으로 설정됩니다.|  
  
## <a name="discontinued-features-in-sssql11"></a><a name="Denali"></a>에서 지원 되지 않는 기능[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 다음 표에는 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서 제거된 기능이 나와 있습니다.  
  
|Category|지원되지 않는 기능|대체 기능|  
|--------------|--------------------------|-----------------|  
|Backup 및 복원|**Backup {database &#124; log} WITH PASSWORD** 및 **backup {database &#124; LOG} WITH mediapassword** 가 중단 됩니다. **[MEDIA] 암호를 사용 하 여 {DATABASE &#124; LOG} 복원은**계속 사용 되지 않습니다.|None|  
|Backup 및 복원|**{DATABASE &#124; LOG} 복원 ... DBO_ONLY 사용**|**{DATABASE &#124; LOG} 복원 ... RESTRICTED_USER 사용**|  
|호환성 수준|호환성 수준 80|데이터베이스를 호환성 수준 90 이상으로 설정해야 합니다.|  
|구성 옵션|`sp_configure 'user instance timeout'` 및 `'user instances enabled'`|Local Database 기능을 사용합니다. 자세한 내용은 [SqlLocalDB 유틸리티](../tools/sqllocaldb-utility.md) 를 참조 하세요.|  
|연결 프로토콜|VIA 프로토콜에 대한 지원이 중단되었습니다.|대신 TCP를 사용하십시오.|  
|데이터베이스 개체|트리거에 있는 `WITH APPEND` 절|전체 트리거를 다시 만듭니다.|  
|데이터베이스 옵션|`sp_dboption`|`ALTER DATABASE`|  
|메일|SQL 메일|데이터베이스 메일을 사용합니다. 자세한 내용은 [Database Mail](../relational-databases/database-mail/database-mail.md) 및  [Use Database Mail Instead of SQL Mail](../relational-databases/policy-based-management/use-database-mail-instead-of-sql-mail.md)을 참조하십시오.|  
|메모리 관리|32비트 AWE(Address Windowing Extensions) 및 32비트 Hot Add 메모리 지원.|64비트 운영 체제를 사용하십시오.|  
|메타데이터|`DATABASEPROPERTY`|`DATABASEPROPERTYEX`|  
|프로그래밍 기능|SQL-DMO(SQL Server Distributed Management Objects)|SMO(SQL Server 관리 개체)|  
|쿼리 힌트|`FASTFIRSTROW` 힌트|`OPTION (FAST`*n* `)` .|  
|원격 서버|`sp_addserver`를 사용하여 새 원격 서버를 만드는 기능은 더 이상 사용되지 않습니다. 'local' 옵션을 사용한 `sp_addserver`는 계속 사용할 수 있습니다. 업그레이드 중에 보존되었거나 복제로 만들어진 원격 서버는 사용할 수 있습니다.|연결된 서버를 사용하여 원격 서버를 대체합니다.|  
|보안|`sp_dropalias`|별칭을 사용자 계정 및 데이터베이스 역할의 조합으로 대체해야 합니다. 업그레이드된 데이터베이스에서 `sp_dropalias`를 사용하여 별칭을 제거해야 합니다.|  
|보안|**2000 이전의 로그인 값을 나타내는** PWDCOMPARE [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 버전 매개 변수는 더 이상 사용되지 않습니다.|None|  
|SMO의 Service Broker 프로그래밍 기능|**Microsoft.SqlServer.Management.Smo.Broker.BrokerPriority** 클래스는 더 이상 **Microsoft.SqlServer.Management.Smo.IObjectPermission** 인터페이스를 구현하지 않습니다.||  
|Set 옵션|`SET DISABLE_DEF_CNST_CHK`|없음|  
|시스템 테이블|sys.database_principal_aliases|별칭 대신 역할을 사용해야 합니다.|  
|Transact-SQL|`RAISERROR` 형식의 `RAISERROR integer 'string'`는 더 이상 사용되지 않습니다.|현재 **RAISERROR (...)** 구문을 사용 하 여 문을 다시 작성 합니다.|  
|Transact-SQL 구문|`COMPUTE / COMPUTE BY`|`ROLLUP` 사용|  
|Transact-SQL 구문|**\*=** And **=&#42;** 사용|ANSI 조인 구문을 사용합니다. 자세한 내용은 [FROM (Transact-SQL)](https://msdn.microsoft.com/library/ms177634\(SQL.105\).aspx)을 참조하십시오.|  
|XEvents|databases_data_file_size_changed, databases_log_file_size_changed<br /><br /> eventdatabases_log_file_used_size_changed<br /><br /> locks_lock_timeouts_greater_than_0<br /><br /> locks_lock_timeouts|database_file_size_change event, database_file_size_change 이벤트로 바뀌었습니다.<br /><br /> database_file_size_change event<br /><br /> lock_timeout_greater_than_0<br /><br /> lock_timeout|  
  
 **추가 XEvent 변경**  
  
 **resource_monitor_ring_buffer_record**:  
  
-   제거된 필드: single_pages_kb, multiple_pages_kb  
  
-   추가된 필드: target_kb, pages_kb  
  
 **memory_node_oom_ring_buffer_recorded**:  
  
-   제거된 필드: single_pages_kb, multiple_pages_kb  
  
-   추가된 필드: target_kb, pages_kb  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014 이후에는 지원되지 않는 데이터베이스 엔진 기능](deprecated-database-engine-features-in-sql-server-2016.md?view=sql-server-2014)  
  
  
