---
title: sys. dm_filestream_file_io_handles (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_filestream_file_io_handles
- sys.dm_filestream_file_io_handles
- dm_filestream_file_io_handles_TSQL
- sys.dm_filestream_file_io_handles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_file_io_handle catalog view
ms.assetid: e59632f4-3292-419f-9217-ca375749f1a5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 56e498fb942b87f187ae53a04ec1b240b71d2c96
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898878"
---
# <a name="sysdm_filestream_file_io_handles-transact-sql"></a>sys.dm_filestream_file_io_handles(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  NSO(네임스페이스 소유자)가 인식하는 파일 핸들을 표시합니다. **Opensqlfilestream** 을 사용 하 여 클라이언트에서 가져온 Filestream 핸들이이 뷰에 표시 됩니다.  
  
|Column|형식|설명|  
|------------|----------|-----------------|  
|**handle_context_address**|**varbinary(8)**|클라이언트의 핸들과 연결 된 내부 n 번째 구조체의 주소를 표시 합니다. Null을 허용합니다.|  
|**creation_request_id**|**int**|이 핸들을 만드는 데 사용된 REQ_PRE_CREATE I/O 요청의 필드를 표시합니다. Null을 허용하지 않습니다.|  
|**creation_irp_id**|**int**|이 핸들을 만드는 데 사용된 REQ_PRE_CREATE I/O 요청의 필드를 표시합니다. Null을 허용하지 않습니다.|  
|**handle_id**|**int**|드라이버가 할당한 이 핸들의 고유한 ID를 표시합니다. Null을 허용하지 않습니다.|  
|**creation_client_thread_id**|**varbinary(8)**|이 핸들을 만드는 데 사용된 REQ_PRE_CREATE I/O 요청의 필드를 표시합니다. Null을 허용합니다.|  
|**creation_client_process_id**|**varbinary(8)**|이 핸들을 만드는 데 사용된 REQ_PRE_CREATE I/O 요청의 필드를 표시합니다. Null을 허용합니다.|  
|**filestream_transaction_id**|**varbinary(128)**|지정된 핸들과 연결된 트랜잭션의 ID를 표시합니다. **Get_filestream_transaction_context** 함수에서 반환 하는 값입니다. 이 필드를 사용 하 여 **dm_filestream_file_io_requests** 뷰에 조인 합니다. Null을 허용합니다.|  
|**access_type**|**nvarchar(60)**|Null을 허용하지 않습니다.|  
|**logical_path**|**nvarchar(256)**|이 핸들이 연 파일의 논리적 경로 이름을 표시합니다. 에서 반환 하는 것과 동일한 경로 이름입니다 **. ** **Varbinary**(**Max**) filestream의 PathName 메서드입니다. Null을 허용합니다.|  
|**physical_path**|**nvarchar(256)**|파일의 실제 NTFS 경로 이름을 표시합니다. 에서 반환 하는 것과 동일한 경로 이름입니다 **. ** **Varbinary**(**max**) filestream의 실제 경로 이름 메서드 추적 플래그 5556에 의해 설정됩니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;Filestream 및 FileTable 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)  
  
  
