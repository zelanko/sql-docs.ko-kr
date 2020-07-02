---
title: MSdbms_datatype (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2ac552c5fe8efe897ea9066819215c82a115d1d5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725471"
---
# <a name="msdbms_datatype-transact-sql"></a>MSdbms_datatype(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **MSdbms_datatype** 테이블에는 다른 유형의 데이터베이스 복제에서 게시자 또는 구독자로 사용 되는 지원 되는 각 DBMS (데이터베이스 관리 시스템)에서 네이티브 데이터 형식의 전체 목록이 포함 되어 있습니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**datatype_id**|**int**|각 고유 데이터 형식을 식별합니다.|  
|**dbms_id**|**int**|유형이 속한 DBMS를 식별합니다.|  
|**type**|**sysname**|데이터 형식 이름(네이티브)입니다.|  
|**createparams**|**int**|다음과 같은 각 데이터 형식에 적용할 수 있는 길이, 전체 자릿수 및 소수 자릿수의 조합을 정의하는 비트맵입니다.<br /><br /> **0x1** = 전체 자릿수<br /><br /> **0x2** = 배율<br /><br /> **0x4** = 길이|  
  
## <a name="remarks"></a>설명  
 SQL Server 인스턴스가 SQL Server 이외 데이터베이스를 구독할 수도 있고 SQL Server 이외 구독자에 게시할 수도 있으므로 이 테이블에 SQL Server 데이터 형식에 대한 항목이 포함됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Oracle 게시자에 대 한 데이터 형식 매핑 지정](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
