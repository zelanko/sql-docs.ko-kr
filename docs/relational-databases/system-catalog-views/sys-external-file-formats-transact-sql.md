---
description: sys. external_file_formats (Transact-sql)
title: sys. external_file_formats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a89efb2c-0a3a-4b64-9284-6e93263e29ac
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 327e43fe36762ae2118c3c737bc0beb28260b8d7
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283794"
---
# <a name="sysexternal_file_formats-transact-sql"></a>sys. external_file_formats (Transact-sql)
[!INCLUDE [sqlserver2016-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdbmi-asa-pdw.md)]

  , 및에 대 한 현재 데이터베이스의 각 외부 파일 형식에 대 한 행을 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSDS](../../includes/sssds-md.md)] [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 합니다.  
  
 의 서버에 있는 각 외부 파일 형식에 대 한 행을 포함 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|file_format_id|**int**|외부 파일 형식에 대 한 개체 ID입니다.||  
|name|**sysname**|파일 형식의 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]및에서는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 데이터베이스에 대해 고유 합니다. 에서 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이는 서버에 대해 고유 합니다.||  
|format_type|**tinyint**|파일 형식 형식입니다.|DELIMITEDTEXT, RCFILE, ORC, PARQUET|  
|field_terminator|**nvarchar (10)**|Format_type = DELIMITEDTEXT의 경우 필드 종결자입니다.||  
|string_delimiter|**nvarchar (10)**|Format_type = DELIMITEDTEXT의 경우 문자열 구분 기호입니다.||  
|date_format|**nvarchar(50)**|Format_type = DELIMITEDTEXT의 경우 사용자 정의 날짜 및 시간 형식입니다.||  
|use_type_default|**bit**|Format_type = 구분 된 텍스트의 경우 PolyBase가 HDFS 텍스트 파일에서로 데이터를 가져올 때 누락 값을 처리 하는 방법을 지정 합니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .|0-누락 된 값을 ' NULL ' 문자열로 저장 합니다.<br /><br /> 1-누락 된 값을 열 기본값으로 저장 합니다.|  
|serde_method|**nvarchar(255)**|Format_type = RCFILE의 경우이는 serialization/deserialization 메서드입니다.||  
|row_terminator|**nvarchar (10)**|Format_type = DELIMITEDTEXT의 경우 외부 Hadoop 파일의 각 행을 종료 하는 문자열입니다.|항상 ' \n '입니다.|  
|encoding|**nvarchar (10)**|Format_type = DELIMITEDTEXT의 경우이는 외부 Hadoop 파일의 인코딩 방법입니다.|항상 ' UTF8 '입니다.|  
|data_compression|**nvarchar(255)**|외부 데이터에 대 한 데이터 압축 방법입니다.|Format_type = DELIMITEDTEXT:<br /><br /> -' org. f i n.<br />-' GzipCodec '가 있습니다.<br /><br /> Format_type = RCFILE:<br /><br /> -' org. f i n.<br /><br /> Format_type = ORC:<br /><br /> -' org. f i n.<br />-' Org.apache.io.compress.snappycodec '가 있습니다.<br /><br /> Format_type = PARQUET:<br /><br /> -' GzipCodec '가 있습니다.<br />-' Org.apache.io.compress.snappycodec '가 있습니다.|  
  
## <a name="permissions"></a>사용 권한  
 사용자가 소유하고 있거나 사용 권한을 부여 받은 보안 개체에 대해서만 카탈로그 뷰의 메타데이터를 볼 수 있습니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [external_data_sources &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [external_tables &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  
