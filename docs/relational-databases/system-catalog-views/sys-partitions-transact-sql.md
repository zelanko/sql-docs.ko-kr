---
title: sys.partitions (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- partitions
- partitions_TSQL
- sys.partitions_TSQL
- sys.partitions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partitions catalog view
ms.assetid: 1c19e1b1-c925-4dad-a652-581692f4ab5e
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 661a37b4136202b9a83b863535670a88a3f100dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102184"
---
# <a name="syspartitions-transact-sql"></a>sys.partitions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터베이스 내의 모든 테이블 및 대부분의 인덱스에서 각 파티션당 행 하나를 포함합니다. Full-Text, Spatial, XML 등의 특수 인덱스 유형은 이 뷰에 포함되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내의 모든 테이블 및 인덱스는 명시적으로 분할되었는지 여부에 상관없이 최소한 하나의 파티션을 포함합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|파티션 ID를 나타냅니다. 데이터베이스 내에서 고유합니다.|  
|object_id|**int**|이 파티션이 속한 개체의 ID를 나타냅니다. 모든 테이블 또는 뷰는 최소한 하나 이상의 파티션으로 구성됩니다.|  
|index_id|**int**|이 파티션이 속한 개체 내부의 인덱스 ID를 나타냅니다.<br /><br /> 0 = 힙<br />1 = 클러스터형 인덱스<br />2 이상 = 비클러스터형 인덱스|  
|partition_number|**int**|소유하는 인덱스나 힙 내의 1부터 시작하는 파티션 번호입니다. 분할되지 않은 테이블과 인덱스의 경우 이 열의 값은 1입니다.|  
|hobt_id|**bigint**|이 파티션에 대한 행을 포함하는 데이터 힙 또는 B-트리의 ID를 나타냅니다.|  
|rows|**bigint**|이 파티션에 있는 행의 대략적인 수를 나타냅니다.|  
|filestream_filegroup_id|**smallint**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 이 파티션에 저장된 FILESTREAM 파일 그룹의 ID를 나타냅니다.|  
|data_compression|**tinyint**|각 파티션의 압축 상태를 나타냅니다.<br /><br /> 0 = 없음 <br />1 = ROW <br />2 = PAGE <br />3 = COLUMNSTORE: **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br />4 = COLUMNSTORE_ARCHIVE: **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> **참고:** 모든 버전에서 전체 텍스트 인덱스를 압축할지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.|  
|data_compression_desc|**nvarchar(60)**|각 파티션의 압축 상태를 나타냅니다. rowstore 테이블의 가능한 값은 NONE, ROW 및 PAGE입니다. columnstore 테이블의 가능한 값은 COLUMNSTORE 및 COLUMNSTORE_ARCHIVE입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
