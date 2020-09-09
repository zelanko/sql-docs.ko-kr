---
description: sys.xml_schema_wildcards(Transact-SQL)
title: sys.xml_schema_wildcards (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_wildcards
- sys.xml_schema_wildcards_TSQL
- xml_schema_wildcards
- xml_schema_wildcards_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_wildcards catalog view
ms.assetid: 7cedfe9a-e99e-4777-8a28-98674b6e5cff
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 706db88cdc82c7b67105826091f826c62e7f3311
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548632"
---
# <a name="sysxml_schema_wildcards-transact-sql"></a>sys.xml_schema_wildcards(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **N**의 **symbol_space** 에 대 한 특성 와일드 카드 ( **V**의**종류** ) 또는 요소 와일드**카드 (** **W**의 경우) 인 XML 스키마 구성 요소별 행을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**||[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)에서 열을 상속 합니다.|  
|**process_content**|**char(1)**|콘텐츠 처리 방법을 나타냅니다.<br /><br /> S = 엄격한 유효성 검사(유효성 검사를 반드시 수행해야 함)<br /><br /> L = 엄격하지 않은 유효성 검사(가능한 경우 유효성 검사를 수행함)<br /><br /> P = 유효성 검사 건너뛰기|  
|**process_content_desc**|**nvarchar(60)**|콘텐츠 처리 방법에 대한 설명입니다.<br /><br /> **STRICT_VALIDATION**<br /><br /> **LAX_VALIDATION**<br /><br /> **SKIP_VALIDATION**|  
|**disallow_namespaces**|**bit**|0 = [sys.xml_schema_wildcard_namespaces](../../relational-databases/system-catalog-views/sys-xml-schema-wildcard-namespaces-transact-sql.md) 에 열거 된 네임 스페이스도 유일 하 게 사용할 수 있습니다.<br /><br /> 1 = 네임스페이스만 허용되지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Xml 스키마 &#40;XML 형식 시스템&#41; 카탈로그 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
