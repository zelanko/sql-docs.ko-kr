---
title: sys.fulltext_catalogs (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_catalogs_TSQL
- sys.fulltext_catalogs
- fulltext_catalogs
- fulltext_catalogs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_catalogs catalog view
ms.assetid: cf1489ff-4819-41fa-a62a-4ed797a16207
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d4f6099b6f741dd5f0f29687cacc37e6cdfe6fb2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47712171"
---
# <a name="sysfulltextcatalogs-transact-sql"></a>sys.fulltext_catalogs(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 전체 텍스트 카탈로그에 대해 한 행을 포함합니다.  
  
> [!NOTE]  
>  이후 릴리스에서 다음 열이 제거 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **data_space_id**합니다 **file_id**, 및 **경로**합니다. 새 개발 작업에서는 이러한 열을 사용하지 말고 이러한 열을 사용 중인 응용 프로그램을 가능한 한 빨리 수정하십시오.  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|fulltext_catalog_id|**int**|전체 텍스트 카탈로그의 ID입니다. 데이터베이스의 전체 텍스트 카탈로그에서 고유합니다.|  
|NAME|**sysname**|카탈로그의 이름입니다. 데이터베이스 내에서 고유합니다.|  
|path|**nvarchar(260)**|파일 시스템에 있는 카탈로그 디렉터리의 이름입니다.|  
|is_default|**bit**|기본 전체 텍스트 카탈로그입니다.<br /><br /> True = 기본값<br /><br /> False = 기본값이 아님|  
|is_accent_sensitivity_on|**bit**|카탈로그의 악센트 구분 설정입니다.<br /><br /> True = 악센트 구분<br /><br /> False = 악센트 구분 안 함|  
|data_space_id|**int**|이 카탈로그가 만들어진 파일 그룹입니다.|  
|file_id|**int**|카탈로그와 연결된 전체 텍스트 파일의 파일 ID입니다.|  
|principal_id|**int**|전체 텍스트 카탈로그를 소유하는 데이터베이스 보안 주체의 ID입니다.|  
|is_importing|**bit**|전체 텍스트 카탈로그를 가져올 것인지 여부를 나타냅니다.<br /><br /> 1 = 카탈로그를 가져옵니다.<br /><br /> 2 = 카탈로그를 가져오지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [CREATE FULLTEXT CATALOG&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [ALTER FULLTEXT CATALOG&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 ["DROP FULLTEXT CATALOG&#40;Transact-SQL&#41;"](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)  
  
  
