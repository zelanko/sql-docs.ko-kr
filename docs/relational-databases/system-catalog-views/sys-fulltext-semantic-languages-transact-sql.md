---
title: sys.fulltext_semantic_languages (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fulltext_semantic_languages
- fulltext_semantic_languages_TSQL
- sys.fulltext_semantic_languages
- sys.fulltext_semantic_languages_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.fulltext_semantic_languages catalog view
ms.assetid: b42a85e6-1db9-4a22-8a70-014574c95198
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b1ea481151f7f9ac26d18aec4057ff9ab83e5d25
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysfulltextsemanticlanguages-transact-sql"></a>sys.fulltext_semantic_languages(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 의미 체계 모델이 등록된 언어마다 하나의 행을 반환합니다. 언어 모델을 등록하면 의미 체계 인덱싱에 해당 언어를 사용하도록 설정됩니다.  
  
 이 카탈로그 뷰는 비슷합니다 [sys.fulltext_languages&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
    
||||  
|-|-|-|  
|**열 이름**|**형식**|**Description**|  
|lcid|int|언어의 Microsoft Windows LCID(로캘 ID)입니다.|  
|name|sysname|별칭 값 이거나 [sys.syslanguages&#40; Transact SQL &#41; ](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 의 값에 해당 하 **lcid**, 또는 숫자로 된 LCID의 문자열 표현입니다.|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 자세한 내용은 [의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)을 참조하세요.  
  
## <a name="metadata"></a>메타데이터  
 의미 체계 인덱싱을 지원 하기 위해 설치 된 의미 체계 언어 통계 데이터베이스에 대 한 자세한 내용은 카탈로그 뷰를 쿼리 [sys.fulltext_semantic_language_statistics_database&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 사용자가 소유하고 있거나 사용 권한을 부여 받은 보안 개체에 대해서만 카탈로그 뷰의 메타데이터를 볼 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 쿼리 하는 방법을 **sys.fulltext_semantic_languages** 의미 체계 인덱싱의 현재 인스턴스에 언어 모델에 등록 된 모든 작업에 대 한 정보를 가져오려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
```  
SELECT * FROM sys.fulltext_semantic_languages;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
