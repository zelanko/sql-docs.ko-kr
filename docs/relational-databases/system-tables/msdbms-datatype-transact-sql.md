---
title: MSdbms_datatype (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_datatype
- MSdbms_datatype_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype system table
ms.assetid: 606168cc-79a8-442f-ab43-936f8f884d72
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf246256471931292d6dfcee8a83386bce256e08
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62816946"
---
# <a name="msdbmsdatatype-transact-sql"></a>MSdbms_datatype(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSdbms_datatype** 표에 게시자 또는 구독자 다른 유형의 데이터베이스 복제에 사용 되는 각 지원 되는 데이터베이스 관리 시스템 (DBMS)에서 네이티브 데이터 형식의 전체 목록이 들어 있습니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**datatype_id**|**int**|각 고유 데이터 형식을 식별합니다.|  
|**dbms_id**|**int**|유형이 속한 DBMS를 식별합니다.|  
|**type**|**sysname**|데이터 형식 이름(네이티브)입니다.|  
|**createparams**|**int**|다음과 같은 각 데이터 형식에 적용할 수 있는 길이, 전체 자릿수 및 소수 자릿수의 조합을 정의하는 비트맵입니다.<br /><br /> **0x1** = PRECISION.<br /><br /> **0x2** = SCALE.<br /><br /> **0x4** = LENGTH.|  
  
## <a name="remarks"></a>Remarks  
 SQL Server 인스턴스의 SQL Server 이외 데이터베이스를 구독할와 게시 하는 SQL Server 이외 구독자 수 있으므로이 테이블에서 SQL Server 데이터 형식에 대 한 항목을 포함 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Oracle 게시자에 대 한 데이터 형식 매핑 지정](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
