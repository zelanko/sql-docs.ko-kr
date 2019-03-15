---
title: sp_filestream_force_garbage_collection (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_filestream_force_garbage_collection
- sp_filestream_force_garbage_collection_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FILESTREAM [SQL Server]
- sp_filestream_force_garbage_collection
ms.assetid: 9d1efde6-8fa4-42ac-80e5-37456ffebd0b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e95110bdbbfbe0f5ca6ff453045cc4f759163036
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57973682"
---
# <a name="spfilestreamforcegarbagecollection-transact-sql"></a>sp_filestream_force_garbage_collection(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  FILESTREAM 가비지 수집기를 실행하고 불필요한 FILESTREAM 파일을 삭제합니다.  
  
 가비지 수집기를 사용하여 FILESTREAM 컨테이너 안의 삭제된 파일을 모두 정리해야 해당 컨테이너를 제거할 수 있습니다. FILESTREAM 가비지 수집기는 자동으로 실행됩니다. 그러나 필요한 경우에 가비지 수집기가 되기 전에 컨테이너를 제거 하려면 실행, sp_filestream_force_garbage_collection를 사용 하 여 가비지 수집기를 수동으로 실행할 수 있습니다.  
  
  
## <a name="syntax"></a>구문  
  
```  
sp_filestream_force_garbage_collection  
    [ @dbname = ]  'database_name',  
    [ @filename = ] 'logical_file_name' ]  
```  
  
## <a name="arguments"></a>인수  
 **@dbname** = *database_name* 가비지 수집기를 실행할 데이터베이스의 이름을 표시 합니다.  
  
> [!NOTE]  
>  *dbname* 됩니다 **sysname**합니다. 지정하지 않으면 현재 데이터베이스로 가정합니다.  
  
 **@filename** = *logical_file_name*  
 가비지 수집기를 실행할 FILESTREAM 컨테이너의 논리적 이름을 지정합니다. **@filename** 선택 사항입니다. 없는 논리적 파일 이름을 지정 된 경우 가비지 수집기가 지정한 데이터베이스의 FILESTREAM 컨테이너를 모두 정리 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
  
|||  
|-|-|  
|값|Description|  
|0|작업 성공|  
|1|작업 실패|  
  
## <a name="result-sets"></a>결과 집합  
  
|값|Description|  
|-----------|-----------------|  
|*file_name*|FILESTREAM 컨테이너 이름을 나타냅니다.|  
|*num_collected_items*|이 컨테이너에서 가비지 수집된(삭제된) FILESTREAM 항목(파일/디렉터리) 수를 나타냅니다.|  
|*num_marked_for_collection_items*|이 컨테이너에서 가비지 수집을 위해 표시된 FILESTREAM 항목(파일/디렉터리) 수를 나타냅니다. 이러한 항목은 아직 삭제 되지 않은 되지만 가비지 수집 단계를 수행 하는 삭제할 수 있습니다.|  
|*num_unprocessed_items*|이 FILESTREAM 컨테이너에서 가비지 수집을 위해 처리되지 적합한 FILESTREAM 항목(파일 또는 디렉터리) 수를 나타냅니다. 다음을 비롯하여 다양한 이유로 항목이 처리되지 않을 수 있습니다.<br /><br /> 로그 백업 또는 검사점을 가져오지 않아 파일이 고정되어야 하는 경우<br /><br /> FULL 또는 BULK_LOGGED 복구 모델의 파일인 경우<br /><br /> 장기 실행 활성 트랜잭션이 있는 경우<br /><br /> 복제 로그 판독기 작업이 실행 되지 않았습니다. 백서를 참조 하세요 [SQL Server 2008의 FILESTREAM 저장소](https://go.microsoft.com/fwlink/?LinkId=209156) 자세한 내용은 합니다.|  
|*last_collected_xact_seqno*|지정한 FILESTREAM 컨테이너에 대해 파일이 가비지 수집된 마지막 해당 LSN(로그 시퀀스 번호)을 반환합니다.|  
  
## <a name="remarks"></a>Remarks  
 요청한 데이터베이스 및 FILESTREAM컨테이너에서 완료될 때까지 FILESTREAM 가비지 수집기 태스크를 명시적으로 실행합니다. 더 이상 필요하지 않은 파일은 가비지 수집 프로세스에서 제거됩니다. 이 작업을 완료하는 데 필요한 시간은 최근에 FILESTREAM 데이터에 발생한 DML 작업의 양과 해당 데이터베이스 또는 컨테이너에 있는 FILESTREAM 데이터의 크기에 따라 결정됩니다. 데이터베이스를 온라인 상태로 설정하여 이 작업을 실행할 수 있지만 그러면 가비지 수집 프로세스가 수행하는 여러 I/O 작업으로 인해 실행 중에 데이터베이스 성능이 저하될 수 있습니다.  
  
> [!NOTE]  
>  평소 업무 시간 외에 꼭 필요할 때만 이 작업을 실행하는 것이 좋습니다.  
  
별도의 컨테이너 또는 별도의 데이터베이스에서만 이 저장 프로시저의 여러 호출을 동시에 실행할 수 있습니다.  

2 단계 작업으로 인해 실제로 기본 Filestream 파일을 삭제 하려면 두 번 저장된 프로시저를 실행 해야 합니다.  

GC (가비지 수집) 로그 잘라내기에 의존합니다. 따라서 파일 최근에 전체 복구 모델을 사용 하 여 데이터베이스에서 삭제 한 후에 이러한 트랜잭션 로그 부분의 로그 백업을 수행 되 고 로그 부분을 비활성 상태로 표시 됩니다 GC ed 됩니다. 단순 복구 모델을 사용 하 여 데이터베이스에 대 한 로그 잘림이 `CHECKPOINT` 가 데이터베이스에 대해 발급 되었습니다.  


## <a name="permissions"></a>사용 권한  
 db_owner 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `FSDB` 데이터베이스의 FILESTREAM 컨테이너에 대해 가비지 수집기를 실행합니다.  
  
### <a name="a-specifying-no-container"></a>1. 컨테이너 지정 안 함  
  
```sql  
USE FSDB;  
GO  
EXEC sp_filestream_force_garbage_collection @dbname = N'FSDB';  
```  
  
### <a name="b-specifying-a-container"></a>2. 컨테이너 지정  
  
```sql  
USE FSDB;  
GO  
EXEC sp_filestream_force_garbage_collection @dbname = N'FSDB',
    @filename = N'FSContainer';  
```  
  
## <a name="see-also"></a>관련 항목  
[Filestream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream 및 FileTable 동적 관리 뷰(Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream 및 FileTable 카탈로그 뷰(Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[sp_kill_filestream_non_transacted_handles (TRANSACT-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)
  
  
