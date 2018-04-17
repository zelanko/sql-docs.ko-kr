---
title: sp_helplanguage (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helplanguage
- sp_helplanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplanguage
- default languages
ms.assetid: 8c4651a5-7dbc-49c5-8691-dc72103c2dfa
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d5447f5cb5f41ab4c9a2dfa162e6ee04932c515c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sphelplanguage-transact-sql"></a>sp_helplanguage(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 특정 대체 언어 또는 모든 언어에 관한 정보를 보고합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helplanguage [ [ @language = ] 'language' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@language=** ] **'***언어***'**  
 정보를 표시할 대체 언어의 이름입니다. *언어* 은 **sysname**, 기본값은 NULL입니다. 경우 *언어* 가 지정 하면 지정된 된 언어에 대 한 정보가 반환 됩니다. 언어를 지정 하지 않으면 경우에서 모든 언어에 대 한 정보는 **sys.syslanguages** 호환성 보기 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**langid**|**smallint**|언어 ID입니다.|  
|**dateformat**|**nchar(3)**|날짜의 형식입니다.|  
|**datefirst**|**tinyint**|첫 번째 요일: 1은 월요일, 화요일, 7은 일요일까지에 대 한 2입니다.|  
|**업그레이드**|**int**|이 언어에 대한 최신 업그레이드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전입니다.|  
|**name**|**sysname**|언어 이름입니다.|  
|**alias**|**sysname**|언어의 대체 이름입니다.|  
|**월**|**nvarchar(372)**|월 이름입니다.|  
|**shortmonths**|**nvarchar(132)**|월의 짧은 이름입니다.|  
|**days**|**nvarchar(217)**|요일 이름입니다.|  
|**lcid**|**int**|언어의 Windows 로캘 ID입니다.|  
|**msglangid**|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메시지 그룹 ID입니다.|  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-information-about-a-single-language"></a>1. 단일 언어에 관한 정보 반환  
 다음 예에서는 대체 언어 `French`에 관한 정보를 표시합니다.  
  
```  
sp_helplanguage French;  
```  
  
### <a name="b-returning-information-about-all-languages"></a>2. 모든 언어에 관한 정보 반환  
 다음 예에서는 설치된 모든 대체 언어에 관한 정보를 표시합니다.  
  
```  
sp_helplanguage;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 엔진 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [@@LANGUAGE&#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [SET LANGUAGE&#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
