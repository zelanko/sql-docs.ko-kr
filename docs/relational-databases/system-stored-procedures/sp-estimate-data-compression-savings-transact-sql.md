---
title: sp_estimate_data_compression_savings (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 25798372f2b949446b746164665dbfe6752443d7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spestimatedatacompressionsavings-transact-sql"></a>sp_estimate_data_compression_savings(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  요청된 개체의 현재 크기를 반환하고 요청된 압축 상태에 대한 개체 크기를 예상합니다. 전체 테이블 또는 테이블 일부에 대해 압축을 계산할 수 있습니다. 여기에는 힙, 클러스터형 인덱스, 비클러스터형 인덱스, 인덱싱된 뷰 및 테이블/인덱스 파티션이 포함됩니다. 개체는 행 압축 또는 페이지 압축을 사용하여 압축할 수 있습니다. 테이블, 인덱스 또는 파티션이 이미 압축된 경우 이 절차에 따라 테이블, 인덱스 또는 파티션이 다시 압축되는 경우의 크기를 예상할 수 있습니다.  
  
> [!NOTE]  
>  압축 및 **sp_estimate_data_compression_savings** 의 일부 버전 에서만에서 사용할 수 없는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 이 저장 프로시저는 요청된 압축 설정을 사용할 경우의 개체 크기를 예상하기 위해 원본 개체를 샘플링하고 이 데이터를 tempdb에 생성된 해당 테이블 및 인덱스에 로드합니다. 그런 다음 tempdb에 생성된 테이블 또는 인덱스가 요청된 설정으로 압축되고 예상된 압축 전후 크기 변경 사항이 계산됩니다.  
  
 테이블, 인덱스 또는 파티션에 사용의 압축 상태를 변경 하는 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 또는 [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) 문. 압축에 대 한 일반 정보를 참조 하십시오. [데이터 압축](../../relational-databases/data-compression/data-compression.md)합니다.  
  
> [!NOTE]  
>  기존 데이터가 조각화된 경우 인덱스를 다시 작성하면 압축을 사용하지 않아도 크기를 줄일 수 있습니다. 인덱스를 다시 작성하는 동안 인덱스에는 채우기 비율이 적용됩니다. 이렇게 하면 인덱스 크기가 커질 수 있습니다.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_estimate_data_compression_savings   
     [ @schema_name = ] 'schema_name'    
   , [ @object_name = ] 'object_name'   
   , [@index_id = ] index_id   
   , [@partition_number = ] partition_number   
   , [@data_compression = ] 'data_compression'   
[;]  
```  
  
## <a name="arguments"></a>인수  
 [ @schema_name=] '*schema_name*'  
 테이블 또는 인덱싱된 뷰를 포함하는 데이터베이스 스키마의 이름입니다. *schema_name* 은 **sysname**합니다. 경우 *schema_name* 가 NULL 이면 현재 사용자의 기본 스키마가 사용 됩니다.  
  
 [ @object_name=] '*object_name*'  
 인덱스가 있는 테이블 또는 인덱싱된 뷰의 이름입니다. *object_name*은 **sysname**입니다.  
  
 [ @index_id=] '*index_id*'  
 인덱스의 ID입니다. *index_id* 은 **int**, 다음 값 중 하나가 될 수 있습니다: 인덱스, NULL 또는 0의 ID 번호 *object_id* 힙. 기본 테이블 또는 뷰에 대한 모든 인덱스 정보를 반환하려면 NULL을 지정합니다. NULL을 지정 하는 경우 NULL을 지정 해야 *partition_number*합니다.  
  
 [ @partition_number=] '*partition_number*'  
 개체의 파티션 번호입니다. *partition_number* 은 **int**, 다음 값 중 하나가 될 수 있습니다: 인덱스 또는 힙, NULL 또는 1 분할 되지 않은 인덱스 또는 힙의 파티션 번호입니다.  
  
 파티션을 지정 하려면 지정할 수도 있습니다는 [$partition](../../t-sql/functions/partition-transact-sql.md) 함수입니다. 소유하는 개체의 모든 파티션에 대한 정보를 반환하려면 NULL을 지정합니다.  
  
 [ @data_compression=] '*data_compression*'  
 계산할 압축 유형입니다. *data_compression* 다음 값 중 하나일 수 있습니다: NONE, 행 또는 페이지입니다.  
  
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
  
## <a name="remarks"></a>주의  
 sp_estimate_data_compression_savings를 사용하면 테이블 또는 파티션에 행 또는 페이지 압축을 사용하도록 설정할 경우의 압축 전후 크기 변경 사항을 예상할 수 있습니다. 예를 들어 평균 행 크기가 40% 줄어드는 경우 개체 크기를 40% 줄일 수 있습니다. 공간 크기는 채우기 비율과 행 크기에 따라 달라지므로 공간이 절약되지 않을 수도 있습니다. 예를 들어 8000바이트 길이의 행이 있고 행 크기를 40% 줄인 경우에도 여전히 데이터 페이지 하나에 행 하나만 넣을 수 있습니다. 이 경우에는 공간이 절약되지 않습니다.  
  
 sp_estimate_data_compression_savings 실행 결과에서 테이블이 확장됨을 나타내는 경우 테이블의 많은 행이 데이터 형식의 전체 자릿수를 거의 모두 사용하며 압축된 형식에 필요한 작은 오버헤드 추가분이 압축으로 얻을 수 있는 공간 절약보다 큰 것입니다. 드물지만 이러한 경우에는 압축을 사용하지 마십시오.  
  
 테이블에 압축을 사용하도록 설정한 경우 sp_estimate_data_compression_savings를 사용하면 테이블을 압축하지 않을 경우의 평균 행 크기를 예상할 수 있습니다.  
  
 이러한 작업 시 테이블에 대한 IS 잠금을 획득할 수 있습니다. IS 잠금을 획득할 수 없는 경우 프로시저가 차단됩니다. 테이블은 커밋된 읽기 격리 수준에서 검색됩니다.  
  
 요청된 압축 설정이 현재 압축 설정과 동일한 경우 저장 프로시저는 기존 채우기 비율을 사용하여 데이터 조각화가 없을 경우의 예상 크기를 반환합니다.  
  
 인덱스 또는 파티션 ID가 없으면 결과가 반환되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 테이블에 대한 SELECT 권한이 필요합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 이 프로시저는 columnstore 테이블에 적용되지 않으므로 데이터 압축 매개 변수 COLUMNSTORE 및 COLUMNSTORE_ARCHIVE를 허용하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Production.WorkOrderRouting` 압축을 사용하여 압축할 경우 `ROW` 테이블 크기를 계산합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_estimate_data_compression_savings 'Production', 'WorkOrderRouting', NULL, NULL, 'ROW' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [데이터베이스 엔진 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [유니코드 압축 구현](../../relational-databases/data-compression/unicode-compression-implementation.md)  
  
  
