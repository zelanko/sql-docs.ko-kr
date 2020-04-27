---
title: MSdistributor (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistributor
- MSdistributor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistributor system table
ms.assetid: 981e9903-0b4b-4508-ac6d-2ee4c813a3d0
author: stevestein
ms.author: sstein
ms.openlocfilehash: aa171f268fc6e39d584461dd0c2a4d69345706a4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67907378"
---
# <a name="msdistributor-transact-sql"></a>MSdistributor(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Msdistributor** 테이블에는 배포자 속성이 포함 되어 있습니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**property**|**sysname**|속성의 이름입니다.|  
|**value**|**nvarchar (3000)**|속성의 값입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
