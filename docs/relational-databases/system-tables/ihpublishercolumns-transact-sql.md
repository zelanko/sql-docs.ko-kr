---
title: IHpublishercolumns (Transact-sql) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67990263"
---
# <a name="ihpublishercolumns-transact-sql"></a>IHpublishercolumns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishercolumns** 시스템 테이블은 게시자에 저장 된 메타 데이터를 나타냅니다. 이 테이블은 현재 배포자를 사용하여 SQL Server 이외 게시자에서 복제된 각 열당 한 개의 행을 포함합니다. **IHpublishercolumns** 의 데이터 형식 정보는 데이터가 게시 되는 비 SQL Server DBMS (데이터베이스 관리 시스템)에만 적용 됩니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|게시된 열을 식별합니다.|  
|**table_id**|**int**|열이 속한 [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) 에서 원본 테이블을 식별 합니다.|  
|**publisher_id**|**smallint**|열이 게시되는 SQL Server 이외 게시자를 식별합니다.|  
|**name**|**sysname**|게시된 열의 이름입니다.|  
|**column_ordinal**|**int**|열을 순서로 식별합니다.|  
|**type**|**varchar (255)**|게시자에서 원본 열의 열 데이터 형식입니다.|  
|**길이**|**bigint**|게시자에서 원본 열의 길이입니다.|  
|**prec**|**int**|게시자에서 원본 열의 전체 자릿수입니다.|  
|**배율을**|**int**|게시자에서 원본 열의 소수 자릿수입니다.|  
|**isnullable**|**bit**|열이 NULL 값을 허용 하는지 여부를 나타냅니다. **1** 은 null 값이 허용 됨을 의미 합니다.|  
|**iscaptured**|**bit**|열에 트리거가 있는지 여부를 나타냅니다. 열이 아티클에 게시되지 않더라도 트리거가 있을 수 있습니다. 값이 **1** 이면 트리거가 열에 존재 하는 것입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sysarticlecolumns &#40;시스템 뷰&#41; &#40;Transact-sql&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
