---
title: sys.fulltext_semantic_languages (TRANSACT-SQL) | Microsoft Docs
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
ms.openlocfilehash: c060f08ff70e04a22af1eb9de09aeb1e3bf4ff71
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133783"
---
# <a name="sysfulltextsemanticlanguages-transact-sql"></a>sys.fulltext_semantic_languages(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 의미 체계 모델이 등록된 언어마다 하나의 행을 반환합니다. 언어 모델을 등록하면 의미 체계 인덱싱에 해당 언어를 사용하도록 설정됩니다.  
  
 이 카탈로그 뷰에 비슷합니다 [sys.fulltext_languages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)합니다.  
    
||||  
|-|-|-|  
|**열 이름**|**형식**|**설명**|  
|lcid|ssNoversion|언어의 Microsoft Windows LCID(로캘 ID)입니다.|  
|name|sysname|별칭 값 이거나 [sys.syslanguages &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 의 값에 해당 하 **lcid**, 또는 숫자로 된 LCID의 문자열 표현입니다.|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 자세한 내용은 [의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)을 참조하세요.  
  
## <a name="metadata"></a>메타데이터  
 의미 체계 인덱싱을 지원 하기 위해 설치 된 의미 체계 언어 통계 데이터베이스에 대 한 자세한 내용은 카탈로그 뷰를 쿼리하여 [sys.fulltext_semantic_language_statistics_database &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 사용자가 소유하고 있거나 사용 권한을 부여 받은 보안 개체에 대해서만 카탈로그 뷰의 메타데이터를 볼 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 쿼리 하는 방법 **sys.fulltext_semantic_languages** 정보를 가져옵니다 언어 모델에 등록 된 모든 의미 체계 인덱싱의 현재 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
```  
SELECT * FROM sys.fulltext_semantic_languages;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
