---
title: IHpublishercolumns (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumns
- IHpublishercolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumns system table
ms.assetid: a5347750-224c-40d9-ae12-57e7213b7db9
author: stevestein
ms.author: sstein
ms.openlocfilehash: a5e2f64294652586a87fcd25fda3c29517dc295d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990263"
---
# <a name="ihpublishercolumns-transact-sql"></a>IHpublishercolumns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **IHpublishercolumns** 시스템 테이블은 게시자에 저장 된 메타 데이터를 나타냅니다. 이 테이블에서 SQL Server 이외 게시자는 현재 배포자를 사용 하 여 복제 된 각 열당 한 개의 행을 포함 합니다. 데이터 형식에 대 한 정보 **IHpublishercolumns** 데이터를 게시 하는 SQL Server 이외 데이터베이스 관리 시스템 (DBMS)에 따라 다릅니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|게시된 열을 식별합니다.|  
|**table_id**|**int**|원본 테이블을 식별 [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) 열이 속한 합니다.|  
|**publisher_id**|**smallint**|비-SQL Server 게시자 열이 게시를 식별 합니다.|  
|**name**|**sysname**|게시된 열의 이름입니다.|  
|**column_ordinal**|**int**|열을 순서로 식별합니다.|  
|**type**|**varchar(255)**|게시자에서 원본 열의 열 데이터 형식입니다.|  
|**length**|**bigint**|게시자에서 원본 열의 길이입니다.|  
|**prec**|**int**|게시자에서 원본 열의 전체 자릿수입니다.|  
|**scale**|**int**|게시자에서 원본 열의 소수 자릿수입니다.|  
|**isnullable**|**bit**|열에 NULL 값을 허용 하는지 여부를 나타냅니다. 여기서 **1** NULL 값이 허용 되는 것을 의미 합니다.|  
|**iscaptured**|**bit**|열에 트리거가 있는지 여부를 나타냅니다. 열이 아티클에 게시되지 않더라도 트리거가 있을 수 있습니다. 값이 **1** 열에 트리거가 있음을 의미 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sysarticlecolumns &#40;시스템 뷰&#41; &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
