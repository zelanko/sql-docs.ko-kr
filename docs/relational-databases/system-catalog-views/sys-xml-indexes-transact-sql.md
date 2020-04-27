---
title: sys. xml_indexes (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_indexes_TSQL
- xml_indexes_TSQL
- sys.xml_indexes
- xml_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_indexes catalog view
ms.assetid: 3408de72-b067-4fda-b5d5-8e856dfd9db3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16d474fc6274fd43b7ebc426445a0881181dcf79
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67895060"
---
# <a name="sysxml_indexes-transact-sql"></a>sys.xml_indexes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 XML 인덱스에 대해 행을 반환합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**\<상속 된 열>**||은 (는) [sys. 인덱스](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)에서 열을 상속 합니다.|  
|**using_xml_index_id**|**int**|NULL = 기본 XML 인덱스입니다.<br /><br /> Nonnull = 보조 XML 인덱스입니다.<br /><br /> Nonnull은 기본 XML 인덱스에 대한 자체 조인 참조입니다.|  
|**secondary_type**|**char (1)**|보조 인덱스에 대한 유형 설명입니다.<br /><br /> P = PATH 보조 XML 인덱스<br /><br /> V = VALUE 보조 XML 인덱스<br /><br /> R = PROPERTY 보조 XML 인덱스<br /><br /> NULL = 기본 XML 인덱스|  
|**secondary_type_desc**|**nvarchar(60)**|보조 인덱스에 대한 유형 설명입니다.<br /><br /> PATH = PATH 보조 XML 인덱스<br /><br /> VALUE = VALUE 보조 XML 인덱스<br /><br /> PROPERTY = PROPERTY 보조 XML 인덱스<br /><br /> NULL = 기본 XML 인덱스|  
|**xml_index_type**|**tinyint**|인덱스 유형:<br /><br /> 0 = 기본 XML 인덱스<br /><br /> 1 = 보조 XML 인덱스<br /><br /> 2 = 선택적 XML 인덱스<br /><br /> 3 = 보조 선택적 XML 인덱스|  
|**xml_index_type_description**|**nvarchar(60)**|인덱스 유형의 설명입니다.<br /><br /> PRIMARY_XML<br /><br /> 보조 XML 인덱스<br /><br /> 선택적 XML 인덱스<br /><br /> 보조 선택적 XML 인덱스|  
|**path_id**|**int**|보조 선택적 XML 인덱스를 제외한 모든 XML 인덱스의 경우 NULL입니다.<br /><br /> 보조 선택적 XML 인덱스의 경우 해당 인덱스가 작성된 승격 경로의 ID입니다. 이 값은 sys.selective_xml_index_paths 시스템 뷰의 path_id와 같은 값입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
