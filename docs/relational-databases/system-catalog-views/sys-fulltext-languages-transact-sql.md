---
title: sys.fulltext_languages (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_languages
- sys.fulltext_languages_TSQL
- fulltext_languages
- fulltext_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- languages [full-text search]
- sys.fulltext_languages catalog view
ms.assetid: 2ed6b53d-1cf2-4763-9d58-36ea24a610ef
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0aa04b9a4b90b470ca3cc6df4a8f5cf62134027c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68220501"
---
# <a name="sysfulltextlanguages-transact-sql"></a>sys.fulltext_languages(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  이 카탈로그 뷰는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 단어 분리기가 등록된 언어당 한 개의 행을 포함합니다. 각 행에는 LCID 및 언어의 이름을 표시합니다. 언어, 다른 언어 리소스 형태소 분석기, 의미 없는 단어 (중지 단어) 및 동의어 사전 파일 수에 대 한 단어 분리기가 등록 하는 경우 전체 텍스트 인덱싱/쿼리 작업에 사용할 수 있습니다. 변수의 **이름을** 또는 **lcid** 전체 텍스트 쿼리 및 전체 텍스트 인덱스를 지정할 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다.  
   
|Column|데이터 형식|설명|  
|------------|---------------|-----------------|  
|**lcid**|**int**|해당 언어의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows LCID(로캘 ID)입니다.|  
|**name**|**sysname**|별칭 값 이거나 [sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 의 값에 해당 하 **lcid** 또는 숫자로 된 LCID의 문자열 표현입니다.|  
  
## <a name="values-returned-for-default-languages"></a>기본 언어에 대해 반환되는 값  
 다음 표에서는 기본적으로 단어 분리기가 등록되는 언어의 값을 보여 줍니다.  
  
|언어|LCID|  
|--------------|----------|  
|아랍어|1025|  
|벵골어 (인도)|1093|  
|영어(영국)|2057|  
|불가리아어|1026|  
|카탈로니아어|1027|  
|중국어(홍콩 특별 행정구, 중국)|3076|  
|중국어 (마카오 특별 행정구)|5124|  
|중국어 (싱가포르)|4100|  
|크로아티아어|1050|  
|체코어|1029|  
|덴마크어|1030|  
|네덜란드어|1043|  
|영어|1033|  
|프랑스어|1036|  
|독일어|1031|  
|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 그리스어|1032|  
|구자라트어|1095|  
|히브리어|1037|  
|힌디어|1081|  
|아이슬란드어|1039|  
|인도네시아어|1057|  
|이탈리아어|1040|  
|일본어|1041|  
|칸나다어|1099|  
|한국어|1042|  
|라트비아어|1062|  
|리투아니아어|1063|  
|말레이어 - 말레이시아|1086|  
|말라얄람어|1100|  
|마라티어|1102|  
|중립|0|  
|노르웨이어(복말)|1044|  
|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 폴란드어|1045|  
|포르투갈어(브라질)|1046|  
|포르투갈어(포르투갈)|2070|  
|펀잡어|1094|  
|루마니아어|1048|  
|러시아어|1049|  
|세르비아어(키릴 자모)|3098|  
|세르비아어(라틴 문자)|2074|  
|중국어(간체)|2052|  
|슬로바키아어|1051|  
|슬로베니아어|1060|  
|스페인어|3082|  
|스웨덴어|1053|  
|타밀어|1097|  
|텔루구어|1098|  
|태국어|1054|  
|중국어(번체)|1028|  
|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 터키어|1055|  
|우크라이나어|1058|  
|우르두어|1056|  
|베트남어|1066|  
  
## <a name="remarks"></a>설명  
 전체 텍스트 검색에 등록 된 언어 목록을 업데이트 하려면 사용 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)'**update_languages**'.  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [sp_fulltext_load_thesaurus_file &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)   
 [sp_fulltext_service&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [구성 및 전체 텍스트 검색 동의어 사전 파일 관리](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [전체 텍스트 검색 업그레이드](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
