---
description: IHconstrainttypes(Transact-SQL)
title: IHconstrainttypes (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHconstrainttypes_TSQL
- IHconstrainttypes
dev_langs:
- TSQL
helpviewer_keywords:
- IHconstrainttypes system table
ms.assetid: 955d6fa9-0b31-4335-a3cd-e4c4d90ad308
author: markingmyname
ms.author: maghan
ms.openlocfilehash: eaa7ef45e9e6b9ae71eceee558af116fe3314449
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540412"
---
# <a name="ihconstrainttypes-transact-sql"></a>IHconstrainttypes(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **IHconstrainttypes** 시스템 테이블에는 SQL Server 이외 게시자에 대해 지원 되는 비 SQL Server 제약 조건의 각 유형에 대 한 행이 하나씩 포함 되어 있습니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**type**|**nvarchar(255)**|지원되는 SQL Server 이외 제약 조건 유형의 이름입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
