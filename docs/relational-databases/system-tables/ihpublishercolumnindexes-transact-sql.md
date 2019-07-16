---
title: IHpublishercolumnindexes (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumnindexes
- IHpublishercolumnindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnindexes system table
ms.assetid: 95b95a1d-b502-4838-825f-82a456487e25
author: stevestein
ms.author: sstein
ms.openlocfilehash: f6dfe2075f983d59b0ef4edecf242a5faadc5821
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990279"
---
# <a name="ihpublishercolumnindexes-transact-sql"></a>IHpublishercolumnindexes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishercolumnindexes** 시스템 테이블에 있는 SQL Server 이외 게시 열을 매핑하는 [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) 시스템 테이블의 인덱스에는 [IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md)시스템 테이블입니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|열을 식별 [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) 관련된 인덱스를 포함 합니다.|  
|**publisherindex_id**|**int**|인덱스를 식별 합니다 [IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md) 열에 연결 된 테이블입니다.|  
|**indid**|**int**|게시된 테이블에서 열의 위치를 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
