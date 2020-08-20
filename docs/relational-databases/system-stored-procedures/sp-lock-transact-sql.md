---
description: sp_lock(Transact-SQL)
title: sp_lock (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_lock_TSQL
- sp_lock
dev_langs:
- TSQL
helpviewer_keywords:
- sp_lock
ms.assetid: 9eaa0ec2-2ad9-457c-ae48-8da92a03dcb0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f8fee809f67de959c7d168ceaac2016b5cddddd9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481152"
---
# <a name="sp_lock-transact-sql"></a>sp_lock(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  잠금에 대한 정보를 보고합니다.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 의 잠금에 대 한 정보를 얻으려면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] [dm_tran_locks](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md) 동적 관리 뷰를 사용 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_lock [ [ @spid1 = ] 'session ID1' ] [ , [@spid2 = ] 'session ID2' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
`[ @spid1 = ] 'session ID1'` 사용자가 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 잠금 정보를 필요로 하는 **sys. dm_exec_sessions** 의 세션 ID 번호입니다. *SESSION ID1* 는 **int** 이며 기본값은 NULL입니다. **Sp_who** 를 실행 하 여 세션에 대 한 프로세스 정보를 가져옵니다. *SESSION ID1* 를 지정 하지 않으면 모든 잠금에 대 한 정보가 표시 됩니다.  
  
`[ @spid2 = ] 'session ID2'` 은 (는) [!INCLUDE[ssDE](../../includes/ssde-md.md)] ID1의 다른 세션 ID 번호입니다 **dm_exec_sessions.** *세션* 을 사용 하는 동시에 잠금이 있을 수 있으며 사용자가 정보를 필요로 하는 경우에도 마찬가지입니다. *SESSION ID2* 는 **int** 이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 **Sp_lock** 결과 집합은 ** \@ spid1** 및 ** \@ spid2** 매개 변수에 지정 된 세션이 보유 한 각 잠금에 대해 하나의 행을 포함 합니다. ** \@ Spid1** 또는 ** \@ spid2** 를 모두 지정 하지 않을 경우 결과 집합은 인스턴스에서 현재 활성 상태인 모든 세션에 대 한 잠금을 보고 합니다 [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**spid**|**smallint**|잠금을 요청하는 프로세스의 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 세션 ID입니다.|  
|**dbid**|**smallint**|잠금이 설정된 데이터베이스의 ID입니다. DB_NAME() 함수를 사용하여 데이터베이스를 식별할 수 있습니다.|  
|**ObjId**|**int**|잠금이 설정된 개체의 ID입니다. 관련 데이터베이스에서 OBJECT_NAME() 함수를 사용하여 개체를 식별할 수 있습니다. 값 99는 특별한 경우로서 데이터베이스에서 페이지 할당을 기록하는 데 사용되는 시스템 페이지 중 하나에 대한 잠금을 나타냅니다.|  
|**IndId**|**smallint**|잠금이 설정된 인덱스의 ID입니다.|  
|**유형**|**nchar (4)**|잠금 유형입니다.<br /><br /> RID = RID(행 식별자)로 식별되는 테이블의 단일 행에 대한 잠금입니다.<br /><br /> KEY = 직렬화할 수 있는 트랜잭션에서 키의 범위를 보호하는 인덱스 내의 잠금입니다.<br /><br /> PAG = 데이터 또는 인덱스 페이지에 대한 잠금입니다.<br /><br /> EXT = 익스텐트에 대한 잠금입니다.<br /><br /> TAB = 모든 데이터와 인덱스가 포함된 전체 테이블에 대한 잠금입니다.<br /><br /> DB = 데이터베이스에 대한 잠금입니다.<br /><br /> FIL = 데이터베이스 파일에 대한 잠금입니다.<br /><br /> APP = 애플리케이션이 지정한 리소스에 대한 잠금입니다.<br /><br /> MD = 메타데이터 또는 카탈로그 정보에 대한 잠금입니다.<br /><br /> HBT = 힙 또는 B-트리의 잠금 (HoBT). 이 정보는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 완전하지 않습니다.<br /><br /> AU = 할당 단위에 대한 잠금입니다. 이 정보는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 완전하지 않습니다.|  
|**리소스**|**nchar(32)**|잠긴 리소스를 식별하는 값입니다. 값의 형식은 **유형** 열에서 식별 되는 리소스 유형에 따라 달라 집니다.<br /><br /> **유형** 값: **리소스** 값<br /><br /> RID: fileid: pagenumber: rid 형식의 식별자입니다. 여기서 fileid는 페이지가 포함 된 파일을 식별 하 고 pagenumber는 행이 포함 된 페이지를 식별 하며 rid는 페이지의 특정 행을 식별 합니다. fileid는 **database_files** 카탈로그 뷰의 **file_id** 열과 일치 합니다.<br /><br /> 키:에서 내부적으로 사용 되는 16 진수 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 입니다.<br /><br /> PAG: fileid: pagenumber 형식의 숫자입니다. 여기서 fileid는 페이지가 포함 된 파일을 식별 하 고 pagenumber는 페이지를 식별 합니다.<br /><br /> EXT: 익스텐트의 첫 번째 페이지를 식별 하는 번호입니다. 이 번호의 형식은 fileid:pagenumber입니다.<br /><br /> 탭: **ObjId** 열에서 테이블이 이미 식별 되었으므로 정보가 제공 되지 않습니다.<br /><br /> DB: **dbid** 열에서 데이터베이스가 이미 식별 되었으므로 정보가 제공 되지 않았습니다.<br /><br /> FIL: **database_files** 카탈로그 뷰의 **file_id** 열과 일치 하는 파일의 식별자입니다.<br /><br /> 앱: 잠겨 있는 응용 프로그램 리소스에 고유한 식별자입니다. DbPrincipleId: 형식으로 지정 \<first two to 16 characters of the resource string> \<hashed value> 합니다.<br /><br /> MD: 리소스 유형에 따라 달라집니다. 자세한 내용은 [dm_tran_locks &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)에서 **resource_description** 열에 대 한 설명을 참조 하세요.<br /><br /> HBT: 제공 된 정보가 없습니다. 대신 **dm_tran_locks** 동적 관리 뷰를 사용 하십시오.<br /><br /> AU: 제공 된 정보가 없습니다. 대신 **dm_tran_locks** 동적 관리 뷰를 사용 하십시오.|  
|**모드**|**nvarchar(8)**|요청한 잠금 모드입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> NULL = 리소스에 대해 허가된 액세스가 없습니다. 자리 표시자 역할을 합니다.<br /><br /> Sch-S = 스키마 안전성. 특정 세션이 스키마 요소에 대해 스키마 안전성 잠금을 보유하고 있는 동안 테이블 또는 인덱스 등의 스키마 요소가 삭제되지 않도록 합니다.<br /><br /> Sch-M = 스키마 수정. 지정한 리소스의 스키마를 변경하려는 세션이 보유해야 하는 잠금 모드입니다. 다른 세션이 표시된 개체를 참조하지 않도록 합니다.<br /><br /> S = 공유. 보유 중인 세션이 리소스에 공유된 액세스를 할 수 있도록 권한을 부여합니다.<br /><br /> U = 업데이트. 업데이트될 리소스에 대해 업데이트 잠금을 획득하도록 합니다. 이후에 업데이트할 가능성을 위해 여러 세션이 리소스를 잠그는 경우 발생하는 일반적인 형태의 교착 상태를 방지하기 위해 사용합니다.<br /><br /> X = 배타. 보유 중인 세션이 리소스에 배타적으로 액세스할 수 있도록 권한을 부여합니다.<br /><br /> IS = 내재된 공유. 잠금 계층 구조의 일부 하위 리소스에 S 잠금을 설정하려는 의도를 표시합니다.<br /><br /> IU = 의도 업데이트. 잠금 계층 구조의 일부 하위 리소스에 U 잠금을 설정하려는 의도를 표시합니다.<br /><br /> IX = 의도 배타. 잠금 계층 구조의 일부 하위 리소스에 X 잠금을 설정하려는 의도를 표시합니다.<br /><br /> SIU = 공유 의도 업데이트. 잠금 계층 구조의 하위 리소스에 대한 업데이트 잠금을 획득하기 위해 리소스에 대한 공유된 액세스를 표시합니다.<br /><br /> SIX = 공유 의도 배타. 잠금 계층 구조의 하위 리소스에 대한 배타적 잠금을 획득하기 위해 리소스에 대한 공유된 액세스를 표시합니다.<br /><br /> UIX = 업데이트 의도 배타. 잠금 계층 구조의 하위 리소스에 대한 배타적 잠금을 획득하기 위해 리소스에 업데이트 잠금을 보유함을 표시합니다.<br /><br /> BU = 대량 업데이트. 대량 작업에 사용합니다.<br /><br /> RangeS_S = 공유 키 범위 및 공유 리소스 잠금. 직렬화 가능 범위 검색을 표시합니다.<br /><br /> RangeS_U = 공유 키 범위 및 업데이트 리소스 잠금. 직렬화 가능 업데이트 검색을 표시합니다.<br /><br /> RangeI_N = 삽입 키 범위 및 Null 리소스 잠금. 새 키를 인덱스에 삽입하기 전에 범위를 테스트하는 데 사용됩니다.<br /><br /> RangeI_S = 키 범위 변환 잠금. RangeI_N 및 S 잠금의 겹침으로 생성됩니다.<br /><br /> RangeI_U =  RangeI_N 및 U 잠금의 겹침으로 생성된 키 범위 변환 잠금.<br /><br /> RangeI_X =  RangeI_N 및 X 잠금의 겹침으로 생성된 키 범위 변환 잠금.<br /><br /> RangeI_X_S = RangeI_N 및 RangeS_S 잠금의 겹침으로 생성된 키 범위 변환 잠금입니다.<br /><br /> RangeI_X_U = RangeI_N 및 RangeS_U 잠금의 겹침으로 생성된 키 범위 변환 잠금.<br /><br /> RangeX_X = 배타 키 범위 및 배타 리소스 잠금. 범위 내에서 키를 업데이트할 때 사용되는 변환 잠금입니다.|  
|**상태**|**nvarchar (5)**|잠금 요청 상태입니다.<br /><br /> CNVRT: 다른 모드에서 잠금을 변환 중이지만 충돌 하는 모드의 잠금을 보유 하는 다른 프로세스에 의해 변환이 차단 됩니다.<br /><br /> GRANT: 잠금을 가져왔습니다.<br /><br /> 대기: 충돌 하는 모드의 잠금을 보유 하는 다른 프로세스에 의해 잠금이 차단 되었습니다.|  
  
## <a name="remarks"></a>설명  
 다음과 같은 방법으로 읽기 작업의 잠금을 제어할 수 있습니다.  
  
-   SET TRANSACTION ISOLATION LEVEL을 사용하여 세션의 잠금 수준을 지정합니다. 구문 및 제한 사항에 대 한 자세한 내용은 [트랜잭션 격리 수준 설정 &#40;transact-sql&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조 하세요.  
  
-   FROM 절에서 테이블 잠금 힌트를 사용하여 테이블의 개별 참조에 대한 잠금 수준을 지정합니다. 구문 및 제한 사항에 대해서는 [transact-sql&#41;&#40;테이블 힌트 ](../../t-sql/queries/hints-transact-sql-table.md)를 참조 하세요.  
  
 세션과 연결되지 않은 모든 분산 트랜잭션은 분리된 트랜잭션입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 모든 분리된 트랜잭션에 SPID 값으로 -2를 할당하여 사용자가 차단 분산 트랜잭션을 쉽게 식별하도록 합니다. 자세한 내용은 [표시된 트랜잭션을 사용하여 관련 데이터베이스를 일관되게 복구&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-listing-all-locks"></a>A. 모든 잠금 나열  
 다음 예에서는 현재 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 보유된 모든 잠금에 대한 정보를 표시합니다.  
  
```sql  
USE master;  
GO  
EXEC sp_lock;  
GO  
```  
  
### <a name="b-listing-a-lock-from-a-single-server-process"></a>B. 단일 서버 프로세스의 잠금 나열  
 다음 예에서는 프로세스 ID `53`에 대해 잠금을 포함한 정보를 표시합니다.  
  
```sql  
USE master;  
GO  
EXEC sp_lock 53;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)   
 [Transact-sql&#41;DB_NAME &#40;](../../t-sql/functions/db-name-transact-sql.md)   
 [KILL &#40;Transact-sql&#41;](../../t-sql/language-elements/kill-transact-sql.md)   
 [Transact-sql&#41;OBJECT_NAME &#40;](../../t-sql/functions/object-name-transact-sql.md)   
 [Transact-sql&#41;sp_who &#40;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [dm_os_tasks &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [sys.dm_os_threads&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)  
  
  
