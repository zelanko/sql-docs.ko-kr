---
title: sys. external_tables (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: fac4720c-b679-4ab2-864b-ff7810a9b559
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c26dbafb76ecf318fa497e11ccac09e800691900
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68054308"
---
# <a name="sysexternal_tables-transact-sql"></a>sys. external_tables (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  현재 데이터베이스의 각 외부 테이블에 대 한 행을 포함 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|\<상속 된 열>||이 뷰가 상속 하는 열 목록은 [sys. 개체 &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조 하세요.||  
|max_column_id_used|**int**|이 테이블에 사용 되는 최대 열 ID입니다.||  
|uses_ansi_nulls|**bit**|테이블이 SET ANSI_NULLS 데이터베이스 옵션을 ON으로 설정하여 생성되었습니다.||  
|data_source_id|**int**|외부 데이터 원본에 대 한 개체 ID입니다.||  
|file_format_id|**int**|HADOOP 외부 데이터 원본에 대 한 외부 테이블의 경우이는 외부 파일 형식에 대 한 개체 ID입니다.||  
|위치|**nvarchar(4000)**|HADOOP 외부 데이터 원본에 대 한 외부 테이블의 경우이는 HDFS의 외부 데이터 경로입니다.||  
|reject_type|**tinyint**|HADOOP 외부 데이터 원본에 대 한 외부 테이블의 경우 외부 데이터를 쿼리할 때 거부 된 행이 계산 되는 방식입니다.|VALUE-거부 된 행 수입니다.<br /><br /> 백분율-거부 된 행의 백분율입니다.|  
|reject_value|**float**|HADOOP 외부 데이터 원본에 대 한 외부 테이블:<br /><br /> *Reject_type =* value의 경우 쿼리가 실패 하기 전까지 허용 되는 행 거부 수입니다.<br /><br /> *Reject_type* =%의 경우 쿼리가 실패 하기 전까지 허용 되는 행 거부의 백분율입니다.||  
|reject_sample_value|**int**|*Reject_type* =%의 경우 거부 된 행의 백분율을 계산 하기 전에 성공적으로 또는 실패 한 로드 행의 수입니다.|Reject_type = VALUE 인 경우 NULL입니다.|  
|distribution_type|**int**|외부 테이블의 경우 SHARD_MAP_MANAGER 외부 데이터 원본에 대해 기본 테이블에 있는 행의 데이터 배포입니다.|0-분할 된<br /><br /> 1-복제 됨<br /><br /> 2 라운드 로빈|  
|distribution_desc|**nvarchar(120)**|외부 테이블의 경우 SHARD_MAP_MANAGER 외부 데이터 원본에 대해 문자열로 표시 되는 배포 유형입니다.||  
|sharding_column_id|**int**|외부 테이블의 경우 SHARD_MAP_MANAGER 외부 데이터 원본 및 분할 된 배포의 경우 분할 key 값을 포함 하는 열의 열 ID입니다.||  
|remote_schema_name|**sysname**|외부 테이블 SHARD_MAP_MANAGER 외부 데이터 원본에 대 한 외부 테이블은 원격 데이터베이스에 있는 기본 테이블이 있는 스키마입니다 (외부 테이블이 정의 된 스키마와 다른 경우).||  
|remote_object_name|**sysname**|외부 테이블 SHARD_MAP_MANAGER 외부 데이터 원본에 대 한 외부 테이블의 경우이 이름은 원격 데이터베이스에 있는 기본 테이블의 이름입니다 (외부 테이블의 이름과 다른 경우).||  
  
## <a name="permissions"></a>사용 권한  
 사용자가 소유하고 있거나 사용 권한을 부여 받은 보안 개체에 대해서만 카탈로그 뷰의 메타데이터를 볼 수 있습니다.  자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [external_file_formats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [external_data_sources &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [CREATE EXTERNAL TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  
