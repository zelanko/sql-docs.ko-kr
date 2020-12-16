---
description: 쿼리
title: 쿼리 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5ff02a32-e8d3-479c-ae8b-07581e41f5f8
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e79bf08e7cbd4364d473a96032e226758b724134
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460926"
---
# <a name="queries"></a>쿼리

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  DML(데이터 조작 언어)은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 SQL Database에서 데이터를 검색하고 데이터로 작업하는 데 사용하는 어휘입니다. 대부분 [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서도 작동합니다(자세한 내용은 개별 명령문을 검토). 이러한 DML 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 데이터를 추가, 수정, 쿼리 또는 제거할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 DML 문을 나열합니다.  

:::row:::
    :::column:::
        [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)
    :::column-end:::
    :::column:::
        [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)
    :::column-end:::
    :::column:::
        [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)
    :::column-end:::
    :::column:::
        [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [MERGE&#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)
    :::column-end:::
    :::column:::
        [WRITETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [READTEXT&#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

&nbsp;

 다음 표에서는 여러 DML 문 또는 절에 사용되는 절을 나열합니다.  
  
|절|다음과 같은 문에서 사용할 수 있습니다.|  
|------------|-------------------------------------|  
|[FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)|DELETE, SELECT, UPDATE|  
|[힌트 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)|DELETE, INSERT, SELECT, UPDATE|  
|[OPTION 절&#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md)|DELETE, SELECT, UPDATE|  
|[OUTPUT 절&#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)|DELETE, INSERT, MERGE, UPDATE|  
|[검색 조건&#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)|DELETE, MERGE, SELECT, UPDATE|  
|[테이블 값 생성자 &#40;Transact-SQL&#41;](../../t-sql/queries/table-value-constructor-transact-sql.md)|FROM, INSERT, MERGE|  
|[TOP&#40;Transact SQL&#41;](../../t-sql/queries/top-transact-sql.md)|DELETE, INSERT, MERGE, SELECT, UPDATE|  
|[WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)|DELETE, SELECT, UPDATE, MATCH|  
|[WITH common_table_expression&#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)|DELETE, INSERT, MERGE, SELECT, UPDATE|  
| &nbsp; | &nbsp; |
