---
title: sys.database_mirroring_witnesses (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring_witnesses
- sys.database_mirroring_witnesses_TSQL
- database_mirroring_witnesses
- database_mirroring_witnesses_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], catalog views
- sys.database_mirroring_witnesses catalog view
- witness [SQL Server], sys.database_mirroring_witnesses catalog view
ms.assetid: 0dd5b794-733b-4a3c-b5a4-62f9f1f0f22d
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ce23f7d9f763bf08842a1f121c881fb5fbdcee0
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="database-mirroring-witness-catalog-views---sysdatabasemirroringwitnesses"></a>데이터베이스 미러링 모니터 카탈로그 뷰-sys.database_mirroring_witnesses
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  서버가 데이터베이스 미러링 파트너 역할을 하는 각 모니터 역할에 대한 행을 포함합니다. 
  
  데이터베이스 미러링 세션에서 자동 장애 조치(Failover)를 수행하려면 미러링 모니터 서버가 필요합니다. 이상적으로 미러링 모니터 서버는 주 서버 및 미러 서버와 다른 컴퓨터에 있어야 합니다. 미러링 모니터 서버는 데이터베이스 역할을 하지 않습니다. 대신 주 서버와 미러 서버의 상태를 모니터링합니다. 주 서버에서 오류가 발생하면 미러링 모니터 서버는 자동으로 장애 조치를 시작할 수 있습니다. 
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|데이터베이스 미러링 세션에 있는 두 개의 데이터베이스 사본의 이름입니다.|  
|**principal_server_name**|**sysname**|현재 주 데이터베이스 역할을 하는 데이터베이스 사본을 가진 파트너 서버의 이름입니다.|  
|**mirror_server_name**|**sysname**|현재 미러 데이터베이스 역할을 하는 데이터베이스 사본을 가진 파트너 서버의 이름입니다.|  
|**safety_level**|**tinyint**|미러 데이터베이스 업데이트를 위한 트랜잭션 보안 설정입니다.<br /><br /> 0 = 알 수 없는 상태<br /><br /> 1 = 해제(비동기)<br /><br /> 2 = 완전(동기)<br /><br /> 자동 장애 조치(Failover)에 미러링 모니터를 사용하려면 완전 트랜잭션 보안(기본값)이 필요합니다.|  
|**safety_level_desc**|**nvarchar(60)**|미러 데이터베이스 업데이트의 보안 설정에 대한 설명입니다.<br /><br /> UNKNOWN<br /><br /> OFF<br /><br /> FULL|  
|**safety_sequence_number**|**int**|업데이트에 대 한 변경에 대 한 시퀀스 번호 **safety_level**합니다.|  
|**role_sequence_number**|**int**|미러링 파트너의 주/미러 역할 변경에 따라 시퀀스 번호를 업데이트합니다.|  
|**mirroring_guid**|**uniqueidentifier**|미러링 파트너 관계의 식별자입니다.|  
|**family_guid**|**uniqueidentifier**|데이터베이스 백업 패밀리의 식별자입니다. 일치하는 복원 상태를 찾는 데 사용됩니다.|  
|**is_suspended**|**bit**|데이터베이스 미러링이 일시 중지됩니다.|  
|**is_suspended_sequence_number**|**int**|시퀀스 번호 설정에 대 한 **is_suspended**합니다.|  
|**partner_sync_state**|**tinyint**|미러링 세션의 동기화 상태<br /><br /> 5 = 파트너가 동기화 합니다. 장애 조치를 수행할 수 있습니다. 장애 조치 참조에 대 한 요구 사항에 대 한 내용은 [세션 중 역할 전환는 데이터베이스 미러링 &#40; SQL Server &#41; ](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md).<br /><br /> 6 = 파트너가 동기화 되지 않습니다. 지금은 장애 조치를 수행할 수 없습니다.|  
|**partner_sync_state_desc**|**nvarchar(60)**|미러링 세션의 동기화 상태 설명<br /><br /> SYNCHRONIZED<br /><br /> UNSYNCHRONIZED|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 미러링 모니터 서버](../../database-engine/database-mirroring/database-mirroring-witness.md)   
 [sys.database_mirroring &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [sys.database_mirroring_endpoints&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
