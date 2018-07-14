---
title: 추적 필터링 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], events
- events [SQL Server], filters
- filters [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 019c10ab-68f6-4e40-a5e8-735b2e1270db
caps.latest.revision: 26
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 367a9669c11cb1841a4af3801abb98e385571388
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37212833"
---
# <a name="filter-a-trace"></a>추적 필터링
  필터가 설정되면 추적에서 수집하는 이벤트가 제한됩니다. 필터가 설정되어 있지 않으면 선택된 이벤트 클래스의 모든 이벤트가 추적 출력에서 반환됩니다. 예를 들어 특정 사용자에 대한 추적에서 Windows 사용자 이름을 제한하면 출력 데이터는 해당 사용자만 표시되도록 간략해집니다.  
  
 반드시 추적에 대한 필터를 설정해야 하는 것은 아닙니다. 그러나 필터는 추적하는 동안 발생하는 오버헤드를 최소화합니다. 필터는 포커스가 있는 데이터를 반환하므로 성능 분석과 감사를 편리하게 해 줍니다.  
  
 추적 내에 캡처된 이벤트 데이터를 필터링하려면 관련된 데이터만 추적에서 반환하는 추적 이벤트 조건을 선택합니다. 예를 들어 추적에서 특정 응용 프로그램 작업에 대한 모니터링을 포함하거나 제외하도록 할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 가 추적을 생성할 때 기본적으로 자체 작업을 필터링합니다.  
  
 또 다른 예를 들면 쿼리를 모니터링하여 실행 시간이 가장 오래 걸리는 일괄 처리를 확인하는 경우 실행하는 데 30초(CPU 최소값인 30,000밀리초) 이상 걸리는 일괄 처리만 모니터링하도록 추적 이벤트 조건을 설정할 수 있습니다.  
  
## <a name="filter-creation-guidelines"></a>필터 생성 지침  
 일반적으로 추적을 필터링하려면 다음 단계를 따릅니다.  
  
1.  추적에 포함시킬 이벤트를 확인합니다.  
  
2.  필요한 정보가 있는 데이터와 데이터 열을 확인합니다.  
  
3.  필요한 데이터 하위 집합을 확인하고 데이터 하위 집합을 기준으로 필터를 정의합니다.  
  
 예를 들어 일정 시간 이상이 걸리는 이벤트만 추적하려고 할 수도 있습니다. 이 경우 **Duration** 데이터 열이 300밀리초보다 더 큰 이벤트를 포함하는 추적을 만들 수 있습니다. 그러면 300밀리초 내에 완료되는 이벤트는 추적에 포함되지 않습니다.  
  
 SQL Server Profiler 또는 Transact-SQL 저장 프로시저를 사용하여 필터를 만들 수 있습니다.  
  
 **추적 템플릿에서 이벤트를 필터링하려면**  
  
 [추적에서의 이벤트 필터링&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
 [추적 필터 설정&#40;Transact-SQL&#41;](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md)  
  
 **필터를 수정하려면**  
  
 [필터 수정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
 필터의 가용성은 데이터 열에 따라 다릅니다. 일부 데이터 열은 필터링할 수 없습니다. 다음 표와 같이 필터링 가능 데이터 열을 특정 관계형 연산자로만 필터링할 수 있습니다.  
  
|관계형 연산자|연산자 기호|Description|  
|-------------------------|---------------------|-----------------|  
|Like|Like|추적 이벤트 데이터가 입력한 텍스트와 같아야 함을 지정합니다. 다중 값을 허용합니다.|  
|유사하지 않음|유사하지 않음|추적 이벤트 데이터가 입력한 텍스트와 같지 않아야 함을 지정합니다. 다중 값을 허용합니다.|  
|같음|=|추적 이벤트 데이터가 입력한 값과 같아야 함을 지정합니다. 다중 값을 허용합니다.|  
|같지 않음|<>|추적 이벤트 데이터가 입력한 값과 같지 않아야 함을 지정합니다. 다중 값을 허용합니다.|  
|보다 큼|>|추적 이벤트 데이터가 입력한 값보다 커야 함을 지정합니다.|  
|크거나 같음|>=|추적 이벤트 데이터가 입력한 값보다 크거나 같아야 함을 지정합니다.|  
|보다 작음|<|추적 이벤트 데이터가 입력한 값보다 작아야 함을 지정합니다.|  
|작거나 같음|<=|추적 이벤트 데이터가 입력한 값보다 작거나 같아야 함을 지정합니다.|  
  
 다음 표에는 필터링할 수 있는 데이터 열과 사용 가능한 관계형 연산자가 나열되어 있습니다.  
  
|데이터 열|관계 연산자|  
|------------------|--------------------------|  
|**ApplicationName**|LIKE, NOT LIKE|  
|**BigintData1**|=, <>, >=, <=|  
|**BigintData2**|=, <>, >=, <=|  
|**BinaryData**|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 이 데이터 열의 이벤트를 필터링할 수 있습니다. 자세한 내용은 [SQL Server Profiler로 추적 필터링](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)을 참조하세요.|  
|**ClientProcessID**|=, <>, >=, <=|  
|**ColumnPermissions**|=, <>, >=, <=|  
|**CPU**|=, <>, >=, <=|  
|**DatabaseID**|=, <>, >=, <=|  
|**DatabaseName**|LIKE, NOT LIKE|  
|**DBUserName**|LIKE, NOT LIKE|  
|**기간**|=, <>, >=, \<=|  
|**EndTime**|>=, <=|  
|**오류**|=, <>, >=, <=|  
|**EventSubClass**|=, <>, >=, <=|  
|**FileName**|LIKE, NOT LIKE|  
|**GUID**|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 이 데이터 열의 이벤트를 필터링할 수 있습니다. 자세한 내용은 [SQL Server Profiler로 추적 필터링](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)을 참조하세요.|  
|**Handle**|=, <>, >=, <=|  
|**HostName**|LIKE, NOT LIKE|  
|**IndexID**|=, <>, >=, <=|  
|**IntegerData**|=, <>, >=, <=|  
|**IntegerData2**|=, <>, >=, <=|  
|**IsSystem**|=, <>, >=, <=|  
|**LineNumber**|=, <>, >=, <=|  
|**LinkedServerName**|LIKE, NOT LIKE|  
|**LoginName**|LIKE, NOT LIKE|  
|**LoginSid**|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 이 데이터 열의 이벤트를 필터링할 수 있습니다. 자세한 내용은 [SQL Server Profiler로 추적 필터링](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)을 참조하세요.|  
|**MethodName**|LIKE, NOT LIKE|  
|**모드**|=, <>, >=, <=|  
|**NestLevel**|=, <>, >=, <=|  
|**NTDomainName**|LIKE, NOT LIKE|  
|**NTUserName**|LIKE, NOT LIKE|  
|**Exchange Spill**|=, <>, >=, <=|  
|**ObjectID2**|=, <>, >=, <=|  
|**ObjectName**|LIKE, NOT LIKE|  
|**ObjectType**|=, <>, >=, <=|  
|**Offset**|=, <>, >=, <=|  
|**OwnerID**|=, <>, >=, <=|  
|**OwnerName**|LIKE, NOT LIKE|  
|**ParentName**|LIKE, NOT LIKE|  
|**사용 권한**|=, <>, >=, <=|  
|**ProviderName**|LIKE, NOT LIKE|  
|**Reads**|=, <>, >=, <=|  
|**RequestID**|=, <>, >=, <=|  
|**RoleName**|LIKE, NOT LIKE|  
|**RowCounts**|=, <>, >=, <=|  
|**SessionLoginName**|LIKE, NOT LIKE|  
|**Severity**|=, <>, >=, <=|  
|**SourceDatabaseID**|=, <>, >=, <=|  
|**SPID**|=, <>, >=, \<=|  
|**SqlHandle**|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 이 데이터 열의 이벤트를 필터링할 수 있습니다. 자세한 내용은 [SQL Server Profiler로 추적 필터링](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)을 참조하세요.|  
|**StartTime**|>=, <=|  
|**State**|=, <>, >=, <=|  
|**성공**|=, <>, >=, <=|  
|**TargetLoginName**|LIKE, NOT LIKE|  
|**TargetLoginSid**|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 이 데이터 열의 이벤트를 필터링할 수 있습니다. 자세한 내용은 [SQL Server Profiler로 추적 필터링](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)을 참조하세요.|  
|**TargetUserName**|LIKE, NOT LIKE|  
|**TextData** <sup>1</sup>|LIKE, NOT LIKE|  
|**TransactionID**|=, <>, >=, <=|  
|**형식**|=, <>, >=, <=|  
|**Writes**|=, <>, >=, <=|  
|**XactSequence**|=, <>, >=, <=|  
  
 <sup>1</sup> 이벤트를 추적 하는 경우는 **osql** 유틸리티 또는 **sqlcmd** 유틸리티를 항상 추가 **%** 필터에 **TextData**  데이터 열입니다.  
  
 보안 예방 조치로서 SQL 추적은 암호에 영향을 미치는 보안 관련 저장 프로시저의 모든 정보를 자동으로 추적에서 생략합니다. 이 보안 메커니즘은 따로 구성할 수 없고 항상 유효하며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 모든 작업을 추적할 수 있는 권한을 가진 사용자가 암호를 캡처할 수 없도록 합니다.  
  
 다음 보안 관련 저장 프로시저가 모니터링되지만 **TextData** 데이터 열에 출력이 기록되지 않습니다.  
  
 [sp_addapprole&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addapprole-transact-sql)  
  
 [sp_adddistpublisher&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql)  
  
 [sp_adddistributiondb&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql)  
  
 [sp_adddistributor&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributor-transact-sql)  
  
 [sp_addlinkedserver&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)  
  
 [sp_addlinkedsrvlogin&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql)  
  
 [sp_addlogin&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)  
  
 [sp_addmergepullsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)  
  
 [sp_addpullsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)  
  
 [sp_addremotelogin&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql)  
  
 [sp_addsubscriber&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql)  
  
 [sp_approlepassword&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-approlepassword-transact-sql)  
  
 [sp_changedistpublisher&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql)  
  
 [sp_changesubscriber&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql)  
  
 [sp_dsninfo&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dsninfo-transact-sql)  
  
 [sp_helpsubscription_properties&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql)  
  
 [sp_link_publication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql)  
  
 [sp_password&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql)  
  
 [sp_setapprole&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-setapprole-transact-sql)  
  
  
