---
title: DBCC CHECKCATALOG (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_CHECKCATALOG_TSQL
- DBCC CHECKCATALOG
- CHECKCATALOG_TSQL
- CHECKCATALOG
dev_langs:
- TSQL
helpviewer_keywords:
- catalogs [SQL Server], consistency checks
- checking catalog consistency
- DBCC CHECKCATALOG statement
- integrity [SQL Server], catalogs
- consistency [SQL Server], catalogs
ms.assetid: 8076eb4e-f049-44bf-9a35-45cdd6ef0105
caps.latest.revision: 51
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f63850a2cf39d783daee65431da349d04cba3b03
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-checkcatalog-transact-sql"></a>DBCC CHECKCATALOG(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 데이터베이스 내의 카탈로그 일관성을 검사합니다. 데이터베이스는 온라인 상태여야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DBCC CHECKCATALOG   
[   
    (   
    database_name | database_id | 0  
    )  
]  
    [ WITH NO_INFOMSGS ]   
```  
  
## <a name="arguments"></a>인수  
 *a s e _* | *database_id* | 0  
 카탈로그 일관성을 검사할 데이터베이스의 이름 또는 ID입니다. 아무 값도 지정하지 않거나 0을 지정하면 현재 데이터베이스가 사용됩니다. 데이터베이스 이름에 대 한 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다.  
  
 WITH NO_INFOMSGS  
 모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="remarks"></a>주의  
DBCC CATALOG 명령이 완료된 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 메시지가 기록됩니다. DBCC 명령이 성공적으로 실행되면 메시지에 실행 완료 및 명령이 실행된 소요 시간이 표시됩니다. 오류로 인해 DBCC 명령이 검사를 완료하기 전에 중지되면 메시지에 명령 종료, 상태 값 및 명령이 실행된 소요 시간이 표시됩니다. 다음 표에서는 메시지에 포함될 수 있는 상태 값을 나열하고 설명합니다.
  
|State|Description|  
|-----------|-----------------|  
|0|오류 번호 8930이 발생했습니다. 메타데이터가 손상되어 DBCC 명령이 종료되었음을 나타냅니다.|  
|1.|오류 번호 8967이 발생했습니다. 내부 DBCC 오류가 있습니다.|  
|2|응급 모드 데이터베이스 복구 중에 오류가 발생했습니다.|  
|3|메타데이터가 손상되어 DBCC 명령이 종료되었음을 나타냅니다.|  
|4|어설션 또는 액세스 위반이 감지되었습니다.|  
|5|알 수 없는 오류가 발생하여 DBCC 명령이 종료되었습니다.|  
  
DBCC CHECKCATALOG는 시스템 메타데이터 테이블 간에 다양한 일관성 검사를 수행합니다. DBCC CHECKCATALOG는 내부 데이터베이스 스냅숏을 사용하여 이러한 검사를 수행하는 데 필요한 트랜잭션 일관성을 유지합니다. 자세한 내용은 참조 [데이터베이스 스냅숏 &#40; 스파스 파일의 크기 보기 Transact SQL &#41; ](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) 의 "DBCC 내부 데이터베이스 스냅숏 사용법" 섹션 및 [DBCC &#40; Transact SQL &#41; ](../../t-sql/database-console-commands/dbcc-transact-sql.md).
스냅숏을 만들 수 없는 경우 DBCC CHECKCATALOG는 필요한 일관성을 얻기 위해 배타적 데이터베이스 잠금을 획득합니다. 불일치가 감지되는 경우 복구가 불가능하며 데이터베이스를 백업에서 복원해야 합니다.
  
> [!NOTE]  
>  에 대해 DBCC CHECKCATALOG 실행 **tempdb** 검사를 수행 하지 않습니다. 성능상의 이유로 데이터베이스 스냅숏에 사용할 수 있으므로이 **tempdb**합니다. 즉, 필요한 트랜잭션 일관성을 얻을 수 없음을 의미합니다. 해결 하려면 서버 재생 **tempdb** 메타 데이터 문제입니다.  
  
> [!NOTE]  
>  DBCC CHECKCATALOG는 FILESTREAM 데이터를 검사하지 않습니다. FILESTREAM은 파일 시스템에 BLOB(Binary Large Object)을 저장합니다.  
  
DBCC CHECKCATALOG는의 일부로 실행도 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)합니다.
  
## <a name="result-sets"></a>결과 집합  
데이터베이스가 지정되지 않은 경우 DBCC CHECKCATALOG는 다음을 반환합니다.
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]가 데이터베이스 이름으로 지정된 경우 DBCC CHECKCATALOG는 다음을 반환합니다.
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **sysadmin** 고정 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할입니다.  
  
## <a name="examples"></a>예  
다음 예에서는 현재 데이터베이스와 `AdventureWorks` 데이터베이스 모두의 카탈로그 무결성을 검사합니다.
  
```sql
-- Check the current database.  
DBCC CHECKCATALOG;  
GO  
-- Check the AdventureWorks2012 database.  
DBCC CHECKCATALOG (AdventureWorks2012);  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[시스템 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)
  

