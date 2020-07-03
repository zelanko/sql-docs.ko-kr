---
title: sys.sys프로세스 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysprocesses_TSQL
- sys.sysprocesses_TSQL
- sys.sysprocesses
- sysprocesses
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysprocesses compatibility view
- sysprocesses system table
ms.assetid: 60a36d36-54b3-4bd6-9cac-702205a21b16
author: rothja
ms.author: jroth
ms.openlocfilehash: 0f195a452ffde16d7de821841367e259a686578f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899773"
---
# <a name="syssysprocesses-transact-sql"></a>sys.sysprocesses(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 실행 중인 프로세스에 대한 정보를 포함합니다. 이러한 프로세스는 클라이언트 프로세스 또는 시스템 프로세스일 수 있습니다. sysprocesses에 액세스하려면 master 데이터베이스 컨텍스트에 있거나 세 부분으로 구성된 master.dbo.sysprocesses 이름을 사용해야 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|spid|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 세션 ID입니다.|  
|kpid|**smallint**|Windows 스레드 ID입니다.|  
|blocked|**smallint**|요청을 차단하고 있는 세션의 ID입니다. 이 열이 NULL이면 요청이 차단되지 않거나 차단 세션의 세션 정보를 사용할 수 없습니다(또는 식별할 수 없음).<br /><br /> -2 = 분리된 분산 트랜잭션이 차단 리소스를 소유합니다.<br /><br /> -3 = 지연된 복구 트랜잭션이 차단 리소스를 소유합니다.<br /><br /> -4 = 내부 래치 상태 전환 때문에 차단 래치 소유자의 세션 ID를 확인할 수 없습니다.|  
|waittype|**binary(2)**|예약되어 있습니다.|  
|waittime|**bigint**|현재 대기 시간(밀리초)입니다.<br /><br /> 0 = 프로세스가 대기하고 있지 않습니다.|  
|lastwaittype|**nchar(32)**|마지막 또는 현재 대기 유형의 이름을 나타내는 문자열입니다.|  
|waitresource|**nchar(256)**|잠금 리소스를 텍스트로 표시한 것입니다.|  
|dbid|**smallint**|프로세스가 현재 사용하고 있는 데이터베이스의 ID입니다.|  
|uid|**smallint**|명령을 실행한 사용자의 ID입니다. 사용자 및 역할 수가 32,767을 초과하는 경우 오버플로되거나 NULL을 반환합니다.|  
|cpu|**int**|프로세스의 누적 CPU 시간입니다. 항목은 SET STATISTICS TIME 옵션의 ON/OFF 여부와 관계없이 모든 프로세스에 대해 업데이트됩니다.|  
|physical_io|**bigint**|프로세스에 대한 누적 디스크 읽기/쓰기입니다.|  
|memusage|**int**|현재 해당 프로세스에 할당된 프로시저 캐시에 있는 페이지 수입니다. 음수는 프로세스가 다른 프로세스에 의해 할당된 메모리를 해제하고 있음을 의미합니다.|  
|login_time|**datetime**|클라이언트 프로세스가 서버에 로그인한 시간입니다.|  
|last_batch|**datetime**|클라이언트 프로세스가 원격 저장 프로시저 호출 또는 EXECUTE 문을 마지막으로 실행한 시간입니다.|  
|ecid|**smallint**|단일 프로세스 대신 작업하고 있는 하위 스레드를 고유하게 식별하는 데 사용하는 실행 컨텍스트 ID입니다.|  
|open_tran|**smallint**|프로세스의 열려 있는 트랜잭션 수입니다.|  
|상태|**nchar(30)**|프로세스 ID 상태입니다. 가능한 값은 다음과 같습니다.<br /><br /> **유휴 상태**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 세션을 다시 설정 하는 중입니다.<br /><br /> **running** = 세션에서 하나 이상의 일괄 처리를 실행 하 고 있습니다. MARS(Multiple Active Result Sets)를 설정하면 세션에서 여러 개의 일괄 처리를 실행할 수 있습니다. 자세한 내용은 [MARS&#40;Multiple Active Result Sets&#41; 사용](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)을 참조하세요.<br /><br /> **background** = 세션에서 교착 상태 감지와 같은 백그라운드 작업을 실행 하 고 있습니다.<br /><br /> **rollback** = 세션에서 트랜잭션 롤백이 진행 중입니다.<br /><br /> **보류 중** = 세션이 작업자 스레드를 사용할 수 있을 때까지 기다리고 있습니다.<br /><br /> 실행 **가능 = 시간** 퀀텀 가져오기를 기다리는 동안 세션의 태스크가 스케줄러의 실행 가능한 큐에 있습니다.<br /><br /> **spinloop** = 세션의 태스크가 spinlock이 사용 가능 해질 때까지 대기 하 고 있습니다.<br /><br /> **suspended** = 세션이 i/o와 같은 이벤트가 완료 되기를 기다리고 있습니다.|  
|sid|**binary(86)**|사용자의 GUID(Globally Unique Identifier)입니다.|  
|hostname|**nchar(128)**|워크스테이션의 이름입니다.|  
|program_name|**nchar(128)**|애플리케이션의 이름입니다.|  
|hostprocess|**nchar(10)**|워크스테이션 프로세스 ID입니다.|  
|cmd|**nchar (52)**|현재 실행 중인 명령입니다.|  
|nt_domain|**nchar(128)**|클라이언트(Windows 인증을 사용하는 경우) 또는 트러스트된 연결의 Windows 도메인입니다.|  
|nt_username|**nchar(128)**|프로세스(Windows 인증을 사용하는 경우) 또는 트러스트된 연결의 Windows 사용자 이름입니다.|  
|net_address|**nchar(12)**|각 사용자의 워크스테이션에서 네트워크 어댑터에 할당된 고유 식별자입니다. 사용자가 로그인하면 이 식별자가 net_address 열에 삽입됩니다.|  
|net_library|**nchar(12)**|클라이언트의 네트워크 라이브러리가 저장된 열입니다. 모든 클라이언트 프로세스는 네트워크 연결에 나타납니다. 네트워크 연결에는 연결을 구축할 수 있도록 해 주는 연관된 네트워크 라이브러리가 있습니다.|  
|loginame|**nchar(128)**|로그인 이름입니다.|  
|context_info|**binary(128)**|SET CONTEXT_INFO 문을 사용하여 일괄 처리에 저장한 데이터입니다.|  
|sql_handle|**binary(20)**|현재 실행 중인 일괄 처리 또는 개체를 나타냅니다.<br /><br /> **참고** 이 값은 개체의 일괄 처리 또는 메모리 주소에서 파생 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 해시 기반 알고리즘을 사용하여 계산되지 않습니다.|  
|stmt_start|**int**|지정된 sql_handle에 대한 현재 SQL 문의 시작 오프셋입니다.|  
|stmt_end|**int**|지정된 sql_handle에 대한 현재 SQL 문의 끝 오프셋입니다.<br /><br /> -1 = 현재 문이 지정된 sql_handle에 대해 fn_get_sql 함수에서 반환한 결과의 끝까지 실행됩니다.|  
|request_id|**int**|요청의 ID입니다. 특정 세션에서 실행 중인 요청을 식별하는 데 사용됩니다.|
|page_resource |**binary (8)** |**적용 대상**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] <br /><br /> 열이 페이지를 포함 하는 경우 페이지 리소스의 8 바이트 16 진수 표현입니다 `waitresource` . |  
  
## <a name="remarks"></a>설명  
 사용자가 서버에 대한 VIEW SERVER STATE 권한을 가지고 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 실행 중인 모든 세션을 볼 수 있습니다. 그렇지 않으면 현재 세션만 볼 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;관련 동적 관리 뷰 및 함수 실행](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
