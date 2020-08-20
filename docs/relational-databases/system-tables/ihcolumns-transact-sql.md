---
description: IHcolumns(Transact-SQL)
title: IHcolumns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHcolumns_TSQL
- IHcolumns
dev_langs:
- TSQL
helpviewer_keywords:
- IHcolumns system table
ms.assetid: 5bb027e5-5279-487b-9c33-5f402987253c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0bc33419b8bb710b223150e1880002ff49681870
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454705"
---
# <a name="ihcolumns-transact-sql"></a>IHcolumns(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **IHcolumns** 시스템 테이블에는 게시 된 각 열에 대 한 행이 하나씩 포함 되어 있습니다. 이 테이블은 SQL Server 이외 게시자에서 열 데이터 형식이 어떻게 표현하여 게시하는지를 정의하며 근본적으로 SQL Server 이외 DBMS(데이터베이스 관리 시스템)과 SQL Server 간에 데이터 형식을 매핑하는 역할을 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|게시된 열을 식별합니다.|  
|**publishercolumn_id**|**int**|게시 된 열을 [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) 시스템 테이블에 저장 된 열 메타 데이터와 연결 합니다.|  
|**name**|**sysname**|열 이름을 지정합니다.|  
|**article_id**|**int**|열이 속한 아티클을 식별합니다.|  
|**column_ordinal**|**int**|열을 순서로 식별합니다.|  
|**mapped_type**|**tinyint**|구독자에 있는 대상 열의 열 데이터 형식입니다.|  
|**mapped_length**|**bigint**|구독자에 있는 열의 길이입니다.|  
|**mapped_prec**|**int**|구독자에 있는 열의 전체 자릿수입니다.|  
|**mapped_scale**|**int**|구독자에 있는 열의 소수 자릿수입니다.|  
|**mapped_nullable**|**bit**|구독자의 열이 NULL 값을 허용 하는지 여부를 나타냅니다. 여기서 **1** 은 null 값이 허용 됨을 의미 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰 ](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Transact-sql&#41;sp_articlecolumn &#40;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;시스템 뷰&#41; &#40;Transact-sql&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
