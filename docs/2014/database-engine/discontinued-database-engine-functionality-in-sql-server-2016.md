---
title: 지원 되지 않는 SQL server 2014 데이터베이스 엔진 기능 | Microsoft Docs
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
caps.latest.revision: 93
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 648ff85c3061bc7d20408eaae7a14748650e5886
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37218043"
---
# <a name="discontinued-database-engine-functionality-in-sql-server-2014"></a>SQL Server 2014에서 지원되지 않는 데이터베이스 엔진 기능
  이 항목에서는 [!INCLUDE[ssDE](../includes/ssde-md.md)] 에서 더 이상 사용할 수 없는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]기능에 대해 설명합니다.  
  
## <a name="discontinued-features-in-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 다음 표에는 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]에서 제거된 기능이 나와 있습니다.  
  
|범주|지원되지 않는 기능|대체 기능|  
|--------------|--------------------------|-----------------|  
|호환성 수준|호환성 수준 90|데이터베이스를 호환성 수준 100 이상으로 설정해야 합니다. 호환성 수준이 100 미만인 데이터베이스가 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]로 업그레이드될 때 데이터베이스의 호환성 수준은 업그레이드 작업 중 100으로 설정됩니다.|  
  
## <a name="discontinued-features-in-includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 다음 표에는 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서 제거된 기능이 나와 있습니다.  
  
|범주|지원되지 않는 기능|대체 기능|  
|--------------|--------------------------|-----------------|  
|Backup 및 Restore 메서드|**백업 {데이터베이스 &#124; LOG} WITH PASSWORD** 및 **백업 {데이터베이스 &#124; LOG} WITH MEDIAPASSWORD** 은 지원 되지 않습니다. **복원 {데이터베이스 &#124; 로그} [MEDIA] PASSWORD를 사용 하 여**계속 되지 않습니다.|InclusionThresholdSetting|  
|Backup 및 Restore 메서드|**RESTORE {DATABASE &AMP;#124; LOG}... WITH DBO_ONLY**|**RESTORE {DATABASE &AMP;#124; LOG}...... RESTRICTED_USER를 사용 하 여**|  
|호환성 수준|호환성 수준 80|데이터베이스를 호환성 수준 90 이상으로 설정해야 합니다.|  
|구성 옵션|`sp_configure 'user instance timeout'` 및 `'user instances enabled'`|Local Database 기능을 사용합니다. 자세한 내용은 참조 하세요. [SqlLocalDB 유틸리티](../tools/sqllocaldb-utility.md)|  
|연결 프로토콜|VIA 프로토콜에 대한 지원이 중단되었습니다.|대신 TCP를 사용하십시오.|  
|데이터베이스 개체|트리거에 있는 `WITH APPEND` 절|전체 트리거를 다시 만듭니다.|  
|데이터베이스 옵션|`sp_dboption`|`ALTER DATABASE`|  
|메일|SQL 메일|데이터베이스 메일을 사용합니다. 자세한 내용은 [데이터베이스 메일](../relational-databases/database-mail/database-mail.md) 하 고 [Use Database Mail Instead of SQL Mail](../relational-databases/policy-based-management/use-database-mail-instead-of-sql-mail.md)합니다.|  
|메모리 관리|32비트 AWE(Address Windowing Extensions) 및 32비트 Hot Add 메모리 지원.|64비트 운영 체제를 사용하십시오.|  
|메타데이터|`DATABASEPROPERTY`|`DATABASEPROPERTYEX`|  
|프로그래밍 기능|SQL-DMO(SQL Server Distributed Management Objects)|SMO(SQL Server Management Objects)|  
|쿼리 힌트|`FASTFIRSTROW` 힌트|`OPTION (FAST` *n* `)`합니다.|  
|원격 서버|`sp_addserver`를 사용하여 새 원격 서버를 만드는 기능은 더 이상 사용되지 않습니다. 'local' 옵션을 사용한 `sp_addserver`는 계속 사용할 수 있습니다. 업그레이드 중에 보존되었거나 복제로 만들어진 원격 서버는 사용할 수 있습니다.|연결된 서버를 사용하여 원격 서버를 대체합니다.|  
|보안|`sp_dropalias`|별칭을 사용자 계정 및 데이터베이스 역할의 조합으로 대체해야 합니다. 사용 하 여 `sp_dropalias` 업그레이드 된 데이터베이스에서 별칭을 제거 합니다.|  
|보안|버전 매개 변수 **PWDCOMPARE** 로그인 값을 나타내는 이전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000이 이제 중단 됩니다.|InclusionThresholdSetting|  
|SMO의 Service Broker 프로그래밍 기능|**Microsoft.SqlServer.Management.Smo.Broker.BrokerPriority** 클래스는 더 이상 **Microsoft.SqlServer.Management.Smo.IObjectPermission** 인터페이스를 구현하지 않습니다.||  
|SET 옵션|`SET DISABLE_DEF_CNST_CHK`|없음|  
|시스템 테이블|sys.database_principal_aliases|별칭 대신 역할을 사용해야 합니다.|  
|Transact-SQL|`RAISERROR` 형식의 `RAISERROR integer 'string'`는 더 이상 사용되지 않습니다.|현재 **RAISERROR(…)** 구문을 사용하여 문을 다시 작성해야 합니다.|  
|Transact-SQL 구문|`COMPUTE / COMPUTE BY`|`ROLLUP` 사용|  
|Transact-SQL 구문|이용 **\* =** 및 **=\***|ANSI 조인 구문을 사용합니다. 자세한 내용은 [FROM (Transact-SQL)](http://msdn.microsoft.com/library/ms177634\(SQL.105\).aspx)을 참조하십시오.|  
|XEvents|databases_data_file_size_changed, databases_log_file_size_changed<br /><br /> eventdatabases_log_file_used_size_changed<br /><br /> locks_lock_timeouts_greater_than_0<br /><br /> locks_lock_timeouts|Database_file_size_change database_file_size_change 이벤트로 대체<br /><br /> database_file_size_change event<br /><br /> lock_timeout_greater_than_0<br /><br /> lock_timeout|  
  
 **추가 XEvent 변경**  
  
 **resource_monitor_ring_buffer_record**:  
  
-   제거된 필드: single_pages_kb, multiple_pages_kb  
  
-   추가된 필드: target_kb, pages_kb  
  
 **memory_node_oom_ring_buffer_recorded**:  
  
-   제거된 필드: single_pages_kb, multiple_pages_kb  
  
-   추가된 필드: target_kb, pages_kb  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 2014에서 사용되지 않는 데이터베이스 엔진 기능](deprecated-database-engine-features-in-sql-server-2016.md)  
  
  
