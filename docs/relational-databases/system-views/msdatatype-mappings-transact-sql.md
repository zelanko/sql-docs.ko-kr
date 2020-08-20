---
description: MSdatatype_mappings(Transact-SQL)
title: MSdatatype_mappings (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdatatype_mappings
- MSdatatype_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdatatype_mappings view
ms.assetid: 13cdabb3-6e07-4e8d-ae80-4235022ccc7f
author: stevestein
ms.author: sstein
ms.openlocfilehash: f67f313d177b5ef22e6cb97b9ab25d5281c860e2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463854"
---
# <a name="msdatatype_mappings-transact-sql"></a>MSdatatype_mappings(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSdatatype_mappings** 뷰는 SQL Server 데이터 형식을 SQL SERVER 아닌 DBMS (데이터베이스 관리 시스템)에서 사용 하는 데이터 형식에 매핑합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**dbms_name**|**nvarchar(128)**|DBMS의 이름입니다. 다음은 가능한 값과 그에 대 한 설명입니다.<br /><br /> **MSSQLSERVER**: 대상이 SQL Server 데이터베이스입니다.<br />**Oracle**: 대상이 ORACLE 데이터베이스입니다.<br />**DB2**: 대상은 IBM DB2 데이터베이스입니다.<br />**Sybase**: 대상이 SYBASE 데이터베이스입니다.|  
|**sql_type**|**nvarchar(128)**|SQL Server 데이터 형식입니다.|  
|**dest_type**|**nvarchar(128)**|SQL Server 이외 데이터 형식의 이름입니다.|  
|**dest_prec**|**bigint**|SQL Server 이외 데이터 형식의 전체 자릿수입니다.|  
|**dest_create_params**|**int**|내부적으로만 사용됩니다.|  
|**dest_nullable**|**bit**|SQL Server 이외 데이터 형식이 NULL 값을 지원할지 여부입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Oracle 게시자에 대 한 데이터 형식 매핑 지정](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
