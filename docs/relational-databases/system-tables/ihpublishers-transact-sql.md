---
title: IHpublishers (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishers
- IHpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishers system table
ms.assetid: 77007246-f10b-4b87-8edf-7afc3c2096af
author: stevestein
ms.author: sstein
ms.openlocfilehash: 92f0c507b15e5a582fbcc1a12b1bccd77d08f7de
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67990164"
---
# <a name="ihpublishers-transact-sql"></a>IHpublishers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishers** 시스템 테이블에는 현재 배포자를 사용 하 여 SQL Server 없는 각 게시자에 대 한 행이 하나씩 포함 되어 있습니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|SQL Server 이외 게시자를 식별합니다.|  
|**공급업체**|**sysname**|SQL Server 이외 데이터베이스 공급업체의 이름입니다.|  
|**publisher_guid**|**uniqueidentifier**|SQL Server 이외 게시자를 식별하는 GUID입니다.|  
|**flush_request_time**|**datetime**|로그 판독기 에이전트가 해당 메타데이터 캐시를 업데이트해야 하는 아티클 메타데이터의 마지막 변경 날짜 및 시간을 표시합니다.|  
|**version**|**sysname**|SQL Server 이외 게시자의 버전을 나타내는 텍스트 문자열입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Transact-sql&#41;sp_adddistpublisher &#40;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [Transact-sql&#41;sp_changedistpublisher &#40;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_helpdistpublisher&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)  
  
  
