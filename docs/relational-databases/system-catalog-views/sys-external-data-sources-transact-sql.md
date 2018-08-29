---
title: sys.external_data_sources (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
ms.assetid: 1016db6e-9950-4ae2-a004-bd4171e27359
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6dec76073fbd0a6e0ed7da85dd247f3435dec85b
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43064931"
---
# <a name="sysexternaldatasources-transact-sql"></a>sys.external_data_sources (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  각 외부 데이터 원본에 대 한 현재 데이터베이스에 대 한 행을 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]하십시오 [!INCLUDE[ssSDS](../../includes/sssds-md.md)], 및 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다.  
  
 각 외부 데이터 원본에 대 한 서버에 대 한 행을 포함 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|data_source_id|**int**|외부 데이터 원본에 대 한 개체 ID입니다.||  
|NAME|**sysname**|외부 데이터 원본의 이름입니다.||  
|위치|**nvarchar(4000)**|프로토콜, IP 주소 및 외부 데이터 원본에 대 한 포트를 포함 하는 연결 문자열입니다.||  
|type_desc|**nvarchar(255)**|문자열로 표시 되는 데이터 원본 유형입니다.|HADOOP, RDBMS, SHARD_MAP_MANAGER, RemoteDataArchiveTypeExtDataSource|  
|유형|**tinyint**|데이터 원본 유형에 숫자로 표시 합니다.|0-HADOOP<br /><br /> 1 - RDBMS<br /><br /> 2-SHARD_MAP_MANAGER<br /><br /> 3 - RemoteDataArchiveTypeExtDataSource|  
|resource_manager_location|**nvarchar(4000)**|HADOOP, IP 및 포트 입력에 대 한 Hadoop 리소스 관리자의 위치입니다. Hadoop 데이터 원본에 대해 작업을 제출 하는 것에 대 한 사용 됩니다.<br /><br /> 다른 유형의 외부 데이터 원본에 대해 NULL입니다.||  
|credential_id|**int**|데이터베이스의 개체 ID 범위는 외부 데이터 원본에 연결 하는 데 사용 하는 자격 증명.||  
|database_name|**sysname**|형식용 RDBMS, 원격 데이터베이스의 이름입니다. 형식의 경우 SHARD_MAP_MANAGER 분할 된 데이터베이스 맵 관리자 데이터베이스의 이름입니다. 다른 유형의 외부 데이터 원본에 대해 NULL입니다.||  
|shard_map_name|**sysname**|형식용 SHARD_MAP_MANAGER 분할 된 데이터베이스 맵의 이름입니다. 다른 유형의 외부 데이터 원본에 대해 NULL입니다.||  
  
## <a name="permissions"></a>사용 권한  
 사용자가 소유하고 있거나 사용 권한을 부여 받은 보안 개체에 대해서만 카탈로그 뷰의 메타데이터를 볼 수 있습니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [sys.external_file_formats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [sys.external_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  
