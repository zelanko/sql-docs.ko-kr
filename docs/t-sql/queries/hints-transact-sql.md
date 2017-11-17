---
title: "힌트 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- query optimizer [SQL Server], hints
- hints [SQL Server], about hints
- SELECT statement [SQL Server], hints
- hints [SQL Server]
- INSERT statement [SQL Server], hints
- UPDATE statement [SQL Server], hints
- DELETE statement [SQL Server], hints
ms.assetid: 99412475-b0df-4264-9938-33a0b302b41a
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6d2d8b50a38299162677b1f7d5bbff501fba9881
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="hints-transact-sql"></a>힌트(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  힌트는 SELECT, INSERT, UPDATE 또는 DELETE 문에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 프로세서에 적용하기 위해 지정한 옵션 또는 전략입니다. 힌트는 쿼리 최적화 프로그램이 쿼리에 대해 선택한 실행 계획보다 우선합니다.  
  
> [!CAUTION]  
>  때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 일반적으로 쿼리에 대해 최적의 실행 계획을 선택 하는 것이 좋습니다, \<알아서 >, \<쿼리 힌트 >, 및 \<테이블 힌트 > 숙련 된 여 최후의 수단 으로만 사용할 수 개발자 및 데이터베이스 관리자입니다.
  
 이 섹션에서는 다음 힌트에 대해 설명합니다.  
  
-   [조인 힌트](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [테이블 힌트](../../t-sql/queries/hints-transact-sql-table.md)  
  
  

