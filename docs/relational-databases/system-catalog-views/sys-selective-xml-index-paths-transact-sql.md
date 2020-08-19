---
description: sys.selective_xml_index_paths(Transact-SQL)
title: sys. selective_xml_index_paths (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xml_schema_attributes_TSQL
- xml_schema_attributes
- sys.xml_schema_attributes_TSQL
- sys.xml_schema_attributes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_attributes catalog view
ms.assetid: 07a73d71-ec3e-4894-947a-5859ca62c606
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: adc4ffa7ae43709a572ff1d7f4de1b3e26974ebb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490123"
---
# <a name="sysselective_xml_index_paths-transact-sql"></a>sys.selective_xml_index_paths(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 서비스 팩 1부터 사용할 수 있습니다. sys.selective_xml_index_paths의 각 행은 특정 선택적 XML 인덱스에 대한 승격 경로 하나를 나타냅니다.  
  
 다음 문을 사용하여 테이블 T의 xmlcol에서 선택적 XML 인덱스를 만드는 경우  
  
```  
CREATE SELECTIVE XML INDEX sxi1 ON T(xmlcol)   
FOR ( path1 = '/a/b/c' AS XQUERY 'xs:string',  
      path2 = '/a/b/d' AS XQUERY 'xs:double'  
    )  
```  
  
 인덱스 sxi1에 해당하는 sys.selective_xml_index_paths에 새로운 두 행이 있습니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|XML 열이 포함된 테이블의 ID입니다.|  
|**index_id**|**int**|선택적 XML 인덱스의 고유한 ID입니다.|  
|**path_id**|**int**|승격 XML 경로 ID입니다.|  
|**path**|**nvarchar(4000)**|승격 경로입니다. 예를 들어 '/a/b/c/d/e'입니다.|  
|**name**|**sysname**|경로 이름입니다.|  
|**path_type**|**tinyint**|0 = XQUERY<br /><br /> 1 = SQL|  
|**path_type_desc**|**sysname**|**Path_type** 값 ' XQUERY ' 또는 ' s q l '을 기준으로 합니다.|  
|**xml_component_id**|**int**|데이터베이스에 있는 XML 스키마 구성 요소의 고유 ID입니다.|  
|**xquery_type_description**|**nvarchar(4000)**|지정한 XSD 유형의 이름입니다.|  
|**is_xquery_type_inferred**|**bit**|1 = 유형을 추정할 수 있음|  
|**xquery_max_length**|**smallint**|최대 길이(XSD 유형 문자 수)입니다.|  
|**is_xquery_max_length_inferred**|**bit**|1 = 최대 길이를 유추할 수 있음|  
|**is_node**|**bit**|0 = node() 힌트가 없음<br /><br /> 1 = node() 최적화 힌트가 적용됨|  
|**system_type_id**|**tinyint**|열의 시스템 유형 ID입니다.|  
|**user_type_id**|**tinyint**|열의 사용자 유형 ID입니다.|  
|**max_length**|**smallint**|유형의 최대 길이(바이트)입니다.<br /><br /> -1 = 열 데이터 형식이 varchar(max), nvarchar(max), varbinary(max) 또는 xml입니다.|  
|**전체 자릿수**|**tinyint**|숫자 기반 형식인 경우에는 형식의 최대 전체 자릿수이고 그렇지 않으면 0입니다.|  
|**scale**|**tinyint**|숫자 기반 형식인 경우에는 형식의 최대 소수 자릿수이고 그렇지 않으면 0입니다.|  
|**collation_name**|**sysname**|문자 기반인 경우에는 형식의 데이터 정렬 이름이고 그렇지 않으면 NULL입니다.|  
|**is_singleton**|**bit**|0 = SINGLETON 힌트가 없음<br /><br /> 1 = SINGLETON 최적화 힌트가 적용됨|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Xml 스키마 &#40;XML 형식 시스템&#41; 카탈로그 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
