---
title: IHpublishercolumnconstraints (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumnconstraints
- IHpublishercolumnconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnconstraints system table
ms.assetid: d7a41da6-e067-430a-8da2-3f6745b8a4f3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 58ef9c5e68e7d209262ebf43891ba5c1bcc4174f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67990288"
---
# <a name="ihpublishercolumnconstraints-transact-sql"></a>IHpublishercolumnconstraints(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishercolumnconstraints** 시스템 테이블은 [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) 시스템 테이블에 있는 SQL Server 되지 않은 게시의 열을 [IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md) 시스템 테이블의 제약 조건에 매핑합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|연결 된 제약 조건을 사용 하 여 [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) 에서 열을 식별 합니다.|  
|**publisherconstraint_id**|**int**|열과 연결 된 [IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md) 에서 제약 조건을 식별 합니다.|  
|**indid**|**int**|게시된 테이블에서 열의 위치를 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
