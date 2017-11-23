---
title: systranschemas (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- systranschemas
- systranschemas_TSQL
dev_langs: TSQL
helpviewer_keywords: systranschemas system table
ms.assetid: 864c3966-cb61-4f2b-8939-ccda112de853
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f5f5c9502b9116bc60797c537edb27fdf79d3080
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="systranschemas-transact-sql"></a>systranschemas(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **systranschemas** 트랜잭션 및 스냅숏 게시에 게시 된 아티클의 스키마 변경 내용 추적 테이블을 사용 합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**tabid**|**int**|스키마가 변경된 테이블 아티클을 식별합니다.|  
|**startlsn**|**binary**|스키마 변경 시작 부분의 LSN 값입니다.|  
|**endlsn**|**binary**|스키마 변경 끝 부분의 LSN 값입니다.|  
|**typeid**|**int**|스키마 변경의 유형입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
