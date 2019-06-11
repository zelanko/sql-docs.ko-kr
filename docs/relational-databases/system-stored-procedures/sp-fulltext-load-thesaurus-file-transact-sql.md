---
title: sp_fulltext_load_thesaurus_file (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_load_thesaurus_file
- sp_fulltext_load_thesaurus_file_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_load_thesaurus_file
- full-text indexes [SQL Server], thesaurus files
- thesaurus [full-text search], editing
ms.assetid: 73a309c3-6d22-42dc-a6fe-8a63747aa2e4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c0857066ba5f8f57a5a6d088a4f37d69315225ea
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822766"
---
# <a name="spfulltextloadthesaurusfile-transact-sql"></a>sp_fulltext_load_thesaurus_file(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버 인스턴스에서 LCID가 지정된 언어에 해당하는 동의어 사전 파일의 데이터를 구문 분석하고 로드하게 합니다. 이 저장 프로시저는 동의어 사전 파일을 업데이트한 후에 유용합니다. 실행 **sp_fulltext_load_thesaurus_file** 지정된 된 LCID의 동의어 사전 파일을 사용 하는 전체 텍스트 쿼리의 다시 컴파일을 유발 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sys.sp_fulltext_load_thesaurus_file lcid [ , @loadOnlyIfNotLoaded  = action ]   
```  
  
## <a name="arguments"></a>인수  
 *lcid*  
 동의어 사전 XML 정의를 로드할 언어의 LCID(로캘 ID)를 매핑하는 정수입니다. 서버 인스턴스에서 사용할 수 있는 언어의 Lcid를 가져오려면 합니다 [sys.fulltext_languages &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md) 카탈로그 뷰.  
  
 **@loadOnlyIfNotLoaded**  = *action*  
 동의어 사전 파일이 이미 로드된 경우에도 내부 동의어 사전 테이블로 로드되는지 여부를 지정합니다. *작업* 중 하나입니다.  
  
|값|정의|  
|-----------|----------------|  
|**0**|이미 로드되었는지 여부와 관계없이 동의어 사전 파일을 로드합니다. 기본적으로 이것이 **sp_fulltext_load_thesaurus_file**합니다.|  
|1|아직 로드되지 않은 경우에만 동의어 사전 파일을 로드합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 동의어 사전 파일은 해당 동의어 사전을 사용하는 전체 텍스트 쿼리에 의해 자동으로 로드됩니다. 전체 텍스트 쿼리에 미치는이 첫 번째 성능 영향을 방지 하려면를 실행 하는 권장 **sp_fulltext_load_thesaurus_file**합니다.  
  
 사용 하 여 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)'**update_languages**' 전체 텍스트 검색에 등록 된 언어 목록을 업데이트 합니다.  
  
## <a name="permissions"></a>사용 권한  
 구성원만 합니다 **sysadmin** 고정된 서버 역할 또는 시스템 관리자를 실행할 수는 **sp_fulltext_load_thesaurus_file** 저장 프로시저입니다.  
  
 동의어 사전 파일은 시스템 관리자만 업데이트, 수정 또는 삭제할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-load-a-thesaurus-file-even-if-it-is-already-loaded"></a>1. 이미 로드되어 있더라도 동의어 사전 파일 로드  
 다음 예에서는 영어 동의어 사전 파일을 구문 분석하고 로드합니다.  
  
```sql
EXEC sys.sp_fulltext_load_thesaurus_file 1033;
```  
  
### <a name="b-load-a-thesaurus-file-only-if-it-is-not-yet-loaded"></a>2. 아직 로드되지 않은 경우에만 동의어 사전 파일 로드  
 다음 예에서는 아직 로드되지 않은 아랍어 동의어 사전 파일을 구문 분석하고 로드합니다.  
  
```sql
EXEC sys.sp_fulltext_load_thesaurus_file 1025, @loadOnlyIfNotLoaded = 1;
```  

## <a name="see-also"></a>관련 항목

[FULLTEXTSERVICEPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)  
[시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
[전체 텍스트 검색에 사용할 동의어 사전 파일 구성 및 관리](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)
