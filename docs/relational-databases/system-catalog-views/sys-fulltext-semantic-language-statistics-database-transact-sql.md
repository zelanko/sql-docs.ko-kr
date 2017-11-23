---
title: sys.fulltext_semantic_language_statistics_database (Transact SQL) | Microsoft Docs
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
- sys.fulltext_semantic_language_statistics_database_TSQL
- fulltext_semantic_language_statistics_database_TSQL
- fulltext_semantic_language_statistics_database
- sys.fulltext_semantic_language_statistics_database
dev_langs: TSQL
helpviewer_keywords: sys.fulltext_semantic_language_statistics_database catalog view
ms.assetid: 32e95614-ed88-4068-8c37-1e21544717bc
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3aa0d4e32e5356d9e0472f2278c8cb5a94096193
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysfulltextsemanticlanguagestatisticsdatabase-transact-sql"></a>sys.fulltext_semantic_language_statistics_database(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 인스턴스에 설치되어 있는 의미 체계 언어 통계 데이터베이스에 대한 행을 반환합니다.  
  
 이 뷰를 쿼리하여 의미 체계 처리에 필요한 의미 체계 언어 통계 구성 요소에 대한 정보를 확인할 수 있습니다.  
   
  
||||  
|-|-|-|  
|**열 이름**|**형식**|**Description**|  
|**database_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 고유한 데이터베이스 ID입니다.|  
|**register_date**|**datetime**|의미 체계 처리를 위해 데이터베이스가 등록된 날짜입니다.|  
|**registered_by**|**int**|의미 체계 처리를 위해 데이터베이스를 등록한 서버 보안 주체의 ID입니다.|  
|**version**|**nvarchar (128)**|의미 체계 언어 통계 데이터베이스와 관련된 최신 버전 정보입니다.|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 자세한 내용은 [의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)을 참조하세요.  
  
## <a name="metadata"></a>메타데이터  
 의미 체계 인덱싱에 지원 되는 언어에 대 한 내용은 카탈로그 뷰를 쿼리 [sys.fulltext_semantic_languages &#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md).  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 사용자가 소유하고 있거나 사용 권한을 부여 받은 보안 개체에 대해서만 카탈로그 뷰의 메타데이터를 볼 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 쿼리 하는 방법을 **sys.fulltext_semantic_language_statistics_database** 의 현재 인스턴스에 등록 된 의미 체계 언어 통계 데이터베이스에 대 한 정보를 가져오려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
```  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
