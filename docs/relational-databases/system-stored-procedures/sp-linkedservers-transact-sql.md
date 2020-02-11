---
title: sp_linkedservers (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_linkedservers
- sp_linkedservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_linkedservers
ms.assetid: d8f82f78-8a1f-4831-bcee-7c36c6e7dfbb
author: stevestein
ms.author: sstein
ms.openlocfilehash: 675707453fbc79f3f9c578469ed5e78b73d2fbfa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139826"
---
# <a name="sp_linkedservers-transact-sql"></a>sp_linkedservers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로컬 서버에 정의되어 있는 연결된 서버 목록을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_linkedservers  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 수(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**SRV_NAME**|**sysname**|연결된 서버의 이름입니다.|  
|**SRV_PROVIDERNAME**|**nvarchar (** 128 **)**|지정되어 있는 연결된 서버에 대한 액세스를 관리하는 OLE DB 공급자의 이름입니다.|  
|**SRV_PRODUCT**|**nvarchar (** 128 **)**|연결된 서버의 제품 이름입니다.|  
|**SRV_DATASOURCE**|**nvarchar (** 4000 **)**|지정되어 있는 연결된 서버에 해당하는 OLE DB의 데이터 원본 속성입니다.|  
|**SRV_PROVIDERSTRING**|**nvarchar (** 4000 **)**|지정되어 있는 연결된 서버에 해당하는 OLE DB의 공급자 문자열 속성입니다.|  
|**SRV_LOCATION**|**nvarchar (** 4000 **)**|지정되어 있는 연결된 서버에 해당하는 OLE DB의 위치 속성입니다.|  
|**SRV_CAT**|**sysname**|지정되어 있는 연결된 서버에 해당하는 OLE DB 카탈로그 속성입니다.|  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_catalogs &#40;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [Transact-sql&#41;sp_column_privileges &#40;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [Transact-sql&#41;sp_columns_ex &#40;](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [Transact-sql&#41;sp_foreignkeys &#40;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [Transact-sql&#41;sp_indexes &#40;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [Transact-sql&#41;sp_primarykeys &#40;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [Transact-sql&#41;sp_table_privileges &#40;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Transact-sql&#41;sp_tables_ex &#40;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;분산 쿼리 저장 프로시저](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)  
  
  
