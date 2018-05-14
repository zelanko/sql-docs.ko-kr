---
title: 힌트(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a404f015c177fe38985c07470645e9a16e2cb716
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="hints-transact-sql"></a>힌트(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  힌트는 SELECT, INSERT, UPDATE 또는 DELETE 문에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 프로세서에 적용하기 위해 지정한 옵션 또는 전략입니다. 힌트는 쿼리 최적화 프로그램이 쿼리에 대해 선택한 실행 계획보다 우선합니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 일반적으로 쿼리에 대한 최상의 실행 계획을 선택하므로 \<join_hint>, \<query_hint> 및 \<table_hint>는 숙련된 개발자나 데이터베이스 관리자가 최후의 수단으로만 사용하는 것이 좋습니다.
  
 이 섹션에서는 다음 힌트에 대해 설명합니다.  
  
-   [조인 힌트](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [테이블 힌트](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
