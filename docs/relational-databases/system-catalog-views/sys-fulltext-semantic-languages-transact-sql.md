---
description: sys.fulltext_semantic_languages(Transact-SQL)
title: sys. fulltext_semantic_languages (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_semantic_languages
- fulltext_semantic_languages_TSQL
- sys.fulltext_semantic_languages
- sys.fulltext_semantic_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_semantic_languages catalog view
ms.assetid: b42a85e6-1db9-4a22-8a70-014574c95198
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 62b8f1fc18fd5c1253451a6a35eb13fd5e2b2105
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420097"
---
# <a name="sysfulltext_semantic_languages-transact-sql"></a>sys.fulltext_semantic_languages(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 의미 체계 모델이 등록된 언어마다 하나의 행을 반환합니다. 언어 모델을 등록하면 의미 체계 인덱싱에 해당 언어를 사용하도록 설정됩니다.  
  
 이 카탈로그 뷰는 [fulltext_languages &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)와 비슷합니다.  
    
|열 이름|Type|설명|  
|-|-|-|   
|lcid|int|언어의 Microsoft Windows LCID(로캘 ID)입니다.|  
|name|sysname|**Lcid**값에 해당 하는 [transact-sql&#41;&#40;sys.sys언어](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 의 별칭 값 또는 숫자 lcid의 문자열 표현입니다.|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 자세한 내용은 [의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)을 참조하세요.  
  
## <a name="metadata"></a>메타데이터  
 의미 체계 인덱싱을 지원 하기 위해 설치 되는 의미 체계 언어 통계 데이터베이스에 대 한 자세한 내용을 보려면 [SQL&#41;&#40;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)카탈로그 뷰 fulltext_semantic_language_statistics_database를 쿼리 합니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 사용자가 소유하고 있거나 사용 권한을 부여 받은 보안 개체에 대해서만 카탈로그 뷰의 메타데이터를 볼 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 현재 인스턴스의 의미 체계 인덱싱에 대해 등록 된 모든 언어 모델에 대 한 정보를 얻기 위해 **fulltext_semantic_languages** 를 쿼리 하는 방법을 보여 줍니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
```  
SELECT * FROM sys.fulltext_semantic_languages;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
