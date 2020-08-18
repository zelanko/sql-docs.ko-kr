---
description: sys.dm_filestream_non_transacted_handles(Transact-SQL)
title: sys. dm_filestream_non_transacted_handles (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_filestream_non_transacted_handles_TSQL
- dm_filestream_non_transacted_handles
- dm_filestream_non_transacted_handles_TSQL
- sys.dm_filestream_non_transacted_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_non_transacted_handles dynamic management view
ms.assetid: 507ec125-67dc-450a-9081-94cde5444a92
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d38b5e210e5a9c7a0b75d2ecb619ae84a61373e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88398739"
---
# <a name="sysdm_filestream_non_transacted_handles-transact-sql"></a>sys.dm_filestream_non_transacted_handles(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  FileTable 데이터와 연결된 현재 열려 있는 비트랜잭션 파일 핸들을 표시합니다.  
  
 이 뷰는 열려 있는 파일 핸들마다 하나의 행을 포함합니다. 이 뷰의 데이터는 서버의 현재 내부 상태에 따라 달라지므로 핸들이 열리고 닫힐 때마다 지속적으로 변경됩니다. 이 뷰에는 기록 정보가 없습니다.  
  
 자세한 내용은 [FileTables 관리](../../relational-databases/blob/manage-filetables.md)를 참조하세요.  
  
|**열**|**형식**|**설명**|  
|----------------|--------------|---------------------|  
|database_id|int|핸들과 연결된 데이터베이스의 ID입니다.|  
|object_id|int|핸들이 연결된 FileTable의 개체 ID입니다.|  
|handle_id|int|고유한 핸들 컨텍스트 식별자입니다. [Sp_kill_filestream_non_transacted_handles &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md) 저장 프로시저에서 특정 핸들을 중지 하는 데 사용 됩니다.|  
|file_object_type|int|핸들의 유형입니다. 이 열은 핸들이 열린 대상, 즉 데이터베이스나 항목 같은 계층 구조 수준을 나타냅니다.|  
|file_object_type_desc|nvarchar(120)|"UNDEFINED",<br />"SERVER_ROOT",<br />"DATABASE_ROOT",<br />"TABLE_ROOT",<br />"TABLE_ITEM"|  
|correlation_process_id|varbinary(8)|요청을 처음 시작한 프로세스의 고유 식별자를 포함합니다.|  
|correlation_thread_id|varbinary(8)|요청을 처음 시작한 스레드의 고유 식별자를 포함합니다.|  
|file_context|varbinary(8)|이 핸들에서 사용하는 파일 개체에 대한 포인터입니다.|  
|state|int|핸들의 현재 상태입니다. ACTIVE, CLOSED 또는 KILLED일 수 있습니다.|  
|state_desc|nvarchar(120)|"ACTIVE",<br />"닫힘",<br />사살|  
|current_workitem_type|int|이 핸들이 현재 처리되고 있는 상태입니다.|  
|current_workitem_type_desc|nvarchar(120)|"NoSetWorkItemType",<br />"FFtPreCreateWorkitem",<br />"FFtGetPhysicalFileNameWorkitem",<br />"FFtPostCreateWorkitem",<br />"FFtPreCleanupWorkitem",<br />"FFtPostCleanupWorkitem",<br />"FFtPreCloseWorkitem",<br />"FFtQueryDirectoryWorkItem",<br />"FFtQueryInfoWorkItem",<br />"FFtQueryVolumeInfoWorkItem",<br />"FFtSetInfoWorkitem",<br />"FFtWriteCompletionWorkitem"|  
|fcb_id|bigint|FileTable 파일 제어 블록 ID입니다.|  
|item_id|varbinary (892)|파일 또는 디렉터리의 항목 ID입니다. 서버 루트 핸들의 경우 null일 수 있습니다.|  
|is_directory|bit|핸들이 디렉터리인지를 나타냅니다.|  
|item_name|nvarchar(512)|항목의 이름입니다.|  
|opened_file_name|nvarchar(512)|원래 요청된 열기 경로입니다.|  
|database_directory_name|nvarchar(512)|데이터베이스 디렉터리 이름을 나타내는 opened_file_name의 부분입니다.|  
|table_directory_name|nvarchar(512)|테이블 디렉터리 이름을 나타내는 opened_file_name의 부분입니다.|  
|remaining_file_name|nvarchar(512)|나머지 디렉터리 이름을 나타내는 opened_file_name의 부분입니다.|  
|open_time|Datetime|핸들이 열린 시간입니다.|  
|flags|int|ShareFlagsUpdatedToFcb = 0x1,<br />DeleteOnClose = 0x2,<br />NewFile = 0x4,<br />PostCreateDoneForNewFile = 0x8,<br />StreamFileOverwritten = 0x10,<br />RequestCancelled = 0x20,<br />NewFileCreationRolledBack = 0x40|  
|login_id|int|핸들을 연 보안 주체의 ID입니다.|  
|login_name|nvarchar(512)|핸들을 연 보안 주체의 이름입니다.|  
|login_sid|varbinary(85)|핸들을 연 보안 주체의 SID입니다.|  
|read_access|bit|읽기 액세스를 위해 열렸습니다.|  
|write_access|bit|쓰기 액세스를 위해 열렸습니다.|  
|delete_access|bit|삭제 액세스를 위해 열렸습니다.|  
|share_read|bit|share_read가 허용되는 상태로 열렸습니다.|  
|share_write|bit|share_write가 허용되는 상태로 열렸습니다.|  
|share_delete|bit|share_delete가 허용되는 상태로 열렸습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [FileTable 관리](../../relational-databases/blob/manage-filetables.md)  
  
  
