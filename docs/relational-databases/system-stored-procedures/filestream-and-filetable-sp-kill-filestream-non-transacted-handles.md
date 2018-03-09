---
title: sp_kill_filestream_non_transacted_handles (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_kill_filestream_non_transacted_handles_TSQL
- sp_kill_filestream_non_transacted_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sp_kill_filestream_non_transacted_handles
ms.assetid: 7188353e-ab29-49a0-8f25-7fb8ab122589
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb1054ec1ce9bab7311417e109ac0cece16c9c88
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="filestream-and-filetable---spkillfilestreamnontransactedhandles"></a>Filestream 및 FileTable-sp_kill_filestream_non_transacted_handles
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  FileTable 데이터에 대한 비트랜잭션 핸들 파일을 닫습니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
sp_kill_filestream_non_transacted_handles [[ @table_name = ] ‘table_name’, [[ @handle_id = ] @handle_id]]  
```  
  
## <a name="arguments"></a>인수  
 *table_name*  
 비트랜잭션 핸들을 닫을 테이블의 이름입니다.  
  
 전달할 수 *table_name* 없이 *handle_id* 를 닫으려면 열려 있는 모든 비트랜잭션 핸들 FileTable에 대 한 합니다.  
  
 값에 대해 NULL을 전달할 수 *table_name* 를 닫으려면 열려 있는 모든 비트랜잭션 핸들 현재 데이터베이스의 모든 Filetable에 대 한 합니다. 기본값은 NULL입니다.  
  
 *handle_id*  
 닫을 개별 핸들의 선택적 ID입니다. 가져올 수는 *handle_id* 에서 [sys.dm_filestream_non_transacted_handles&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md) 동적 관리 뷰. 각 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 고유해야 합니다. 지정 하는 경우 *handle_id*에 대 한 값을 제공 해야 한다면 *table_name*합니다.  
  
 값에 대해 NULL을 전달할 수 *handle_id* 를 닫으려면 열려 있는 모든 비트랜잭션 핸들에서 지정한 FileTable에 대 한 *table_name*합니다. 기본값은 NULL입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-set"></a>결과 집합  
 없음  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 *handle_id* 에 필요한 **sp_kill_filestream_non_transacted_handles** 관련이 없는 session_id 또는 다른에 사용 되는 작업 단위 **kill** 명령입니다.  
  
 자세한 내용은 [FileTables 관리](../../relational-databases/blob/manage-filetables.md)를 참조하세요.  
  
## <a name="metadata"></a>메타데이터  
 열려 있는 비트랜잭션 파일 핸들에 대 한 내용은 동적 관리 뷰를 쿼리하려면 [sys.dm_filestream_non_transacted_handles&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md).  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 있어야 **VIEW DATABASE STATE** 파일 핸들을 가져올 수 있는 권한을 **sys.dm_FILESTREAM_non_transacted_handles** 동적 관리 뷰를 실행할 **sp_kill_filestream_non_ transacted_handles**합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 호출 하는 방법을 보여 **sp_kill_filestream_non_transacted_handles** 를 FileTable 데이터에 대 한 비트랜잭션 파일 핸들을 닫아야 합니다.  
  
```sql  
-- Close all open handles in the current database.  
sp_kill_filestream_non_transacted_handles  
  
-- Close all open handles in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = ’myFileTable’  
  
-- Close a specific handle in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = ’myFileTable’, @handle_id = 0xFFFAAADD  
```  
  
 스크립트를 사용 하는 방법을 보여 주는 다음 예제는 *handle_id* 하 고 닫습니다.  
  
```sql  
DECLARE @handle_id varbinary(16);  
DECLARE @table_name sysname;  
  
SELECT TOP 1 @handle_id = handle_id, @table_name = Object_name(table_id)  
FROM sys.dm_FILESTREAM_non_transacted_handles;  
  
EXEC sp_kill_filestream_non_transacted_handles @dbname, @table_name, @handle_id;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [FileTable 관리](../../relational-databases/blob/manage-filetables.md)  
  
  
