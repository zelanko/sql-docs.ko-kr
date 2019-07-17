---
title: sys.dm_db_persisted_sku_features (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_persisted_sku_features_TSQL
- sys.dm_db_persisted_sku_features
- dm_db_persisted_sku_features_TSQL
- dm_db_persisted_sku_features
dev_langs:
- TSQL
helpviewer_keywords:
- editions [SQL Server], feature restrictions
- sys.dm_db_persisted_sku_features dynamic management view
ms.assetid: b4b29e97-b523-41b9-9528-6d4e84b89e09
author: stevestein
ms.author: sstein
ms.openlocfilehash: f59d96f9a1aa6598c5acb4fe9a88ea57965ede5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096267"
---
# <a name="sysdmdbpersistedskufeatures-transact-sql"></a>sys.dm_db_persisted_sku_features(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 일부 기능 중 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 데이터베이스 파일의 정보를 저장하는 방법이 변경되었습니다. 이러한 기능은 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전으로 제한됩니다. 이러한 기능을 포함하는 데이터베이스는 이러한 기능이 지원되지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전으로 이동할 수 없습니다. 현재 데이터베이스에서 사용 되는 버전별 기능을 나열 하려면 sys.dm_db_persisted_sku_features 동적 관리 뷰를 사용 합니다.
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|feature_name|**sysname**|데이터베이스에 설정되어 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 모든 버전에서 지원되지 않는 기능의 외부 이름입니다. 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 모든 사용 가능한 버전으로 마이그레이션하려면 먼저 이 기능을 제거해야 합니다.|  
|feature_id|**int**|기능과 연관된 기능 ID입니다. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)].|  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>설명  
 특정 버전으로 제한 될 수 있는 기능은 데이터베이스에서 사용 하는 경우 뷰는 없는 행을 반환 합니다.  
  
 sys.dm_db_persisted_sku_features에 특정 제한 하는 대로 다음 데이터베이스 변경 기능을 나열할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전:  
  
-   **ChangeCapture**: 데이터베이스에 변경 데이터 캡처를 사용할 수 있음을 나타냅니다. 변경 데이터 캡처를 제거 하려면 사용 합니다 [sys.sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) 저장 프로시저입니다. 자세한 내용은 [변경 데이터 캡처 정보&#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)를 참조하세요.  
  
-   **ColumnStoreIndex**: 하나 이상의 테이블에 columnstore 인덱스를 나타냅니다. 데이터베이스 버전으로 이동할 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 기능은 지원 하지 않는, 사용 합니다 [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) 또는 [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) columnstore 인덱스를 제거 하는 문. 자세한 내용은 [Columnstore 인덱스](../../relational-databases/indexes/columnstore-indexes-overview.md)합니다.  
  
    **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
-   **압축**: 하나 이상의 테이블 또는 인덱스 데이터 압축 또는 vardecimal 저장소 형식을 사용 함을 나타냅니다. 데이터베이스 버전으로 이동할 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 기능은 지원 하지 않는, 사용 하 여는 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 또는 [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) 문을 데이터 압축을 제거 합니다. vardecimal 저장소 형식을 제거하려면 sp_tableoption 문을 사용합니다. 자세한 내용은 [Data Compression](../../relational-databases/data-compression/data-compression.md)을 참조하세요.  
  
-   **MultipleFSContainers**: 데이터베이스가 여러 FILESTREAM 컨테이너를 사용 함을 나타냅니다. 데이터베이스에 여러 컨테이너 (파일)를 사용 하 여 FILESTREAM 파일 그룹입니다. 자세한 내용은 [FILESTREAM&#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)을 참조하세요.  
  
-   **InMemoryOLTP**: 데이터베이스에서 메모리 내 OLTP를 사용 함을 나타냅니다. 데이터베이스에 MEMORY_OPTIMIZED_DATA 파일 그룹이 포함됩니다. 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
  **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]). 
  
-   **분할 합니다.** 데이터베이스에 분할된 테이블, 분할된 인덱스, 파티션 구성표 또는 파티션 함수가 포함되도록 지정합니다. 데이터베이스가 Enterprise 또는 Developer 이외의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전으로 이동하도록 설정하는 경우 테이블이 단일 파티션에 있도록 수정하는 것만으로는 충분하지 않습니다. 분할된 테이블을 제거해야 합니다. 테이블에 데이터가 포함된 경우 각 파티션을 분할되지 않은 테이블로 변환하려면 SWITCH PARTITION을 사용합니다. 그런 다음 분할된 테이블, 파티션 구성표 및 파티션 함수를 삭제합니다.  
  
-   **TransparentDataEncryption.** 투명한 데이터 암호화를 사용하여 데이터베이스를 암호화함을 나타냅니다. 투명한 데이터 암호화를 제거하려면 ALTER DATABASE 문을 사용합니다. 자세한 내용은 [TDE&#40;투명한 데이터 암호화&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하세요.  

> [!NOTE]
> 부터 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 서비스 팩 1에서는 이러한 기능을 사용할 수 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에만 Enterprise 또는 Developer Edition으로 제한 되지 않는 한 합니다.

 데이터베이스에서 특정 버전으로 제한되는 기능을 사용하는지 확인하려면 데이터베이스에서 다음 문을 실행합니다.  
  
```sql  
SELECT feature_name FROM sys.dm_db_persisted_sku_features;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [버전 및 SQL Server 2016의 지원되는 기능](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [버전 및 SQL Server 2017 의 지원 되는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  
