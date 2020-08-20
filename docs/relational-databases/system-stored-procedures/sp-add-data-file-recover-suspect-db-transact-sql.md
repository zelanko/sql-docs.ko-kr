---
description: sp_add_data_file_recover_suspect_db(Transact-SQL)
title: sp_add_data_file_recover_suspect_db (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_data_file_recover_suspect_db
- sp_add_data_file_recover_suspect_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_data_file_recover_suspect_db
ms.assetid: b25262aa-a228-48b7-8739-6581c760b171
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ae07b655dd7b693876c61b600315ac8874d988ff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481665"
---
# <a name="sp_add_data_file_recover_suspect_db-transact-sql"></a>sp_add_data_file_recover_suspect_db(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  파일 그룹의 공간 부족(1105 오류)으로 인해 데이터베이스를 완벽하게 복구하지 못했을 때 파일 그룹에 데이터 파일을 추가합니다. 파일이 추가된 다음에는 이 저장 프로시저가 주의 대상 설정을 해제하고 데이터베이스를 완벽하게 복구합니다. 매개 변수는 ALTER DATABASE *DATABASE_NAME* 파일 추가와 동일 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_data_file_recover_suspect_db [ @dbName= ] 'database'   
    , [ @filegroup = ] 'filegroup_name'   
    , [ @name = ] 'logical_file_name'   
    , [ @filename= ] 'os_file_name'   
    , [ @size = ] 'size'   
    , [ @maxsize = ] 'max_size'   
    , [ @filegrowth = ] 'growth_increment'  
```  
  
## <a name="arguments"></a>인수  
`[ @dbName = ] 'database_ '` 데이터베이스의 이름입니다. *데이터베이스* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @filegroup = ] 'filegroup_name_ '` 파일을 추가할 파일 그룹입니다. *filegroup_name* 은 **nvarchar (260)** 이며 기본값은 주 파일을 나타내는 NULL입니다.  
  
`[ @name = ] 'logical_file_name_ '` 는에서 파일을 참조 하는 데 사용 되는 이름입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이 이름은 서버에서 고유해야 합니다. *logical_file_name* 은 **nvarchar (260)** 이며 기본값은 없습니다.  
  
`[ @filename = ] 'os_file_name_ '` 운영 체제에서 파일에 사용 하는 경로 및 파일 이름입니다. 파일은 반드시 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 인스턴스에 있어야 합니다. *os_file_name* 은 **nvarchar (260)** 이며 기본값은 없습니다.  
  
`[ @size = ] 'size_ '` 파일의 초기 크기입니다. *크기* 는 **nvarchar (20)** 이며 기본값은 NULL입니다. 소수점이 포함되지 않은 정수를 지정하십시오. 메가바이트를 지정하려면 MB를, 킬로바이트를 지정하려면 KB를 사용합니다. 기본값은 MB입니다. 최소값은 512KB입니다. *Size* 를 지정 하지 않으면 기본값은 1mb입니다.  
  
`[ @maxsize = ] 'max_size_ '` 파일이 증가할 수 있는 최대 크기입니다. *max_size* 은 **nvarchar (20)** 이며 기본값은 NULL입니다. 소수점이 포함되지 않은 정수를 지정하십시오. 메가바이트를 지정하려면 MB를, 킬로바이트를 지정하려면 KB를 사용합니다. 기본값은 MB입니다.  
  
 *Max_size* 지정 하지 않으면 디스크가 꽉 찼을 때까지 파일이 증가 합니다. 디스크가 꽉 차는 시점이 되면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 애플리케이션 로그에서 관리자에게 경고 메시지를 표시합니다.  
  
`[ @filegrowth = ] 'growth_increment_ '` 새 공간이 필요할 때마다 파일에 추가 되는 공간 크기입니다. *growth_increment* 은 **nvarchar (20)** 이며 기본값은 NULL입니다. 값 0은 증가하지 않음을 나타냅니다. 소수점이 포함되지 않은 정수를 지정하십시오. 값은 MB, KB 또는 %로 지정할 수 있습니다. %가 지정된 경우, 증가분은 공간이 증가될 당시의 파일 크기의 지정된 비율을 의미합니다. MB, KB 또는 % 접미사를 붙이지 않고 숫자를 지정하면 MB가 기본값이 됩니다.  
  
 *GROWTH_INCREMENT* NULL 이면 기본값은 10%이 고 최소 값은 64입니다. 지정한 크기는 64KB 단위로 반올림됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 Execute 권한은 **sysadmin** 고정 서버 역할의 멤버에 게 기본적으로 부여 됩니다. 이 권한은 이전할 수 없습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `db1` 데이터베이스가 `fg1` 파일 그룹에서 공간 부족(1105 오류)으로 인해 복구하는 동안 주의 대상으로 표시되었습니다.  
  
```  
USE master;  
GO  
EXEC sp_add_data_file_recover_suspect_db db1, fg1, file2,  
    'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\db1_file2.mdf', '1MB';  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE &#40;Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Transact-sql&#41;sp_add_log_file_recover_suspect_db &#40;](../../relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
