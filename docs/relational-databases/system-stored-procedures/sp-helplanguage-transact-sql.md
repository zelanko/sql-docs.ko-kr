---
title: sp_helplanguage (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d46e178fc1872a84bb573f16629803c59f2fb6c6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68122508"
---
# <a name="sp_helplanguage-transact-sql"></a>sp_helplanguage(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 특정 대체 언어 또는 모든 언어에 관한 정보를 보고합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helplanguage [ [ @language = ] 'language' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @language = ] 'language'`정보를 표시할 대체 언어의 이름입니다. *language* 는 **sysname**이며 기본값은 NULL입니다. *Language* 를 지정 하면 지정 된 언어에 대 한 정보가 반환 됩니다. Language를 지정 하지 않으면 **sys.syslanguages** 호환성 보기의 모든 언어에 대 한 정보가 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**langid**|**smallint**|언어 ID입니다.|  
|**dateformat**|**nchar (3)**|날짜의 형식입니다.|  
|**datefirst**|**tinyint**|첫 번째 요일: 월요일의 경우 1, 화요일의 경우 2, 일요일은 7까지입니다.|  
|**업그레이드할**|**int**|이 언어에 대한 최신 업그레이드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전입니다.|  
|**name**|**sysname**|언어 이름입니다.|  
|**앤티앨리어스**|**sysname**|언어의 대체 이름입니다.|  
|**개월**|**nvarchar (372)**|월 이름입니다.|  
|**shortmonths**|**nvarchar (132)**|월의 짧은 이름입니다.|  
|**일별로**|**nvarchar (217)**|요일 이름입니다.|  
|**lcid**|**int**|언어의 Windows 로캘 ID입니다.|  
|**msglangid**|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]메시지 그룹 ID입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-information-about-a-single-language"></a>A. 단일 언어에 관한 정보 반환  
 다음 예에서는 대체 언어 `French`에 관한 정보를 표시합니다.  
  
```  
sp_helplanguage French;  
```  
  
### <a name="b-returning-information-about-all-languages"></a>B. 모든 언어에 관한 정보 반환  
 다음 예에서는 설치된 모든 대체 언어에 관한 정보를 표시합니다.  
  
```  
sp_helplanguage;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [@@LANGUAGE&#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [SET LANGUAGE&#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
