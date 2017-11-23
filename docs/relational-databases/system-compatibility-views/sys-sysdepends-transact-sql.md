---
title: sys.sysdepends (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sysdepends_TSQL
- sysdepends
- sysdepends_TSQL
- sys.sysdepends
dev_langs: TSQL
helpviewer_keywords:
- sysdepends system table
- sys.sysdepends compatibility view
ms.assetid: f9c182cb-386f-4e72-859f-9f1115b389f9
caps.latest.revision: "43"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 76a51f07ef8b504c616cd4ef080d0c84e9f782a5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="syssysdepends-transact-sql"></a>sys.sysdepends(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스의 개체(뷰, 프로시저 및 트리거)와 그 정의에 포함된 개체(테이블, 뷰 및 프로시저) 간의 종속성에 관한 정보를 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**id**|**int**|개체 ID입니다.|  
|**depid**|**int**|종속 개체 ID입니다.|  
|**번호**|**smallint**|프로시저 번호입니다.|  
|**depnumber**|**smallint**|종속 프로시저 번호입니다.|  
|**상태**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deptype**|**tinyint**|다음과 같이 종속 개체 유형을 식별합니다.<br /><br /> 0 = 개체 또는 열(스키마 바운드가 아닌 참조만 해당)<br /><br /> 1 = 개체 또는 열(스키마 바운드 참조)|  
|**depdbid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**depsiteid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**selall**|**bit**|1 = 개체가 SELECT * 문에 사용됩니다.<br /><br /> 0 = 아니요|  
|**resultobj**|**bit**|1 = 개체가 업데이트되고 있습니다.<br /><br /> 0 = 아니요|  
|**readobj**|**bit**|1 = 개체를 읽고 있습니다.<br /><br /> 0 = 아니요|  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 뷰 &#40; 시스템 테이블 매핑 Transact SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰 &#40; Transact SQL &#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [sp_depends &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-depends-transact-sql.md)   
 [sys.sql_dependencies &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)  
  
  
