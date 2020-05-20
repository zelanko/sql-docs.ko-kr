---
title: sys. external_data_sources (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1016db6e-9950-4ae2-a004-bd4171e27359
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bbec44831d7025fd53cafe0248eb1f69b79bf14d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828167"
---
# <a name="sysexternal_data_sources-transact-sql"></a>sys.external_data_sources(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  , 및에 대 한 현재 데이터베이스의 각 외부 데이터 원본에 대 한 행을 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSDS](../../includes/sssds-md.md)] [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 합니다.  
  
 의 서버에 있는 각 외부 데이터 원본에 대 한 행을 포함 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 합니다.  
  
|열 이름|데이터 형식|설명|범위|  
|-----------------|---------------|-----------------|-----------|  
|data_source_id|**int**|외부 데이터 원본에 대 한 개체 ID입니다.||  
|name|**sysname**|외부 데이터 원본의 이름입니다.||  
|위치|**nvarchar(4000)**|외부 데이터 원본에 대 한 프로토콜, IP 주소 및 포트를 포함 하는 연결 문자열입니다.||  
|type_desc|**nvarchar(255)**|문자열로 표시 되는 데이터 원본 유형입니다.|HADOOP, RDBMS, SHARD_MAP_MANAGER, RemoteDataArchiveTypeExtDataSource|  
|형식|**tinyint**|숫자로 표시 되는 데이터 원본 유형입니다.|0-HADOOP<br /><br /> 1-RDBMS<br /><br /> 2-SHARD_MAP_MANAGER<br /><br /> 3-RemoteDataArchiveTypeExtDataSource|  
|resource_manager_location|**nvarchar(4000)**|HADOOP 형식의 경우 Hadoop 리소스 관리자의 IP 및 포트 위치입니다. 이는 Hadoop 데이터 원본에서 작업을 제출 하는 데 사용 됩니다.<br /><br /> 다른 유형의 외부 데이터 원본에 대해서는 NULL입니다.||  
|credential_id|**int**|외부 데이터 원본에 연결 하는 데 사용 되는 데이터베이스 범위 자격 증명의 개체 ID입니다.||  
|database_name|**sysname**|RDBMS 유형의 경우 원격 데이터베이스의 이름입니다. 유형 SHARD_MAP_MANAGER의 경우 분할 된 데이터베이스 맵 관리자 데이터베이스의 이름입니다. 다른 유형의 외부 데이터 원본에 대해서는 NULL입니다.||  
|shard_map_name|**sysname**|유형 SHARD_MAP_MANAGER의 경우 분할 된 맵의 이름입니다. 다른 유형의 외부 데이터 원본에 대해서는 NULL입니다.||  
  
## <a name="permissions"></a>권한  
 사용자가 소유하고 있거나 사용 권한을 부여 받은 보안 개체에 대해서만 카탈로그 뷰의 메타데이터를 볼 수 있습니다.  자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [external_file_formats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [external_tables &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  
