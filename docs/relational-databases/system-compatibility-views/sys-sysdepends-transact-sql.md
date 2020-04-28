---
title: sysdepends (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysdepends_TSQL
- sysdepends
- sysdepends_TSQL
- sys.sysdepends
dev_langs:
- TSQL
helpviewer_keywords:
- sysdepends system table
- sys.sysdepends compatibility view
ms.assetid: f9c182cb-386f-4e72-859f-9f1115b389f9
author: rothja
ms.author: jroth
ms.openlocfilehash: 5d928926294bb3e80f860a535a266b5c106e3f18
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68053501"
---
# <a name="syssysdepends-transact-sql"></a>sys.sysdepends(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스의 개체(뷰, 프로시저 및 트리거)와 그 정의에 포함된 개체(테이블, 뷰 및 프로시저) 간의 종속성에 관한 정보를 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|개체 ID입니다.|  
|**depid**|**int**|종속 개체 ID입니다.|  
|**number**|**smallint**|프로시저 번호입니다.|  
|**depnumber**|**smallint**|종속 프로시저 번호입니다.|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deptype**|**tinyint**|다음과 같이 종속 개체 유형을 식별합니다.<br /><br /> 0 = 개체 또는 열(스키마 바운드가 아닌 참조만 해당)<br /><br /> 1 = 개체 또는 열(스키마 바운드 참조)|  
|**depdbid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**depsiteid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**selall**|**bit**|1 = 개체가 SELECT * 문에 사용됩니다.<br /><br /> 0 = 아니요|  
|**resultobj**|**bit**|1 = 개체가 업데이트되고 있습니다.<br /><br /> 0 = 아니요|  
|**readobj**|**bit**|1 = 개체를 읽고 있습니다.<br /><br /> 0 = 아니요|  
  
## <a name="see-also"></a>참고 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Transact-sql&#41;&#40;호환성 뷰](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [Transact-sql&#41;sp_depends &#40;](../../relational-databases/system-stored-procedures/sp-depends-transact-sql.md)   
 [sql_dependencies &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)  
  
  
