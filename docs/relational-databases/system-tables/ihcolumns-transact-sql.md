---
title: IHcolumns (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- IHcolumns_TSQL
- IHcolumns
dev_langs: TSQL
helpviewer_keywords: IHcolumns system table
ms.assetid: 5bb027e5-5279-487b-9c33-5f402987253c
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 857380d30397d02b2fe1ba9adfd11ca9382b9eee
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="ihcolumns-transact-sql"></a>IHcolumns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHcolumns** 시스템 테이블 게시 된 각 열당 하나의 행을 포함 합니다. 기본적으로 SQL Server 이외 데이터베이스 관리 시스템 (DBMS) 간에 데이터 형식을 매핑할에 게시 될 때 열 데이터 형식에서의 SQL Server 이외 게시자는 표현 하는 방법을 정의 하려면이 테이블은 사용 및 SQL Server. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|게시된 열을 식별합니다.|  
|**publishercolumn_id**|**int**|게시 된 열에 저장 된 열 메타 데이터와 연결 된 [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) 시스템 테이블입니다.|  
|**name**|**sysname**|열 이름을 지정합니다.|  
|**article_id**|**int**|열이 속한 아티클을 식별합니다.|  
|**column_ordinal**|**int**|열을 순서로 식별합니다.|  
|**mapped_type**|**tinyint**|구독자에 있는 대상 열의 열 데이터 형식입니다.|  
|**mapped_length**|**bigint**|구독자에 있는 열의 길이입니다.|  
|**mapped_prec**|**int**|구독자에 있는 열의 전체 자릿수입니다.|  
|**mapped_scale**|**int**|구독자에 있는 열의 소수 자릿수입니다.|  
|**mapped_nullable**|**bit**|구독자에 있는 열의 NULL 값을 허용 하는지 여부를 나타냅니다. 여기서 **1** NULL 값이 허용 되는 것을 의미 합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [복제 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_articlecolumn&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40; 시스템 뷰 &#41; &#40; Transact SQL &#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40; Transact SQL &#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
