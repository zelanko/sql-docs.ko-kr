---
title: "쿼리 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 5ff02a32-e8d3-479c-ae8b-07581e41f5f8
caps.latest.revision: "8"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: dab62a8aae5a986bc54928208a258cab48d16247
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="queries"></a>쿼리
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터 조작 언어 (DML)은 검색 한 데이터로 작업 하는 데 사용 하는 어휘 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 SQL 데이터베이스입니다. SQL 데이터 웨어하우스 및 PDW (자세한 내용은 각 개별 문을 검토) 가장 에서도 작동 합니다. 이러한 DML 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 데이터를 추가, 수정, 쿼리 또는 제거할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 DML 문을 나열합니다.  
  
|||  
|-|-|  
|[BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)|[SELECT &#40;TRANSACT-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|  
|[DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|[UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)|  
|[INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)|[Updatetext&#40; Transact SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)|  
|[MERGE&#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)|[WRITETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)|  
|[Readtext&#40; Transact SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)||  
  
 다음 표에서는 여러 DML 문 또는 절에 사용되는 절을 나열합니다.  
  
|절|다음과 같은 문에서 사용할 수 있습니다.|  
|------------|-------------------------------------|  
|[FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)|DELETE, SELECT, UPDATE|  
|[힌트 &#40; Transact SQL &#41;](../../t-sql/queries/hints-transact-sql.md)|DELETE, INSERT, SELECT, UPDATE|  
|[OPTION 절 &#40; Transact SQL &#41;](../../t-sql/queries/option-clause-transact-sql.md)|DELETE, SELECT, UPDATE|  
|[OUTPUT 절&#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)|DELETE, INSERT, MERGE, UPDATE|  
|[검색 조건 &#40; Transact SQL &#41;](../../t-sql/queries/search-condition-transact-sql.md)|DELETE, MERGE, SELECT, UPDATE|  
|[테이블 값 생성자 &#40; Transact SQL &#41;](../../t-sql/queries/table-value-constructor-transact-sql.md)|FROM, INSERT, MERGE|  
|[Top&#40; Transact SQL &#41;](../../t-sql/queries/top-transact-sql.md)|DELETE, INSERT, MERGE, SELECT, UPDATE|  
|[여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)|DELETE, SELECT, UPDATE, 일치|  
|[Common_table_expression &AMP;#40; Transact SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)|DELETE, INSERT, MERGE, SELECT, UPDATE|  
  
  
