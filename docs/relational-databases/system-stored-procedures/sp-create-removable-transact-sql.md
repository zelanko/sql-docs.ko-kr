---
title: sp_create_removable (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_create_removable
- sp_create_removable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_removable
ms.assetid: 06e36ae5-f70d-4a26-9a7f-ee4b9360b355
author: stevestein
ms.author: sstein
ms.openlocfilehash: d6f842b96a9b179548688a4c655a566087ba1ebf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68108622"
---
# <a name="sp_create_removable-transact-sql"></a>sp_create_removable(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이동식 미디어 데이터베이스를 작성합니다. 3개 이상(시스템 카탈로그 테이블용으로 하나, 트랜잭션 로그용으로 하나 및 데이터 테이블용으로 하나 이상)의 파일을 작성하고 이러한 파일에 데이터베이스를 놓습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) 를 사용 하는 것이 좋습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_create_removable   
   [ @dbname = ] 'dbname',   
   [ @syslogical= ] 'syslogical',   
   [ @sysphysical = ] 'sysphysical',   
   [ @syssize = ] syssize,   
   [ @loglogical = ] 'loglogical',   
   [ @logphysical = ] 'logphysical',   
   [ @logsize = ] logsize,   
   [ @datalogical1 = ] 'datalogical1',   
   [ @dataphysical1 = ] 'dataphysical1',   
   [ @datasize1 = ] datasize1 ,   
   [ @datalogical16 = ] 'datalogical16',   
   [ @dataphysical16 = ] 'dataphysical16',   
   [ @datasize16 = ] datasize16 ]  
```  
  
## <a name="arguments"></a>인수  
`[ @dbname = ] 'dbname'`이동식 미디어에서 사용 하기 위해 만들 데이터베이스의 이름입니다. *dbname* 은 **sysname**입니다.  
  
`[ @syslogical = ] 'syslogical'`시스템 카탈로그 테이블을 포함 하는 파일의 논리적 이름입니다. *syslogical* 은 **sysname**입니다.  
  
`[ @sysphysical = ] 'sysphysical'`물리적 이름입니다. 여기에는 시스템 카탈로그 테이블을 보유하고 있는 파일의 정규화된 경로가 포함됩니다. *sysphysical* 은 **nvarchar (260)** 입니다.  
  
`[ @syssize = ] syssize`시스템 카탈로그 테이블을 보유 하는 파일의 크기 (mb)입니다. *syssize* 는 **int**입니다. 최소 *syssize* 는 1입니다.  
  
`[ @loglogical = ] 'loglogical'`트랜잭션 로그를 포함 하는 파일의 논리적 이름입니다. *loglogical* 은 **sysname**입니다.  
  
`[ @logphysical = ] 'logphysical'`물리적 이름입니다. 여기에는 트랜잭션 로그가 있는 파일의 정규화된 경로가 포함됩니다. *logphysical* 는 **nvarchar (260)** 입니다.  
  
`[ @logsize = ] logsize`트랜잭션 로그를 포함 하는 파일의 크기 (mb)입니다. *logsize* 는 **int**입니다. 최소 *logsize* 는 1입니다.  
  
`[ @datalogical1 = ] 'datalogical'`데이터 테이블을 포함 하는 파일의 논리적 이름입니다. *datalogical* 는 **sysname**입니다.  
  
 1개에서 16개까지의 데이터 파일이 있어야 합니다. 일반적으로 데이터베이스가 대형일 것으로 예상되며 여러 디스크에 배포되어야 할 때 두 개 이상의 데이터 파일이 작성됩니다.  
  
`[ @dataphysical1 = ] 'dataphysical'`물리적 이름입니다. 여기에는 데이터 테이블을 포함하는 파일의 정규화된 경로가 포함됩니다. *dataphysical* 은 **nvarchar (260)** 입니다.  
  
`[ @datasize1 = ] 'datasize'`데이터 테이블을 포함 하는 파일의 크기 (mb)입니다. *datasize* 는 **int**입니다. 최소 *datasize* 는 1입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 CD 등과 같은 이동식 미디어에 데이터베이스를 복사하여 다른 사용자에게 배포하고자 하는 경우에는 이 저장 프로시저를 사용하십시오.  
  
## <a name="permissions"></a>사용 권한  
 CREATE DATABASE, CREATE ANY DATABASE 또는 ALTER ANY DATABASE 권한이 필요합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디스크 사용을 제어하기 위해 일반적으로 데이터베이스를 만들 수 있는 사용 권한은 일부 로그인 계정으로 제한됩니다.  
  
### <a name="permissions-on-data-and-log-files"></a>데이터 및 로그 파일에 대한 사용 권한  
 데이터베이스에 대해 특정 작업이 수행될 때마다 데이터베이스의 데이터 및 로그 파일에 해당 사용 권한이 설정됩니다. 이러한 사용 권한을 설정하면 누구나 액세스할 수 있는 디렉터리에 있는 파일이 실수로 변경되는 것을 방지할 수 있습니다.  
  
|데이터베이스에 대한 작업|파일에 사용 권한 설정|  
|---------------------------|------------------------------|  
|새 파일을 추가하기 위해 수정됨|생성일|  
|백업|연결|  
|복원|분리|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 데이터 및 로그 파일 권한을 설정하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `inventory` 데이터베이스를 이동식 데이터베이스로 만듭니다.  
  
```  
EXEC sp_create_removable 'inventory',   
   'invsys',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invsys.mdf'  
, 2,   
   'invlog',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invlog.ldf', 4,  
   'invdata',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invdata.ndf',   
10;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 분리 및 연결 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [Transact-sql&#41;sp_certify_removable &#40;](../../relational-databases/system-stored-procedures/sp-certify-removable-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Transact-sql&#41;sp_dbremove &#40;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [Transact-sql&#41;sp_detach_db &#40;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [Transact-sql&#41;sp_helpfile &#40;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [Transact-sql&#41;sp_helpfilegroup &#40;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
