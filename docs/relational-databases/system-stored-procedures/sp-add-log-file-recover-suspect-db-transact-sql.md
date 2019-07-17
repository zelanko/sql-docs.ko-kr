---
title: sp_add_log_file_recover_suspect_db (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_file_recover_suspect_db_TSQL
- sp_add_log_file_recover_suspect_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_file_recover_suspect_db
ms.assetid: b41ca3a5-7222-4c22-a012-e66a577a82f6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9f951aaee96bccf0c2876c781aaebdd2a009b51d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140483"
---
# <a name="spaddlogfilerecoversuspectdb-transact-sql"></a>sp_add_log_file_recover_suspect_db(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로그 공간 부족(9002 오류)으로 인해 데이터베이스를 완벽하게 복구하지 못했을 때 파일 그룹에 로그 파일을 추가합니다. 파일을 추가한 후 **sp_add_log_file_recover_suspect_db** 주의 대상 설정을 해제 하 고 데이터베이스의 복구를 완료 합니다. 매개 변수는 ALTER DATABASE에 대 한 것과 동일 *database_name* 로그 파일을 추가 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_log_file_recover_suspect_db [ @dbName= ] 'database' ,   
    [ @name = ] 'logical_file_name' ,   
    [ @filename= ] 'os_file_name' ,   
    [ @size = ] 'size' ,   
    [ @maxsize = ] 'max_size' ,   
    [ @filegrowth = ] 'growth_increment'  
```  
  
## <a name="arguments"></a>인수  
`[ @dbName = ] 'database'` 데이터베이스의 이름이입니다. *데이터베이스* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @name = ] 'logical_file_name'` 사용 하는 이름을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 파일을 참조 합니다. 이 이름은 서버에서 고유해야 합니다. *logical_file_name* 됩니다 **nvarchar(260)** , 기본값은 없습니다.  
  
`[ @filename = ] 'os_file_name'` 경로 및 파일 이름은 운영 체제에서 파일에 사용 합니다. 파일은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 설치된 서버에 있어야 합니다. *os_file_name* 됩니다 **nvarchar(260)** , 기본값은 없습니다.  
  
`[ @size = ] 'size_ '` 파일의 초기 크기가입니다. *크기* 됩니다 **nvarchar(20)** , 기본값은 NULL입니다. 소수점이 포함되지 않은 정수를 지정하십시오. 메가바이트를 지정하려면 MB를, 킬로바이트를 지정하려면 KB를 사용합니다. 기본값은 MB입니다. 최소값은 512KB입니다. 하는 경우 *크기* 지정 하지 않으면 기본값은 1MB입니다.  
  
`[ @maxsize = ] 'max_size_ '` 파일이 증가할 수 있는 최대 크기가입니다. *max_size* 됩니다 **nvarchar(20)** , 기본값은 NULL입니다. 소수점이 포함되지 않은 정수를 지정하십시오. 메가바이트를 지정하려면 MB를, 킬로바이트를 지정하려면 KB를 사용합니다. 기본값은 MB입니다.  
  
 하는 경우 *max_size* 지정 하지 않으면 디스크가 꽉 찰 때까지 파일이 커집니다. 디스크가 꽉 차는 시점이 되면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 응용 프로그램 로그에서 관리자에게 경고 메시지를 표시합니다.  
  
`[ @filegrowth = ] 'growth_increment_ '` 공간이 새로 필요할 때마다 파일에 추가 하는 공간의 크기가입니다. *growth_increment* 됩니다 **nvarchar(20)** , 기본값은 NULL입니다. 값 0은 증가하지 않음을 나타냅니다. 소수점이 포함되지 않은 정수를 지정하십시오. 값은 MB, KB 또는 %로 지정할 수 있습니다. %가 지정된 경우, 증가분은 공간이 증가될 당시의 파일 크기의 지정된 비율을 의미합니다. MB, KB 또는 % 접미사를 붙이지 않고 숫자를 지정하면 MB가 기본값이 됩니다.  
  
 하는 경우 *growth_increment* NULL 이며 기본값은 10%가 최소 크기 값은 64KB입니다. 지정한 크기는 64KB 단위로 반올림됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>사용 권한  
 실행 권한은 기본적으로 멤버를 **sysadmin** 고정된 서버 역할입니다. 이 권한은 이전할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `db1` 데이터베이스가 로그 공간이 부족(9002 오류)하여 복구하는 동안 주의 대상으로 표시되었습니다.  
  
```  
USE master;  
GO  
EXEC sp_add_log_file_recover_suspect_db db1, logfile2,  
'C:\Program Files\Microsoft SQL  
    Server\MSSQL13.MSSQLSERVER\MSSQL\Data\db1_logfile2.ldf',   
    '1MB';  
```  
  
## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_add_data_file_recover_suspect_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-data-file-recover-suspect-db-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
