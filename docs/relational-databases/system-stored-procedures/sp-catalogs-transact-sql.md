---
title: sp_catalogs (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_catalogs_TSQL
- sp_catalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sp_catalogs
ms.assetid: ebb29ee2-be65-4e09-9c53-e3c6d12633e1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0844001016f67d227b4612176b2804dcda0a3d29
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68045944"
---
# <a name="sp_catalogs-transact-sql"></a>sp_catalogs(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정되어 있는 연결된 서버의 카탈로그 목록을 반환합니다. 이것은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 데이터베이스와 동일합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_catalogs [ @server_name = ] 'linked_svr'  
```  
  
## <a name="arguments"></a>인수  
`[ @server_name = ] 'linked_svr'`연결 된 서버의 이름입니다. *linked_svr* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**Catalog_name**|**nvarchar (** 128 **)**|카탈로그의 이름입니다.|  
|**설명**|**nvarchar (** 4000 **)**|카탈로그에 관한 설명입니다.|  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `OLE DB ODBC Linked Server #3`이라는 연결된 서버에 대한 카탈로그 정보를 반환합니다.  
  
> [!NOTE]  
>  유용한 **** 정보를 제공 하려면가 이미 `OLE DB ODBC Linked Server #3` 있어야 합니다. sp_catalogs  
  
```  
USE master;  
GO  
EXEC sp_catalogs 'OLE DB ODBC Linked Server #3';  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [Transact-sql&#41;sp_columns_ex &#40;](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [Transact-sql&#41;sp_column_privileges &#40;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [Transact-sql&#41;sp_foreignkeys &#40;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [Transact-sql&#41;sp_indexes &#40;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [Transact-sql&#41;sp_linkedservers &#40;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [Transact-sql&#41;sp_primarykeys &#40;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [Transact-sql&#41;sp_tables_ex &#40;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [Transact-sql&#41;sp_table_privileges &#40;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
