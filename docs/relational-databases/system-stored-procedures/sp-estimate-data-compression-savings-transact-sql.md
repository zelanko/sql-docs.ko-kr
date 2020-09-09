---
description: sp_estimate_data_compression_savings(Transact-SQL)
title: sp_estimate_data_compression_savings (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_estimate_data_compression_savings_TSQL
- sp_estimate_data_compression_savings
dev_langs:
- TSQL
helpviewer_keywords:
- compression [SQL Server], estimating
- sp_estimate_data_compression_savings
ms.assetid: 6f6c7150-e788-45e0-9d08-d6c2f4a33729
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4615bc9a30d28224ee3d1ed906a704af923d046d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543508"
---
# <a name="sp_estimate_data_compression_savings-transact-sql"></a>sp_estimate_data_compression_savings(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  요청된 개체의 현재 크기를 반환하고 요청된 압축 상태에 대한 개체 크기를 예상합니다. 전체 테이블 또는 테이블 일부에 대해 압축을 계산할 수 있습니다. 여기에는 힙, 클러스터형 인덱스, 비클러스터형 인덱스, columnstore 인덱스, 인덱싱된 뷰, 테이블 및 인덱스 파티션이 포함 됩니다. 행, 페이지, columnstore 또는 columnstore 보관 압축을 사용 하 여 개체를 압축할 수 있습니다. 테이블, 인덱스 또는 파티션이 이미 압축된 경우 이 절차에 따라 테이블, 인덱스 또는 파티션이 다시 압축되는 경우의 크기를 예상할 수 있습니다.  
  
> [!NOTE]
> 압축 및 **sp_estimate_data_compression_savings** 일부 버전에서는 사용할 수 없습니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 이 저장 프로시저는 요청된 압축 설정을 사용할 경우의 개체 크기를 예상하기 위해 원본 개체를 샘플링하고 이 데이터를 tempdb에 생성된 해당 테이블 및 인덱스에 로드합니다. 그런 다음 tempdb에 생성된 테이블 또는 인덱스가 요청된 설정으로 압축되고 예상된 압축 전후 크기 변경 사항이 계산됩니다.  
  
 테이블, 인덱스 또는 파티션의 압축 상태를 변경 하려면 [ALTER table](../../t-sql/statements/alter-table-transact-sql.md) 또는 [alter index](../../t-sql/statements/alter-index-transact-sql.md) 문을 사용 합니다. 압축에 대 한 일반 정보는 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조 하세요.  
  
> [!NOTE]  
> 기존 데이터가 조각화된 경우 인덱스를 다시 작성하면 압축을 사용하지 않아도 크기를 줄일 수 있습니다. 인덱스를 다시 작성하는 동안 인덱스에는 채우기 비율이 적용됩니다. 이렇게 하면 인덱스 크기가 커질 수 있습니다.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_estimate_data_compression_savings   
     [ @schema_name = ] 'schema_name'    
   , [ @object_name = ] 'object_name'   
   , [ @index_id = ] index_id   
   , [ @partition_number = ] partition_number   
   , [ @data_compression = ] 'data_compression'   
[;]  
```  
  
## <a name="arguments"></a>인수  
 [ @schema_name =] '*schema_name*'  
 테이블 또는 인덱싱된 뷰를 포함하는 데이터베이스 스키마의 이름입니다. *schema_name* 는 **sysname**입니다. *SCHEMA_NAME* NULL 이면 현재 사용자의 기본 스키마가 사용 됩니다.  
  
 [ @object_name =] '*object_name*'  
 인덱스가 있는 테이블 또는 인덱싱된 뷰의 이름입니다. *object_name*은 **sysname**입니다.  
  
 [ @index_id =] *index_id*  
 인덱스의 ID입니다. *index_id* 는 **int**이며 인덱스의 id 번호, NULL 또는 *object_id* 경우 값 중 하나일 수 있습니다. 기본 테이블 또는 뷰에 대한 모든 인덱스 정보를 반환하려면 NULL을 지정합니다. NULL을 지정 하는 경우 *partition_number*에 대해서도 null을 지정 해야 합니다.  
  
 [ @partition_number =] *partition_number*  
 개체의 파티션 번호입니다. *partition_number* 은 **int**이며 인덱스 또는 힙의 파티션 번호, NULL 또는 1 (분할 되지 않은 인덱스 또는 힙의 경우) 중 하나일 수 있습니다.  
  
 파티션을 지정 하려면 [$partition](../../t-sql/functions/partition-transact-sql.md) 함수를 지정할 수도 있습니다. 소유하는 개체의 모든 파티션에 대한 정보를 반환하려면 NULL을 지정합니다.  
  
 [ @data_compression =] '*data_compression*'  
 계산할 압축 유형입니다. *data_compression* 는 NONE, ROW, PAGE, COLUMNSTORE 또는 COLUMNSTORE_ARCHIVE 값 중 하나일 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 테이블, 인덱스 또는 파티션의 현재 크기 및 예상 크기를 제공하는 다음 결과 집합이 반환됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|object_name|**sysname**|테이블 또는 인덱싱된 뷰의 이름입니다.|  
|schema_name|**sysname**|테이블 또는 인덱싱된 뷰의 스키마입니다.|  
|index_id|**int**|인덱스의 인덱스 ID입니다.<br /><br /> 0 = 힙<br /><br /> 1 = 클러스터형 인덱스<br /><br /> > 1 = 비클러스터형 인덱스|  
|partition_number|**int**|파티션 번호입니다. 분할되지 않은 테이블 또는 인덱스의 경우 1을 반환합니다.|  
|size_with_current_compression_setting (KB)|**bigint**|요청된 테이블, 인덱스 또는 파티션의 현재 크기입니다.|  
|size_with_requested_compression_setting (KB)|**bigint**|요청된 압축 설정을 사용하는 테이블, 인덱스 또는 파티션의 예상 크기이며, 해당되는 경우 조각화가 없는 것으로 가정하고 기존 채우기 비율이 사용됩니다.|  
|sample_size_with_current_compression_setting (KB)|**bigint**|현재 압축 설정을 사용하는 샘플의 크기입니다. 여기에는 조각화가 포함됩니다.|  
|sample_size_with_requested_compression_setting (KB)|**bigint**|요청된 압축 설정을 사용하여 만든 샘플의 크기이며, 해당되는 경우 조각화가 없는 것으로 가정하고 기존 채우기 비율을 사용합니다.|  
  
## <a name="remarks"></a>설명  
 를 사용 `sp_estimate_data_compression_savings` 하 여 행, 페이지, columnstore 또는 columnstore 보관 압축에 테이블이 나 파티션을 사용 하도록 설정할 때 발생할 수 있는 절감 액을 예측할 수 있습니다. 예를 들어 평균 행 크기가 40% 줄어드는 경우 개체 크기를 40% 줄일 수 있습니다. 공간 크기는 채우기 비율과 행 크기에 따라 달라지므로 공간이 절약되지 않을 수도 있습니다. 예를 들어 8000 바이트 길이의 행이 있고 해당 크기를 40%로 줄이면 데이터 페이지에 행을 하나만 포함할 수 있습니다. 이 경우에는 공간이 절약되지 않습니다.  
  
 `sp_estimate_data_compression_savings` 실행 결과에서 테이블이 확장됨을 나타내는 경우 테이블의 많은 행이 데이터 형식의 전체 자릿수를 거의 모두 사용하며 압축된 형식에 필요한 작은 오버헤드 추가분이 압축으로 얻을 수 있는 공간 절약보다 큰 것입니다. 드물지만 이러한 경우에는 압축을 사용하지 마십시오.  
  
 테이블에 압축을 사용하도록 설정한 경우 `sp_estimate_data_compression_savings`를 사용하면 테이블을 압축하지 않을 경우의 평균 행 크기를 예상할 수 있습니다.  
  
 이러한 작업 시 테이블에 대한 IS 잠금을 획득할 수 있습니다. IS 잠금을 획득할 수 없는 경우 프로시저가 차단됩니다. 테이블은 커밋된 읽기 격리 수준에서 검색됩니다.  
  
 요청된 압축 설정이 현재 압축 설정과 동일한 경우 저장 프로시저는 기존 채우기 비율을 사용하여 데이터 조각화가 없을 경우의 예상 크기를 반환합니다.  
  
 인덱스 또는 파티션 ID가 없으면 결과가 반환되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 테이블에 대한 `SELECT` 권한이 필요합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 SQL Server 2019 이전에는이 절차가 columnstore 인덱스에 적용 되지 않았기 때문에 데이터 압축 매개 변수 COLUMNSTORE 및 COLUMNSTORE_ARCHIVE를 수락 하지 않았습니다.  SQL Server 2019부터 columnstore 인덱스를 추정의 원본 개체와 요청 된 압축 형식으로 모두 사용할 수 있습니다.

 > [!IMPORTANT]
 > 에서 [메모리 최적화 TempDB 메타 데이터](../databases/tempdb-database.md#memory-optimized-tempdb-metadata) 를 사용 하도록 설정 하면 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 임시 테이블에 columnstore 인덱스를 만들 수 없습니다. 이러한 제한으로 인해 sp_estimate_data_compression_savings은 COLUMNSTORE 및 COLUMNSTORE_ARCHIVE 데이터 압축 매개 변수를 지원 하지 않으므로 메모리 최적화 TempDB 메타 데이터를 사용할 수 있습니다.

## <a name="considerations-for-columnstore-indexes"></a>Columnstore 인덱스에 대한 고려 사항
 부터 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 는 `sp_estimate_compression_savings` columnstore 및 columnstore 보관 압축을 모두 계산 합니다. 페이지 및 행 압축과 달리 columnstore 압축을 개체에 적용 하려면 새 columnstore 인덱스를 만들어야 합니다. 이러한 이유로이 프로시저의 COLUMNSTORE 및 COLUMNSTORE_ARCHIVE 옵션을 사용할 경우 프로시저에 제공 되는 원본 개체의 형식에 따라 압축 된 예상 크기에 사용 되는 columnstore 인덱스 유형이 결정 됩니다. 다음 표에서는 @data_compression 매개 변수가 COLUMNSTORE 또는 COLUMNSTORE_ARCHIVE로 설정 된 경우 각 원본 개체 유형에 대 한 압축 절감 액을 계산 하는 데 사용 되는 참조 개체를 보여 줍니다.

 |원본 개체|참조 개체|
 |-----------------|---------------|
 |힙|클러스터형 columnstore 인덱스|
 |클러스터형 인덱스|클러스터형 columnstore 인덱스|
 |비클러스터형 인덱스|비클러스터형 columnstore 인덱스 (키 열 및 제공 된 비클러스터형 인덱스의 포괄 열 뿐만 아니라 테이블의 파티션 열 포함)|
 |비클러스터형 columnstore 인덱스|비클러스터형 columnstore 인덱스 (제공 된 비클러스터형 columnstore 인덱스와 동일한 열 포함)|
 |클러스터형 columnstore 인덱스|클러스터형 columnstore 인덱스|

> [!NOTE]  
> Rowstore 원본 개체 (클러스터형 인덱스, 비클러스터형 인덱스 또는 힙)에서 columnstore 압축을 추정 하는 경우 원본 개체에 columnstore 인덱스에서 지원 되지 않는 데이터 형식의 열이 있는 경우에는 오류가 발생 하 여 sp_estimate_compression_savings 실패 합니다.

 마찬가지로 `@data_compression` 매개 변수를, 또는로 설정 `NONE` 하 `ROW` `PAGE` 고 원본 개체가 columnstore 인덱스인 경우 다음 표에서는 사용 되는 참조 개체를 간략하게 설명 합니다.

 |원본 개체|참조 개체|
 |-----------------|---------------|
 |클러스터형 columnstore 인덱스|힙|
 |비클러스터형 columnstore 인덱스|비클러스터형 인덱스 (비클러스터형 columnstore 인덱스에 포함 된 열을 키 열로 포함) 및 테이블의 파티션 열 (있는 경우)을 포괄 열로 포함|

> [!NOTE]  
> Columnstore 원본 개체에서 rowstore 압축 (NONE, ROW 또는 PAGE)을 추정 하는 경우 rowstore (비클러스터형) 인덱스에서 지원 되는 제한은 원본 인덱스에 32 개 보다 많은 열이 포함 되지 않아야 합니다.
  
## <a name="examples"></a>예제  
 다음 예에서는 `Production.WorkOrderRouting` 압축을 사용하여 압축할 경우 `ROW` 테이블 크기를 계산합니다.  
  
```sql  
USE AdventureWorks2016;  
GO  
EXEC sp_estimate_data_compression_savings 'Production', 'WorkOrderRouting', NULL, NULL, 'ROW' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [유니코드 압축 구현](../../relational-databases/data-compression/unicode-compression-implementation.md)  
  
  
