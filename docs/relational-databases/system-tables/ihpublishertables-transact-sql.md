---
title: IHpublishertables (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 9a75e78c8423b925ca2dfc617cbbae7e4bdcc11d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67990161"
---
# <a name="ihpublishertables-transact-sql"></a>IHpublishertables(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishertables** 시스템 테이블은 게시자에 저장 된 메타 데이터를 나타냅니다. 이 테이블은 현재 배포자를 사용하여 SQL Server 이외 게시자에서 게시되는 각 원본 테이블당 한 개의 행을 포함합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|게시된 테이블을 식별합니다.|  
|**publisher_id**|**smallint**|테이블이 게시되는 SQL Server 이외 게시자를 식별합니다.|  
|**name**|**sysname**|게시된 테이블의 이름입니다.|  
|**소유자도**|**sysname**|테이블 소유자입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
