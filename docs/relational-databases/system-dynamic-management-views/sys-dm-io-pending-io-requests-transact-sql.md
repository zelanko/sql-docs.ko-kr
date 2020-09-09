---
description: sys.dm_io_pending_io_requests(Transact-SQL)
title: sys. dm_io_pending_io_requests (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_io_pending_io_requests
- dm_io_pending_io_requests
- dm_io_pending_io_requests_TSQL
- sys.dm_io_pending_io_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_pending_io_requests dynamic management view
ms.assetid: d1fb46dd-5c74-4c04-9ecf-8934b1bedb5b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7e61b234942d6e486886ae8238db8b9c68e65385
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89532574"
---
# <a name="sysdm_io_pending_io_requests-transact-sql"></a>sys.dm_io_pending_io_requests(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 보류 중인 각 I/O 요청에 대해 행을 반환합니다.  
  
> [!NOTE]  
>  또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이름 **sys. dm_pdw_nodes_io_pending_io_requests**을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**io_completion_request_address**|**varbinary(8)**|IO 요청의 메모리 주소입니다. Null을 허용하지 않습니다.|  
|**io_type**|**nvarchar(60)**|보류 중인 I/O 요청의 유형입니다. Null을 허용하지 않습니다.|  
|**io_pending_ms_ticks**|**bigint**|내부적으로만 사용됩니다. Null을 허용하지 않습니다.| 
|**io_pending**|**int**|I/O 요청이 보류 중인지 또는 Windows에서 완료되었는지 여부를 나타냅니다. Windows에서는 I/O 요청을 완료했지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 I/O 요청을 처리하고 목록에서 제거하기 위한 컨텍스트 전환을 아직 수행하지 못한 경우 I/O 요청은 계속 보류 상태일 수 있습니다. Null을 허용하지 않습니다.|  
|**io_completion_routine_address**|**varbinary(8)**|I/O 요청이 완료될 때 호출할 내부 함수입니다. Null을 허용합니다.|  
|**io_user_data_address**|**varbinary(8)**|내부적으로만 사용됩니다. Null을 허용합니다.|  
|**scheduler_address**|**varbinary(8)**|이 I/O 요청을 실행한 스케줄러입니다. I/O 요청이 스케줄러의 보류 중인 I/O 목록에 나타납니다. 자세한 내용은 [dm_os_schedulers &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)을 참조 하십시오. Null을 허용하지 않습니다.|  
|**io_handle**|**varbinary(8)**|I/O 요청에 사용되는 파일의 파일 핸들입니다. Null을 허용합니다.|  
|**io_offset**|**bigint**|I/O 요청의 오프셋입니다. Null을 허용하지 않습니다.|  
|**io_handle_path**|**nvarchar(256)**| I/o 요청에 사용 되는 파일의 경로입니다. Null을 허용합니다.|
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수 ](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


