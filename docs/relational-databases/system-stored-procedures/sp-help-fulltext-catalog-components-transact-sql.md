---
title: sp_help_fulltext_catalog_components (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_catalog_components_TSQL
- sp_help_fulltext_catalog_components
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_catalog_components
ms.assetid: fbd6a3d4-6a4c-42a2-bff8-2a5eb0745e47
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 54c22d025ae809d035fe75a0b8fe89160bdfb84f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720371"
---
# <a name="sphelpfulltextcatalogcomponents-transact-sql"></a>sp_help_fulltext_catalog_components(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스의 모든 전체 텍스트 카탈로그에 사용된 필터, 단어 분리기, 프로토콜 처리기 등 모든 구성 요소의 목록을 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_fulltext_catalog_components  
```  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**전체 텍스트 카탈로그 이름**|**int**|전체 텍스트 카탈로그의 이름입니다.|  
|**전체 텍스트 카탈로그 id**|**sysname**|전체 텍스트 카탈로그의 ID입니다.|  
|**componenttype**|**sysname**|구성 요소의 유형입니다. 다음 중 하나일 수 있습니다.<br /><br /> Assert<br /><br /> 프로토콜 처리기<br /><br /> 단어 분리기|  
|**componentname**|**sysname**|구성 요소의 이름입니다.|  
|**clsid**|**uniqueidentifier**|구성 요소의 클래스 식별자입니다.|  
|**fullpath**|**nvarchar(256)**|구성 요소 위치에 대한 경로입니다.<br /><br /> NULL = 호출자의 멤버가 아닌 **serveradmin** 고정된 서버 역할입니다.|  
|**version**|**nvarchar(30)**|구성 요소 버전입니다.|  
|**manufacturer**|**sysname**|구성 요소 제조업체의 이름입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [전체 텍스트 검색과 의미 체계 검색 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [sys.fulltext_catalogs&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [sp_help_fulltext_system_components &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)  
  
  
