---
title: 힌트(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7ee01e23c544ac01ee9fb85e5b59d31b73088987
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731287"
---
# <a name="hints-transact-sql"></a>힌트(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  힌트는 SELECT, INSERT, UPDATE 또는 DELETE 문에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 프로세서에 적용하기 위해 지정한 옵션 또는 전략입니다. 힌트는 쿼리 최적화 프로그램이 쿼리에 대해 선택한 실행 계획보다 우선합니다.  
  
> [!CAUTION]  
>  일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 쿼리에 대해 최상의 실행 계획을 선택하므로 숙련된 개발자 및 데이터베이스 관리자는 마지막 방법으로만 \<join_hint>, \<query_hint>, \<table_hint>를 사용하는 것이 좋습니다.
  
 이 섹션에서는 다음 힌트에 대해 설명합니다.  
  
-   [조인 힌트](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [테이블 힌트](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
