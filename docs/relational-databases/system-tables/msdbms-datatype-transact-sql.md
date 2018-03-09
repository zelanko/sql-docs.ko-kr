---
title: MSdbms_datatype (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSdbms_datatype
- MSdbms_datatype_TSQL
dev_langs: TSQL
helpviewer_keywords: MSdbms_datatype system table
ms.assetid: 606168cc-79a8-442f-ab43-936f8f884d72
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd690436908a61b43b4e7af829e8bc3528fd5305
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="msdbmsdatatype-transact-sql"></a>MSdbms_datatype(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_datatype** 테이블 게시자 또는 구독자 다른 유형의 데이터베이스 복제에 사용 되는 각 지원 되는 데이터베이스 관리 시스템 (DBMS)에서 네이티브 데이터 형식의 전체 목록을 포함 합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**datatype_id**|**int**|각 고유 데이터 형식을 식별합니다.|  
|**dbms_id**|**int**|유형이 속한 DBMS를 식별합니다.|  
|**유형**|**sysname**|데이터 형식 이름(네이티브)입니다.|  
|**createparams**|**int**|다음과 같은 각 데이터 형식에 적용할 수 있는 길이, 전체 자릿수 및 소수 자릿수의 조합을 정의하는 비트맵입니다.<br /><br /> **0x1** = 전체 자릿수입니다.<br /><br /> **0x2** = 합니다.<br /><br /> **0x4** = 길이입니다.|  
  
## <a name="remarks"></a>주의  
 이 테이블에는 SQL Server의 인스턴스 수도 있고 SQL Server 이외 데이터베이스를 구독 하는 SQL Server 이외 구독자를 게시 하기 때문에 SQL Server 데이터 형식에 대 한 항목이 포함 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Oracle 게시자에 대 한 데이터 형식 매핑 지정](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [복제 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
