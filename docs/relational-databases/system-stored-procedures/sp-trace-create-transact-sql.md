---
title: sp_trace_create (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_create_TSQL
- sp_trace_create
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_create
ms.assetid: f3a43597-4c5a-4520-bcab-becdbbf81d2e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a8327dc8beafb5d4e219cdaf25c44c75af3e85e5
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892599"
---
# <a name="sp_trace_create-transact-sql"></a>sp_trace_create(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  추적 정의를 만듭니다. 새 추적은 중지된 상태가 됩니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 확장 이벤트를 대신 사용하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_trace_create [ @traceid = ] trace_id OUTPUT   
          , [ @options = ] option_value   
          , [ @tracefile = ] 'trace_file'   
     [ , [ @maxfilesize = ] max_file_size ]  
     [ , [ @stoptime = ] 'stop_time' ]  
     [ , [ @filecount = ] 'max_rollover_files' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @traceid = ] trace_id`가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 새 추적에 할당 한 번호입니다. 모든 사용자 제공 입력은 무시됩니다. *trace_id* 은 **int**이며 기본값은 NULL입니다. 사용자는 *trace_id* 값을 사용 하 여이 저장 프로시저에서 정의 된 추적을 식별, 수정 및 제어할 수 있습니다.  
  
`[ @options = ] option_value`추적에 대해 설정 된 옵션을 지정 합니다. *option_value* 는 **int**이며 기본값은 없습니다. 선택한 옵션 값의 합계를 지정하여 이러한 옵션의 조합을 선택할 수 있습니다. 예를 들어 TRACE_FILE_ROLLOVER와 SHUTDOWN_ON_ERROR 옵션을 모두 설정 하려면 *option_value*에 **6** 을 지정 합니다.  
  
 다음 표에서는 옵션, 설명 및 해당 값을 나열합니다.  
  
|옵션 이름|옵션 값|설명|  
|-----------------|------------------|-----------------|  
|TRACE_FILE_ROLLOVER|**2**|*Max_file_size* 에 도달 하면 현재 추적 파일이 닫히고 새 파일이 생성 되도록 지정 합니다. 모든 새 기록은 새 파일에 기록합니다. 새 파일은 이전 파일과 같은 이름을 갖지만 정수를 붙여 시퀀스를 표시합니다. 예를 들어 원래 추적 파일 이름이 filename.trc이면, 다음 추적 파일 이름은 filename_1.trc이고 그 다음은 filename_2.trc의 식으로 명명됩니다.<br /><br /> 롤오버 추적 파일이 많이 생성될수록 파일 이름에 붙이는 정수 값도 순차적으로 증가합니다.<br /><br /> *Max_file_size*값을 지정 하지 않고이 옵션을 지정 하는 경우 SQL Server는 기본값 *max_file_size* (5mb)를 사용 합니다.|  
|SHUTDOWN_ON_ERROR|**4**|어떤 이유에서건 추적을 파일에 쓸 수 없으면 SQL Server가 시스템을 종료하도록 지정합니다. 이 옵션은 보안 감사 추적을 수행할 때 유용합니다.|  
|TRACE_PRODUCE_BLACKBOX|**8**|서버가 만든 마지막 5MB 추적 정보의 기록은 서버에 의해 저장됨을 지정합니다. TRACE_PRODUCE_BLACKBOX는 다른 모든 옵션과 호환되지 않습니다.|  
  
`[ @tracefile = ] 'trace_file'`추적을 기록할 위치와 파일 이름을 지정 합니다. *trace_file* 은 **nvarchar (** 가 수) 이며 기본값은 없습니다. *trace_file* 은 로컬 디렉터리 (예: n ' C:\MSSQL\Trace\trace.trc ') 이거나 공유 또는 경로에 대 한 UNC 일 수 있습니다 \\ \\ *Servername* \\ *Sharename* \\ *Directory*  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 모든 추적 파일 이름에 **.trc** 확장명을 추가 합니다. TRACE_FILE_ROLLOVER 옵션 및 *max_file_size* 지정 된 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 추적 파일이 최대 크기로 확장 될 때 새 추적 파일을 만듭니다. 새 파일의 이름은 원본 파일과 동일 하지만 _ n은 **1**부터 시작 하 여 시퀀스를 나타내는 _*n* 이 추가 됩니다. 예를 들어 첫 번째 추적 파일의 이름이 **filename .trc**인 경우 두 번째 추적 파일의 이름은 **filename_1 .trc**입니다.  
  
 TRACE_FILE_ROLLOVER 옵션을 사용하는 경우 원래 추적 파일 이름에 밑줄 문자를 사용하지 않는 것이 좋습니다. 밑줄을 사용할 경우 다음 동작이 발생합니다.  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]는 롤오버 파일 (이러한 파일 롤오버 옵션 중 하나를 구성 하는 경우)을 자동으로 로드 하거나 로드 하 라는 메시지를 표시 하지 않습니다.  
  
-   Fn_trace_gettable 함수는 원래 파일 이름이 밑줄과 숫자 값으로 끝나는 롤오버 파일 ( *number_files* 인수를 사용 하 여 지정 된 경우)을 로드 하지 않습니다. 이는 파일이 롤오버될 때 자동으로 추가된 밑줄과 숫자에는 적용되지 않습니다.  
  
> [!NOTE]  
>  추적 파일의 이름을 변경하여 원래 파일 이름에서 밑줄을 제거하면 이러한 문제를 모두 해결할 수 있습니다. 예를 들어 원래 파일 이름이 **my_trace .trc**이 고 롤오버 파일의 이름이 **my_trace_1**인 경우에서 파일을 열기 전에 파일 이름을 **mytrace .trc** 및 **mytrace_1 .trc** 로 바꿀 수 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 있습니다.  
  
 TRACE_PRODUCE_BLACKBOX 옵션을 사용 하는 경우 *trace_file* 를 지정할 수 없습니다.  
  
`[ @maxfilesize = ] max_file_size`추적 파일이 증가할 수 있는 최대 크기 (MB)를 지정 합니다. *max_file_size* 는 **bigint**이며 기본값은 **5**입니다.  
  
 이 매개 변수를 TRACE_FILE_ROLLOVER 옵션 없이 지정 하면 사용 된 디스크 공간이 *max_file_size*에 지정 된 크기를 초과할 때 추적에서 파일 기록을 중지 합니다.  
  
`[ @stoptime = ] 'stop_time'`추적이 중지 되는 날짜 및 시간을 지정 합니다. *stop_time* 은 **datetime**이며 기본값은 NULL입니다. NULL일 경우 추적은 수동으로 중지하거나 서버가 시스템을 종료할 때까지 계속 실행됩니다.  
  
 *Stop_time* 와 *max_file_size* 를 모두 지정 하 고 TRACE_FILE_ROLLOVER 지정 하지 않으면 지정 된 중지 시간이 나 최대 파일 크기에 도달할 때 추적이 가장 됩니다. *Stop_time*, *max_file_size*및 TRACE_FILE_ROLLOVER 지정 된 경우 추적이 드라이브를 채우지 않는다고 가정 하 고 지정 된 중지 시간에 추적이 중지 됩니다.  
  
`[ @filecount = ] 'max_rollover_files'`동일한 기본 파일 이름으로 유지할 최대 추적 파일 수를 지정 합니다. *max_rollover_files* 는 **int**이며 1 보다 큽니다. 이 매개 변수는 TRACE_FILE_ROLLOVER 옵션을 지정한 경우에만 유효합니다. *Max_rollover_files* 지정 된 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 새 추적 파일을 열기 전에 가장 오래 된 추적 파일을 삭제 하 여 *max_rollover_files* 추적 파일 수 이하로 유지 하려고 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 기본 파일 이름에 숫자를 추가하여 추적 파일의 보존 기간을 추적합니다.  
  
 예를 들어 *trace_file* 매개 변수가 "c:\mytrace"로 지정 된 경우 이름이 "c:\ mytrace_123" 인 파일은 이름이 "c:\ mytrace_124 .trc" 인 파일 보다 오래 된 것입니다. *Max_rollover_files* 를 2로 설정 하면 추적 파일 "c:\ mytrace_125 .trc"를 만들기 전에 "c:\ mytrace_123 .trc" 파일을 SQL Server 삭제 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 각 파일을 한 번만 삭제하려고 시도하며 다른 프로세스에서 사용 중인 파일은 삭제할 수 없습니다. 그러므로 추적을 실행하는 동안 다른 애플리케이션에서 추적 파일을 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 추적 파일을 파일 시스템에 유지합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 아래 표에서는 저장 프로시저가 완료된 후 사용자가 얻을 수 있는 코드 값을 설명합니다.  
  
|반환 코드|설명|  
|-----------------|-----------------|  
|0|오류가 없습니다.|  
|1|알 수 없는 오류입니다.|  
|10|잘못된 옵션입니다. 지정한 옵션이 호환되지 않으면 반환됩니다.|  
|12|파일이 생성되지 않았습니다.|  
|13|메모리가 부족합니다. 지정한 동작을 수행할 메모리가 충분하지 않으면 반환됩니다.|  
|14|잘못된 중지 시간입니다. 지정한 중지 시간이 이미 지난 경우 반환됩니다.|  
|15|잘못된 매개 변수입니다. 사용자가 호환되지 않는 매개 변수를 제공하면 반환됩니다.|  
  
## <a name="remarks"></a>설명  
 **sp_trace_create** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 SQL Server에서 사용할 수 있는 **xp_trace_ \* ** 확장 저장 프로시저에서 이전에 실행 한 작업을 대부분 수행 하는 저장 프로시저입니다. 대신 **sp_trace_create** 를 사용 합니다.  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_setqueuecreateinfo**  
  
-   **xp_trace_setqueuedestination**  
  
 **sp_trace_create** 는 추적 정의만 만듭니다. 추적을 시작하거나 변경하는 데 사용할 수 없는 저장 프로시저입니다.  
  
 모든 SQL 추적 저장 프로시저 (**sp_trace_xx**)의 매개 변수는 엄격 하 게 형식화 됩니다. 이러한 매개 변수가 정확한 입력 매개 변수 데이터 형식으로 호출되지 않으면 인수 설명에서 지정한 대로 저장 프로시저는 오류를 반환합니다.  
  
 **Sp_trace_create**의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에는 추적 파일 폴더에 대 한 쓰기 권한이 있어야 합니다. 추적 파일이 있는 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정이 관리자가 아닌 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에 명시적으로 쓰기 권한을 부여해야 합니다.  
  
> [!NOTE]  
>  **Fn_trace_gettable** 시스템 함수를 사용 하 여 **sp_trace_create** 를 사용 하 여 만든 추적 파일을 테이블에 자동으로 로드할 수 있습니다. 이 시스템 함수를 사용 하는 방법에 대 한 자세한 내용은 [fn_trace_gettable &#40;transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)을 참조 하십시오.  
  
 추적 저장 프로시저 사용에 대한 예는 [추적 만들기&#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)를 참조하세요.  
  
 **TRACE_PRODUCE_BLACKBOX** 에는 다음과 같은 특징이 있습니다.  
  
-   이 옵션은 롤오버 추적입니다. 기본 *file_count* 은 2 이지만 *filecount* 옵션을 사용 하 여 사용자가 재정의할 수 있습니다.  
  
-   다른 추적과 같은 기본 *file_size* 은 5mb 이며 변경할 수 있습니다.  
  
-   파일 이름을 지정할 수 없습니다. 파일은 **N '%SQLDIR%\MSSQL\DATA\blackbox.trc '** 로 저장 됩니다.  
  
-   이 추적에는 다음과 같은 이벤트와 이러한 이벤트의 열만 포함됩니다.  
  
    -   **RPC starting**  
  
    -   **Batch starting**  
  
    -   **Exception**  
  
    -   **Attention**  
  
-   이 추적에서는 이벤트나 열을 추가 또는 제거할 수 없습니다.  
  
-   이 추적에는 필터를 지정할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 사용자는 ALTER TRACE 권한이 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_trace_generateevent &#40;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [Transact-sql&#41;sp_trace_setevent &#40;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Transact-sql&#41;sp_trace_setfilter &#40;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [Transact-sql&#41;sp_trace_setstatus &#40;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [SQL 추적](../../relational-databases/sql-trace/sql-trace.md)  
  
  
