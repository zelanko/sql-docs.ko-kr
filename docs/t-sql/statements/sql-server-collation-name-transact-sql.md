---
title: "SQL Server 데이터 정렬 이름 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], SQL collations
- SQL collations
- names [SQL Server], collations
ms.assetid: 56483d24-add7-483d-9b96-c6fda460ddbc
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fc7265f4efe0d790ab61e4e522af83d6b91b710a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-collation-name-transact-sql"></a>SQL Server 데이터 정렬 이름(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬의 데이터 정렬 이름을 지정하는 단일 문자열입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 Windows 데이터 정렬을 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 Windows 데이터 정렬을 지원하기 전에 개발된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬이라는 제한된 수(<80)의 데이터 정렬도 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬은 이전 버전과의 호환성을 위해 계속 지원되지만 새로운 개발 작업에 사용해서는 안 됩니다. Windows 데이터 정렬에 대 한 자세한 내용은 참조 하십시오. [Windows 데이터 정렬 이름 &#40; Transact SQL &#41; ](../../t-sql/statements/windows-collation-name-transact-sql.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
<SQL_collation_name> :: =   
SQL_SortRules[_Pref]_CPCodepage_<ComparisonStyle>  
  
<ComparisonStyle> ::=  
_CaseSensitivity_AccentSensitivity | _BIN  
```  
  
## <a name="arguments"></a>인수  
 *SortRules*  
 사전 정렬을 지정했을 때 정렬 규칙이 적용되는 알파벳 또는 언어를 나타내는 문자열입니다. 예를 들면 Latin1_General 또는 Polish 등이 있습니다.  
  
 **기본 설정**  
 대문자 우선을 지정합니다. 비교에서 대소문자를 구분하더라도 다른 차이가 없는 경우 대문자가 소문자보다 먼저 정렬됩니다.  
  
 *Codepage*  
 데이터 정렬에 사용되는 코드 페이지를 표시하는 1 - 4자리 숫자를 지정합니다. **CP1** 다른 모든 코드 페이지는 전체 코드 페이지 번호에 대 한 지정 된, 코드 페이지 1252 지정 합니다. 예를 들어 **CP1251** 코드 페이지 1251 지정 하 고 **CP850** 코드 페이지 850 지정 합니다.  
  
 *CaseSensitivity*  
 **CI** 지정 대/소문자 구분, **CS** 대/소문자 구분을 지정 합니다.  
  
 *AccentSensitivity*  
 **AI** 지정 악센트 구분 안 함, **AS** 악센트 구분을 지정 합니다.  
  
 **BIN**  
 사용할 이진 정렬 순서를 지정합니다.  
  
## <a name="remarks"></a>주의  
 서버에서 지원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬을 나열하려면 다음 쿼리를 실행합니다.  
  
```  
SELECT * FROM sys.fn_helpcollations()   
WHERE name LIKE 'SQL%';  
```  

>  [!NOTE]  
>  정렬 순서 ID 80에 대 한 코드 페이지 1250의 창 데이터 정렬 및 이진 순서 중 하나를 따르세요. 예를 들어: Albanian_BIN, Croatian_BIN, Czech_BIN, Romanian_BIN, Slovak_BIN, slovenian_bin 등이 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [상수 &#40; Transact SQL &#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [테이블 &#40; Transact SQL &#41;](../../t-sql/data-types/table-transact-sql.md)   
 [sys.fn_helpcollations&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)  
  
  

