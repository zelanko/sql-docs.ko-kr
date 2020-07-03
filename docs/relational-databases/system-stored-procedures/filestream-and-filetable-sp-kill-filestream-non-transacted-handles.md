---
title: sp_kill_filestream_non_transacted_handles (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_kill_filestream_non_transacted_handles_TSQL
- sp_kill_filestream_non_transacted_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sp_kill_filestream_non_transacted_handles
ms.assetid: 7188353e-ab29-49a0-8f25-7fb8ab122589
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fdceccb1d11ce8818e9f26e46adf6b698e493cd4
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898150"
---
# <a name="sp_kill_filestream_non_transacted_handles-transact-sql"></a>sp_kill_filestream_non_transacted_handles(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  FileTable 데이터에 대한 비트랜잭션 핸들 파일을 닫습니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
sp_kill_filestream_non_transacted_handles [[ @table_name = ] 'table_name', [[ @handle_id = ] @handle_id]]  
```  
  
## <a name="arguments"></a>인수  
 *table_name*  
 비트랜잭션 핸들을 닫을 테이블의 이름입니다.  
  
 FileTable에 대 한 열려 있는 모든 비트랜잭션 핸들을 닫기 위해 *handle_id* 없이 *table_name* 를 전달할 수 있습니다.  
  
 *Table_name* 값에 대해 NULL을 전달 하 여 현재 데이터베이스에 있는 모든 filetable에 대 한 열려 있는 모든 비트랜잭션 핸들을 닫을 수 있습니다. 기본값은 NULL입니다.  
  
 *handle_id*  
 닫을 개별 핸들의 선택적 ID입니다. [Dm_filestream_non_transacted_handles &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md) 동적 관리 뷰에서 *handle_id* 를 가져올 수 있습니다. 각 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 고유해야 합니다. *Handle_id*지정 하는 경우에는 *table_name*에 대 한 값도 제공 해야 합니다.  
  
 *Handle_id* 값에 대해 NULL을 전달 하 여 *Table_name*에서 지정한 FileTable에 대해 열려 있는 모든 비트랜잭션 핸들을 닫을 수 있습니다. 기본값은 NULL입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-set"></a>결과 집합  
 없음  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 **Sp_kill_filestream_non_transacted_handles** 에 필요한 *handle_id* 는 다른 **kill** 명령에 사용 되는 session_id 또는 작업 단위와 관련이 없습니다.  
  
 자세한 내용은 [FileTables 관리](../../relational-databases/blob/manage-filetables.md)를 참조하세요.  
  
## <a name="metadata"></a>메타데이터  
 열려 있는 비트랜잭션 파일 핸들에 대 한 자세한 내용은 동적 관리 뷰 [dm_filestream_non_transacted_handles &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)을 쿼리 합니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 **Dm_FILESTREAM_non_transacted_handles** 동적 관리 뷰에서 파일 핸들을 가져오고 **sp_kill_filestream_non_transacted_handles**를 실행 하려면 **VIEW DATABASE STATE** 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 **sp_kill_filestream_non_transacted_handles** 를 호출 하 여 FileTable 데이터에 대 한 비트랜잭션 파일 핸들을 닫는 방법을 보여 줍니다.  
  
```sql  
-- Close all open handles in the current database.  
sp_kill_filestream_non_transacted_handles  
  
-- Close all open handles in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = 'myFileTable'  
  
-- Close a specific handle in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = 'myFileTable', @handle_id = 0xFFFAAADD  
```  
  
 다음 예제에서는 스크립트를 사용 하 여 *handle_id* 를 가져오고 닫는 방법을 보여 줍니다.  
  
```sql  
DECLARE @handle_id varbinary(16);  
DECLARE @table_name sysname;  
  
SELECT TOP 1 @handle_id = handle_id, @table_name = Object_name(table_id)  
FROM sys.dm_FILESTREAM_non_transacted_handles;  
  
EXEC sp_kill_filestream_non_transacted_handles @dbname, @table_name, @handle_id;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [FileTable 관리](../../relational-databases/blob/manage-filetables.md)  
 [Filestream 및 FileTable 동적 관리 뷰 (Transact-sql)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
 <br>[Filestream 및 FileTable 카탈로그 뷰 (Transact-sql)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
 <br>[sp_filestream_force_garbage_collection(Transact-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)
  
