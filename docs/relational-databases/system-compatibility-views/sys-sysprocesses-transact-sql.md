---
title: sys.sysprocesses (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 551d266374d6fd367eb4bba9e1d76a6322461c31
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="syssysprocesses-transact-sql"></a>sys.sysprocesses(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 실행 중인 프로세스에 대한 정보를 포함합니다. 이러한 프로세스는 클라이언트 프로세스 또는 시스템 프로세스일 수 있습니다. sysprocesses에 액세스하려면 master 데이터베이스 컨텍스트에 있거나 세 부분으로 구성된 master.dbo.sysprocesses 이름을 사용해야 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|spid|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 세션 id입니다.|  
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
|상태|**nchar(30)**|프로세스 ID 상태입니다. 가능한 값은 아래와 같습니다.<br /><br /> **유휴**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 세션을 다시 설정 합니다.<br /><br /> **실행** = 세션이 실행 되는 일괄 처리를 하나 이상 있습니다. MARS(Multiple Active Result Sets)를 설정하면 세션에서 여러 개의 일괄 처리를 실행할 수 있습니다. 자세한 내용은 참조 [Multiple Active Result Sets를 사용 하 여 &#40; MARS &#41; ](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).<br /><br /> **배경** = 세션에서 교착 상태 감지와 같은 백그라운드 태스크를 실행 합니다.<br /><br /> **롤백** = 세션에서 트랜잭션 롤백을 진행 합니다.<br /><br /> **보류 중인** =는 세션에서 작업자 스레드를 사용할 수 있을 때까지 기다리고 있습니다.<br /><br /> **실행 가능한** = 세션에서 작업이 시간 퀀텀을 얻기 위해 기다리는 동안 스케줄러의 실행 가능한 큐입니다.<br /><br /> **spinloop** = 세션의 태스크가 spinlock을 기다리고 있습니다.<br /><br /> **일시 중단** = 세션이 I/O가 완료 등의 이벤트에 대 한 대기 합니다.|  
|sid|**binary(86)**|사용자의 GUID(Globally Unique Identifier)입니다.|  
|hostname|**nchar(128)**|워크스테이션의 이름입니다.|  
|program_name|**nchar(128)**|응용 프로그램의 이름입니다.|  
|hostprocess|**nchar(10)**|워크스테이션 프로세스 ID입니다.|  
|cmd|**nchar(16)**|현재 실행 중인 명령입니다.|  
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
  
## <a name="remarks"></a>주의  
 사용자가 서버에 대한 VIEW SERVER STATE 권한을 가지고 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 실행 중인 모든 세션을 볼 수 있습니다. 그렇지 않으면 현재 세션만 볼 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [실행 관련 동적 관리 뷰 및 함수 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [시스템 뷰 &#40; 시스템 테이블 매핑 Transact SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
