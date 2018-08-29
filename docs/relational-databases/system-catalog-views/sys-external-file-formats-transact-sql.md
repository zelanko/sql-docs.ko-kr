---
title: sys.external_file_formats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a89efb2c-0a3a-4b64-9284-6e93263e29ac
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ac5155109f7ac5de836df711d6a629dffcdae91b
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43107306"
---
# <a name="sysexternalfileformats-transact-sql"></a>sys.external_file_formats (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  에 대 한 현재 데이터베이스에 각 외부 파일 형식에 대 한 행을 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]하십시오 [!INCLUDE[ssSDS](../../includes/sssds-md.md)], 및 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다.  
  
 각 외부 파일 형식에 대 한 서버에서 한 행을 포함 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|file_format_id|**int**|외부 파일 형식에 대 한 개체 ID입니다.||  
|NAME|**sysname**|파일 형식의 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], 데이터베이스에 대해 고유 합니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 서버에 대해 고유 합니다.||  
|format_type|**tinyint**|파일 형식입니다.|DELIMITEDTEXT, RCFILE, ORC, PARQUET|  
|field_terminator|**nvarchar(10)**|Format_type =, DELIMITEDTEXT 필드 종결자입니다.||  
|string_delimiter|**nvarchar(10)**|Format_type = DELIMITEDTEXT, 문자열 구분 기호입니다.||  
|date_format|**nvarchar(50)**|Format_type = DELIMITEDTEXT, 사용자 정의 날짜 및 시간 형식입니다.||  
|use_type_default|**bit**|Format_type = 구분 기호로 분리 된 텍스트, PolyBase가 HDFS 텍스트 파일에서 데이터를 가져올 때 누락 값을 처리 하는 방법을 지정 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다.|0 – 'NULL' 문자열로 누락 값을 저장 합니다.<br /><br /> 1-열 기본 값으로 누락 된 값을 저장 합니다.|  
|serde_method|**nvarchar(255)**|Format_type = RCFILE 직렬화/역직렬화 메서드입니다.||  
|row_terminator|**nvarchar(10)**|Format_type = DELIMITEDTEXT, 외부 Hadoop 파일의 각 행을 종료 하는 문자열입니다.|항상 ' \n '입니다.|  
|인코딩|**nvarchar(10)**|Format_type = DELIMITEDTEXT, 외부 Hadoop 파일에 대 한 인코딩 방법입니다.|항상 ' UTF8'가 있습니다.|  
|data_compression|**nvarchar(255)**|외부 데이터에 대 한 데이터 압축 메서드입니다.|DELIMITEDTEXT = 했습니다. format_type의 경우:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br />-   'org.apache.hadoop.io.compress.GzipCodec'<br /><br /> Format_type = RCFILE:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br /><br /> ORC = 했습니다. format_type의 경우:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'<br /><br /> Format_type = PARQUET:<br /><br /> -   'org.apache.hadoop.io.compress.GzipCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'|  
  
## <a name="permissions"></a>사용 권한  
 사용자가 소유하고 있거나 사용 권한을 부여 받은 보안 개체에 대해서만 카탈로그 뷰의 메타데이터를 볼 수 있습니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [sys.external_data_sources &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [sys.external_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  
