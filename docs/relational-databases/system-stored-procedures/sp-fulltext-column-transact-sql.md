---
description: sp_fulltext_column(Transact-SQL)
title: sp_fulltext_column (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_column_TSQL
- sp_fulltext_column
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_column
ms.assetid: a84cc45d-1b50-44af-85df-2ea033b8a6a9
author: CarlRabeler
ms.author: carlrab
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 544854219f8fbc26a06b80280c6f36f64fe726c6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481247"
---
# <a name="sp_fulltext_column-transact-sql"></a>sp_fulltext_column(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  테이블의 특정 열을 전체 텍스트 인덱싱에 참여시킬지 여부를 지정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [ALTER 전체 인덱스](../../t-sql/statements/alter-fulltext-index-transact-sql.md) 를 사용 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_fulltext_column [ @tabname= ] 'qualified_table_name' ,   
     [ @colname= ] 'column_name' ,   
     [ @action= ] 'action'   
     [ , [ @language= ] 'language_term' ]   
     [ , [ @type_colname= ] 'type_column_name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @tabname = ] 'qualified_table_name'` 는 한 부분 또는 두 부분으로 구성 된 테이블 이름입니다. 테이블은 반드시 현재 데이터베이스에 있어야 합니다. 테이블에 전체 텍스트 인덱스가 있어야 합니다. *qualified_table_name* 은 **nvarchar (517)** 이며 기본값은 없습니다.  
  
`[ @colname = ] 'column_name'`*Qualified_table_name*의 열 이름입니다. 열은 character, **varbinary (max)** 또는 **image** 열 이어야 하며 계산 열이 될 수 없습니다. *column_name* 는 **sysname**이며 기본값은 없습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 **varbinary (max)** 또는 **image** 데이터 형식의 열에 저장 된 텍스트 데이터의 전체 텍스트 인덱스를 만들 수 있습니다. 이미지와 그림은 인덱싱되지 않습니다.  
  
`[ @action = ] 'action'` 수행할 동작입니다. *action* 은 **varchar (20)** 이며 기본값은 없고 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**add**|테이블의 비활성 전체 텍스트 인덱스에 *qualified_table_name* *column_name* 를 추가 합니다. 이 동작으로 전체 텍스트 인덱싱에 열을 사용할 수 있습니다.|  
|**drop**|테이블의 비활성 전체 텍스트 인덱스에서 *qualified_table_name* *column_name* 를 제거 합니다.|  
  
`[ @language = ] 'language_term'` 열에 저장 된 데이터의 언어입니다. 에 포함 된 언어 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Fulltext_languages &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)을 참조 하십시오.  
  
> [!NOTE]  
>  열에 여러 언어 또는 지원되지 않는 언어의 데이터가 있을 때는 중립을 사용하십시오. 기본값은 구성 옵션인 '기본 전체 텍스트 언어'에 의해 지정됩니다.  
  
`[ @type_colname = ] 'type_column_name'`*Column_name*문서 유형을 보유 하는 *qualified_table_name* 의 열 이름입니다. 이 열은 **char**, **nchar**, **varchar**또는 **nvarchar**여야 합니다. *Column_name* 데이터 형식이 **varbinary (max)** 또는 **image**유형인 경우에만 사용 됩니다. *type_column_name* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 전체 텍스트 인덱스가 활성화되었을 경우 진행 중인 채우기가 모두 중지됩니다. 또한 활성화된 전체 텍스트 인덱스가 있는 테이블에 대해 변경 내용 추적을 사용할 수 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 인덱스가 현재 상태인지 확인합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 테이블에서 모든 현재 채우기를 중지하고 기존 인덱스를 삭제한 후 채우기를 새로 시작합니다.  
  
 변경 내용 추적이 진행 중이고 인덱스를 보관하는 동안 전체 텍스트 인덱스에서 열을 추가하거나 삭제해야 할 경우 테이블은 비활성 상태이어야 하고 필요한 열은 추가 또는 삭제되어야 합니다. 이러한 동작은 열을 고정시킵니다. 실제 채우기가 시작되면 테이블은 나중에 활성화될 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 사용자는 **db_ddladmin** 고정 데이터베이스 역할의 멤버 이거나 고정 데이터베이스 역할 **db_owner** 또는 테이블 소유자의 멤버 여야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `DocumentSummary` 테이블의 `Document` 열을 해당 테이블의 전체 텍스트 인덱스에 추가합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_column 'Production.Document', DocumentSummary, 'add';  
GO  
```  
  
 다음 예에서는 사용자가 `spanishTbl`라는 테이블에 전체 텍스트 인덱스를 만들었다고 가정합니다. 전체 텍스트 인덱스에 `spanishCol` 열을 추가하려면 다음 저장 프로시저를 실행하십시오.  
  
```  
EXEC sp_fulltext_column 'spanishTbl', 'spanishCol', 'add', 0xC0A;  
GO  
```  
  
 이 쿼리를 실행하면 다음과 같은 결과가 나타납니다.  
  
```  
SELECT *   
FROM spanishTbl   
WHERE CONTAINS(spanishCol, 'formsof(inflectional, trabajar)')  
```  
  
 결과 집합은 `trabajar`, `trabajo` 및 `trabajamos`과 같이 작업할 `trabajan`의 다른 형식이 있는 행을 포함합니다.  
  
> [!NOTE]  
>  하나의 전체 텍스트 쿼리 함수 절에 있는 모든 열은 같은 언어를 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [OBJECTPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [Transact-sql&#41;sp_help_fulltext_columns &#40;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)   
 [Transact-sql&#41;sp_help_fulltext_columns_cursor &#40;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [Transact-sql&#41;sp_help_fulltext_tables &#40;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [Transact-sql&#41;sp_help_fulltext_tables_cursor &#40;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;전체 텍스트 검색 및 의미 체계 검색 저장 프로시저 ](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
