---
title: IHpublishertables (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishertables
- IHpublishertables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishertables system table
ms.assetid: 7d16ac39-633a-4fe2-8f22-1d9afc191ee9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d556a80e018a9d3707aa03de7fdefe8c45bcb611
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62704156"
---
# <a name="ihpublishertables-transact-sql"></a>IHpublishertables(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **IHpublishertables** 시스템 테이블은 게시자에 저장 된 메타 데이터를 나타냅니다. 이 테이블에서-SQL Server 이외 게시자는 현재 배포자를 사용 하 여 게시 된 각 원본 테이블당 한 개의 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|게시된 테이블을 식별합니다.|  
|**publisher_id**|**smallint**|비-SQL Server 게시자 테이블은 게시를 식별 합니다.|  
|**name**|**sysname**|게시된 테이블의 이름입니다.|  
|**owner**|**sysname**|테이블 소유자입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
