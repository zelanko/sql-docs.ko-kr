---
title: sys.external_tables (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: fac4720c-b679-4ab2-864b-ff7810a9b559
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 06f71aedda72735652da9ee353dcd62e5c24b48c
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "33181319"
---
# <a name="sysexternaltables-transact-sql"></a>sys.external_tables (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  현재 데이터베이스의 각 외부 테이블에 대 한 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|\<열을 상속 >||이 뷰가 상속 하는 열 목록은 참조 [sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)합니다.||  
|max_column_id_used|**int**|이 테이블에 대해 사용 되는 최대 열 ID입니다.||  
|uses_ansi_nulls|**bit**|테이블이 SET ANSI_NULLS 데이터베이스 옵션을 ON으로 설정하여 생성되었습니다.||  
|data_source_id|**int**|외부 데이터 원본에 대 한 개체 ID입니다.||  
|file_format_id|**int**|HADOOP 외부 데이터 소스를 통해 외부 테이블에는 외부 파일 형식에 대 한 개체 ID입니다.||  
|위치|**nvarchar(4000)**|HADOOP 외부 데이터 소스를 통해 외부 테이블에 대 한 HDFS에서 외부 데이터의 경로입니다.||  
|reject_type|**tinyint**|HADOOP 외부 데이터 소스를 통해 외부 테이블 거부 된 행은 외부 데이터를 쿼리할 때는 계산 하는 방법입니다.|값-거부 된 행의 수입니다.<br /><br /> 백분율 – 거부 된 행의 비율입니다.|  
|reject_value|**float**|에 대 한 외부 테이블을 통해 HADOOP 외부 데이터 원본:<br /><br /> 에 대 한 *reject_type =* 값에 쿼리를 중지 하기 전에 허용할 사용 권한 거부 행의 수입니다.<br /><br /> 에 대 한 *reject_type* 백분율 = 쿼리가 실패 하기 전까지 허용 거부 사유 행의 비율입니다.||  
|reject_sample_value|**int**|에 대 한 *reject_type* = 백분율, 거부 된 행의 비율을 계산 하기 전에 로드할 성공 또는 실패 한, 행의 수입니다.|경우에는 NULL reject_type = VALUE입니다.|  
|distribution_type|**int**|SHARD_MAP_MANAGER 외부 데이터 소스를 통해 외부 테이블의 경우 기본 테이블에서 행의 데이터 분포입니다.|0 – sharded 일<br /><br /> 1 – 복제<br /><br /> 2-라운드 로빈|  
|distribution_desc|**nvarchar(120)**|SHARD_MAP_MANAGER 외부 데이터 소스를 통해 외부 테이블에 대 한 문자열로 표시 되는 배포 형식입니다.||  
|sharding_column_id|**int**|SHARD_MAP_MANAGER 외부 데이터 원본 및 sharded 배포를 통해 외부 테이블에 대 한 분할 키 값을 포함 하는 열의 열 ID입니다.||  
|remote_schema_name|**sysname**|SHARD_MAP_MANAGER 외부 데이터 소스를 통해 외부 테이블에 대 한 기본 테이블 (외부 테이블 정의 된 스키마와에서 다름) 경우 원격 데이터베이스에 있는 위치 스키마입니다.||  
|remote_object_name|**sysname**|SHARD_MAP_MANAGER 외부 데이터 소스를 통해 외부 테이블에 대 한 원격 데이터베이스 (다른 경우 외부 테이블의 이름)의 기본 테이블의 이름입니다.||  
  
## <a name="permissions"></a>사용 권한  
 사용자가 소유하고 있거나 사용 권한을 부여 받은 보안 개체에 대해서만 카탈로그 뷰의 메타데이터를 볼 수 있습니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [sys.external_file_formats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [sys.external_data_sources &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [CREATE EXTERNAL TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  
