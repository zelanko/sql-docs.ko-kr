---
title: IHpublishers (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- IHpublishers
- IHpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishers system table
ms.assetid: 77007246-f10b-4b87-8edf-7afc3c2096af
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d57aa3f5245326b8e036ae061e32297f2493a78
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="ihpublishers-transact-sql"></a>IHpublishers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishers** 시스템 테이블에 대 한 각 SQL Server 이외 게시자는 현재 배포자를 사용 하 여 행이 하나씩 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|-SQL Server 이외 게시자를 식별합니다.|  
|**공급 업체**|**sysname**|SQL Server 이외 데이터베이스 공급 업체의 이름입니다.|  
|**publisher_guid**|**uniqueidentifier**|SQL Server 이외 게시자를 식별하는 GUID입니다.|  
|**flush_request_time**|**datetime**|로그 판독기 에이전트가 해당 메타데이터 캐시를 업데이트해야 하는 아티클 메타데이터의 마지막 변경 날짜 및 시간을 표시합니다.|  
|**version**|**sysname**|버전의-SQL Server 이외 게시자를 지정 하는 텍스트 문자열입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_adddistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)  
  
  
