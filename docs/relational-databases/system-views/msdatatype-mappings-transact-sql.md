---
title: MSdatatype_mappings (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSdatatype_mappings
- MSdatatype_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdatatype_mappings view
ms.assetid: 13cdabb3-6e07-4e8d-ae80-4235022ccc7f
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 71eed306b288dc54c2935f99f8139da42713d6b8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="msdatatypemappings-transact-sql"></a>MSdatatype_mappings(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdatatype_mappings** 뷰를 SQL Server 데이터 형식을 SQL Server 이외 데이터베이스 관리 시스템 (DBMS)에서 사용 되는 데이터 형식에 매핑합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**dbms_name**|**nvarchar(128)**|DBMS의 이름이입니다. 다음은 가능한 값 및 해당 설명을 보려면입니다.<br /><br /> **MSSQLSERVER**: 대상은 SQL Server 데이터베이스입니다.<br />**ORACLE**: 대상은 Oracle 데이터베이스입니다.<br />**DB2**: 대상은 IBM DB2 데이터베이스입니다.<br />**SYBASE**: 대상은 Sybase 데이터베이스입니다.|  
|**sql_type**|**nvarchar(128)**|SQL Server 데이터 형식이입니다.|  
|**dest_type**|**nvarchar(128)**|SQL Server 이외 데이터 형식의 이름이입니다.|  
|**dest_prec**|**bigint**|SQL Server 이외 데이터 형식의 전체 자릿수가입니다.|  
|**dest_create_params**|**int**|내부적으로만 사용됩니다.|  
|**dest_nullable**|**bit**|SQL Server 이외 데이터 형식이 NULL 값을 지원할지 여부입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Oracle 게시자에 대 한 데이터 형식 매핑 지정](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
