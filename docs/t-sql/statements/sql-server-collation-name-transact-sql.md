---
title: SQL Server Collation Name(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], SQL collations
- SQL collations
- names [SQL Server], collations
ms.assetid: 56483d24-add7-483d-9b96-c6fda460ddbc
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 765f825a690af65ec4740975cc21c5364d133bb5
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211402"
---
# <a name="sql-server-collation-name-transact-sql"></a>SQL Server 데이터 정렬 이름(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬의 데이터 정렬 이름을 지정하는 단일 문자열입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 Windows 데이터 정렬을 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 Windows 데이터 정렬을 지원하기 전에 개발된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬이라는 제한된 수(<80)의 데이터 정렬도 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬은 이전 버전과의 호환성을 위해 계속 지원되지만 새로운 개발 작업에 사용해서는 안 됩니다. Windows 데이터 정렬에 대한 자세한 내용은 [Windows Collation Name &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)을 참조하세요.  
  
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
  
 **Pref**  
 대문자 우선을 지정합니다. 비교에서 대소문자를 구분하더라도 다른 차이가 없는 경우 대문자가 소문자보다 먼저 정렬됩니다.  
  
 *Codepage*  
 데이터 정렬에 사용되는 코드 페이지를 표시하는 1 - 4자리 숫자를 지정합니다. **CP1**은 코드 페이지 1252를 지정하며 다른 모든 코드 페이지에 대해서는 완전한 코드 페이지 번호를 지정합니다. 예를 들어 **CP1251**은 코드 페이지 1251을 지정하며 **CP850**은 코드 페이지 850을 지정합니다.  
  
 *CaseSensitivity*  
 **CI**는 대/소문자를 구분하지 않도록 지정하고 **CS**는 대/소문자를 구분하도록 지정합니다.  
  
 *AccentSensitivity*  
 **AI**는 악센트를 구분하지 않도록 지정하고 **AS**는 악센트를 구분하도록 지정합니다.  
  
 **BIN**  
 사용할 이진 정렬 순서를 지정합니다.  
  
## <a name="remarks"></a>Remarks  
 서버에서 지원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬을 나열하려면 다음 쿼리를 실행합니다.  
  
```  
SELECT * FROM sys.fn_helpcollations()   
WHERE name LIKE 'SQL%';  
```  

> [!NOTE]
>  정렬 순서 ID 80의 경우 코드 페이지 1250과 이진 순서를 가진 Window 데이터 정렬을 사용하세요. 예를 들어 다음과 같이 사용할 수 있습니다. Albanian_BIN, Croatian_BIN, Czech_BIN, Romanian_BIN, Slovak_BIN, Slovenian_BIN 등이 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [상수&#40;Transact-SQL&#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlserver)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)   
 [sys.fn_helpcollations&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)  
  
  
