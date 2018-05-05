---
title: sys.dm_filestream_file_io_requests (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_filestream_file_io_requests
- dm_filestream_file_io_requests
- sys.dm_filestream_file_io_requests_TSQL
- dm_filestream_file_io_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_file_io_requests catalog view
ms.assetid: d41e39a5-14d5-4f3d-a2e3-a822b454c1ed
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9ff2a5c22f48b767556e45b2f4b7a00c606d136c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmfilestreamfileiorequests-transact-sql"></a>sys.dm_filestream_file_io_requests(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 시간에 NSO(네임스페이스 소유자)에 의해 처리 중인 I/O 요청의 목록을 표시합니다.  
  
|열|형식|Description|  
|------------|----------|-----------------|  
|**request_context_address**|**varbinary(8)**|드라이버의 I/O 요청이 포함된 NSO 메모리 블록의 내부 주소를 표시합니다. Null을 허용하지 않습니다.|  
|**current_spid**|**smallint**|현재 SQL Server 연결에 대한 SPID(시스템 프로세스 ID)를 표시합니다. Null을 허용하지 않습니다.|  
|**request_type**|**nvarchar(60)**|IRP(I/O 요청 패킷) 유형을 표시합니다. 가능한 요청 유형은 REQ_PRE_CREATE, REQ_POST_CREATE, REQ_RESOLVE_VOLUME, REQ_GET_VOLUME_INFO, REQ_GET_LOGICAL_NAME, REQ_GET_PHYSICAL_NAME, REQ_PRE_CLEANUP, REQ_POST_CLEANUP, REQ_CLOSE, REQ_FSCTL, REQ_QUERY_INFO, REQ_SET_INFO, REQ_ENUM_DIRECTORY, REQ_QUERY_SECURITY 및 REQ_SET_SECURITY입니다. Null을 허용하지 않습니다.|  
|**request_state**|**nvarchar(60)**|NSO에 있는 I/O 요청의 상태를 표시합니다. 가능한 값은 REQ_STATE_RECEIVED, REQ_STATE_INITIALIZED, REQ_STATE_ENQUEUED, REQ_STATE_PROCESSING, REQ_STATE_FORMATTING_RESPONSE, REQ_STATE_SENDING_RESPONSE, REQ_STATE_COMPLETING 및 REQ_STATE_COMPLETED입니다. Null을 허용하지 않습니다.|  
|**request_id**|**int**|드라이버가 이 요청에 할당한 고유한 요청 ID를 표시합니다. Null을 허용하지 않습니다.|  
|**irp_id**|**int**|고유한 IRP ID를 표시합니다. 지정된 IRP와 관련된 모든 I/O 요청을 식별하는 데 유용합니다. Null을 허용하지 않습니다.|  
|**handle_id**|**int**|네임스페이스 핸들 ID를 나타냅니다. NSO 관련 ID이며 인스턴스에서 고유합니다. Null을 허용하지 않습니다.|  
|**client_thread_id**|**varbinary(8)**|요청을 시작한 클라이언트 응용 프로그램의 스레드 ID를 표시합니다.<br /><br /> **\*\* 경고 \* \***  이 클라이언트 응용 프로그램은 SQL Server와 동일한 컴퓨터에서 실행 되는 경우에 의미가 있습니다. 클라이언트 응용 프로그램은 원격으로 실행 하는 경우는 **client_thread_id** 원격 클라이언트 대신 작동 하는 일부 시스템 프로세스의 스레드 ID를 표시 합니다.<br /><br /> Null을 허용합니다.|  
|**client_process_id**|**varbinary(8)**|클라이언트 응용 프로그램이 SQL Server와 동일한 컴퓨터에서 실행되는 경우 해당 클라이언트 응용 프로그램의 프로세스 ID를 표시합니다. 원격 클라이언트일 경우 해당 클라이언트 대신 작동하는 시스템 프로세스의 ID를 표시합니다. Null을 허용합니다.|  
|**handle_context_address**|**varbinary(8)**|클라이언트의 핸들과 연결된 내부 NSO 구조의 주소를 표시합니다. Null을 허용합니다.|  
|**filestream_transaction_id**|**varbinary(128)**|지정된 핸들과 연결된 트랜잭션의 ID 및 이 핸들과 연결된 모든 요청을 표시합니다. 반환 된 값은 고 **get_filestream_transaction_context** 함수입니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Filestream 및 FileTable 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)  
  
  
