---
title: sp_help_fulltext_catalog_components (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6fae0542a38a215d79228674fa6b2a9fbe4b9eb7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728197"
---
# <a name="sp_help_fulltext_catalog_components-transact-sql"></a>sp_help_fulltext_catalog_components(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스의 모든 전체 텍스트 카탈로그에 사용된 필터, 단어 분리기, 프로토콜 처리기 등 모든 구성 요소의 목록을 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_fulltext_catalog_components  
```  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**전체 텍스트 카탈로그 이름**|**int**|전체 텍스트 카탈로그의 이름입니다.|  
|**전체 텍스트 카탈로그 id**|**sysname**|전체 텍스트 카탈로그의 ID입니다.|  
|**componenttype**|**sysname**|구성 요소의 유형입니다. 다음 중 하나<br /><br /> Assert<br /><br /> 프로토콜 처리기<br /><br /> 단어 분리기|  
|**componentname**|**sysname**|구성 요소의 이름입니다.|  
|**가**|**uniqueidentifier**|구성 요소의 클래스 식별자입니다.|  
|**fullpath**|**nvarchar(256)**|구성 요소 위치에 대한 경로입니다.<br /><br /> NULL = 호출자가 **serveradmin** 고정 서버 역할의 멤버가 아닙니다.|  
|**version**|**nvarchar(30)**|구성 요소 버전입니다.|  
|**manufacturer**|**sysname**|구성 요소 제조업체의 이름입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;전체 텍스트 검색 및 의미 체계 검색 저장 프로시저](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [fulltext_catalogs &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [Transact-sql&#41;sp_help_fulltext_system_components &#40;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)  
  
  
