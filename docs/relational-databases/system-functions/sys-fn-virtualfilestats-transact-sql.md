---
description: sys.fn_virtualfilestats(Transact-SQL)
title: sys. fn_virtualfilestats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_virtualfilestats_TSQL
- fn_virtualfilestats
dev_langs:
- TSQL
helpviewer_keywords:
- I/O [SQL Server], statistics
- fn_virtualfilestats function
- sys.fn_virtualfilestats function
- statistical information [SQL Server], I/O
ms.assetid: 96b28abb-b059-48db-be2b-d60fe127f6aa
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fedf4b7412578bb73a717d1646f29ac1471b14ef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481819"
---
# <a name="sysfn_virtualfilestats-transact-sql"></a>sys.fn_virtualfilestats(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  로그 파일을 포함하여 데이터베이스 파일의 I/O 통계를 반환합니다. 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 정보는 [dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) 동적 관리 뷰에서 사용할 수도 있습니다.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
fn_virtualfilestats ( { database_id | NULL } , { file_id | NULL } )  
```  
  
## <a name="arguments"></a>인수  
 *database_id* | NULL  
 데이터베이스의 ID입니다. *database_id*는 **int**이며 기본값은 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 데이터베이스에 대한 정보를 반환하려면 NULL을 지정합니다.  
  
 *file_id* | NULL  
 파일 ID입니다. *file_id* 는 **int**이며 기본값은 없습니다. 데이터베이스의 모든 파일에 대한 정보를 반환하려면 NULL을 지정하십시오.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**DbId**|**smallint**|데이터베이스 ID입니다.|  
|**FileId**|**smallint**|파일의 ID입니다.|  
|**없으면**|**bigint**|데이터를 사용한 시점의 데이터베이스 타임스탬프입니다. **int** 이전 버전의 int [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] . |  
|**NumberReads**|**bigint**|파일에 대해 읽기가 실행된 횟수입니다.|  
|**BytesRead**|**bigint**|파일에 대해 실행된 읽기의 바이트 수입니다.|  
|**IoStallReadMS**|**bigint**|사용자가 파일에 대한 읽기 I/O가 완료될 때까지 대기한 총 시간(밀리초)입니다.|  
|**NumberWrites**|**bigint**|파일에 대해 쓰기가 실행된 횟수입니다.|  
|**BytesWritten**|**bigint**|파일에 대해 실행된 쓰기의 바이트 수입니다.|  
|**IoStallWriteMS**|**bigint**|사용자가 파일에 대한 쓰기 I/O가 완료될 때까지 대기한 총 시간(밀리초)입니다.|  
|**IoStallMS**|**bigint**|**Iostallreadms** 및 **Iostallreadms**의 합계입니다.|  
|**FileHandle**|**bigint**|파일 핸들의 값입니다.|  
|**BytesOnDisk**|**bigint**|디스크에 있는 파일의 실제 크기(바이트)입니다.<br /><br /> 데이터베이스 파일의 경우이 값은 **sys. database_files** **크기** 와 동일 하지만 페이지가 아닌 바이트 단위로 표시 됩니다.<br /><br /> 데이터베이스 스냅샷 스파스 파일의 경우 이 값은 운영 체제에서 파일에 사용 중인 공간입니다.|  
  
## <a name="remarks"></a>설명  
 **fn_virtualfilestats** 는 파일에 대해 수행 된 i/o의 총 수와 같은 통계 정보를 제공 하는 시스템 테이블 반환 함수입니다. 이 함수는 사용자가 파일에 읽기/쓰기를 수행할 때 대기해야 하는 시간의 길이를 추적하는 데 사용됩니다. I/O 작업이 빈번하게 이루어지는 파일을 식별하는 데 사용되기도 합니다.  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-displaying-statistical-information-for-a-database"></a>A. 데이터베이스에 대한 통계 정보 표시  
 다음 예에서는 ID가 `1`인 데이터베이스의 파일 ID 1에 대한 통계 정보를 표시합니다.  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(1, 1);  
GO  
```  
  
### <a name="b-displaying-statistical-information-for-a-named-database-and-file"></a>B. 명명된 데이터베이스 및 파일에 대한 통계 정보 표시  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 예제 데이터베이스의 로그 파일에 대한 통계 정보를 표시합니다. 시스템 함수는 `DB_ID` *database_id* 매개 변수를 지정 하는 데 사용 됩니다.  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(DB_ID(N'AdventureWorks2012'), 2);  
GO  
```  
  
### <a name="c-displaying-statistical-information-for-all-databases-and-files"></a>C. 모든 데이터베이스 및 파일에 대한 통계 정보 표시  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 모든 데이터베이스의 모든 파일에 대한 통계 정보를 표시합니다.  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(NULL,NULL);  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;DB_ID &#40;](../../t-sql/functions/db-id-transact-sql.md)   
 [Transact-sql&#41;FILE_IDEX &#40;](../../t-sql/functions/file-idex-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
