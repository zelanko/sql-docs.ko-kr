---
title: SET DATEFORMAT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATEFORMAT
- SET DATEFORMAT
- SET_DATEFORMAT_TSQL
- DATEFORMAT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], formats
- dates [SQL Server], ordering date parts
- SET DATEFORMAT option [SQL Server]
- DATEFORMAT option [SQL Server]
- date and time [SQL Server], SET DATEFORMAT
- options [SQL Server], date
- date and time [SQL Server], DATEFORMAT
- dateparts [SQL Server], dateformat
ms.assetid: da217878-7ec4-477e-aa13-604073c948f8
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9ba990b7438201d459be8052bd119f5689b9af88
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634359"
---
# <a name="set-dateformat-transact-sql"></a>SET DATEFORMAT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  날짜 문자열을 해석하기 위해 월, 일 및 연도 날짜 부분의 순서를 설정합니다. 이러한 문자열은 **date**, **smalldatetime**, **datetime**, **datetime2** 또는 **datetimeoffset** 형식입니다.  
  
 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 날짜 및 시간 데이터 형식 및 함수에 대한 개요는 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
SET DATEFORMAT { format | @format_var }   
```  
  
## <a name="arguments"></a>인수  
 *format* |  **@** _format_var_  
 날짜 부분의 순서입니다. 유효한 매개 변수는 **mdy**, **dmy**, **ymd**, **ydm**, **myd** 및 **dym**입니다. 유니코드나 유니코드로 변환된 DBCS(더블바이트 문자 집합) 중 하나가 될 수 있습니다. 미국 영어 기본값은 **mdy**입니다. 모든 지원 언어의 기본 DATEFORMAT에 대한 내용은 [sp_helplanguage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)를 참조하세요.  
  
## <a name="remarks"></a>설명  
 DATEFORMAT **ydm**은 **date**, **datetime2** 및 **datetimeoffset** 데이터 형식에 대해 지원되지 않습니다.  
  
 DATEFORMAT 설정은 문자열 형식에 따라 날짜 데이터 형식에 대해 문자열을 다르게 해석할 수 있습니다. 예를 들어 **datetime** 및 **smalldatetime** 해석은 **date**, **datetime2** 또는  **datetimeoffset**과 일치하지 않을 수 있습니다. DATEFORMAT은 문자열이 데이터베이스의 날짜 값으로 변환될 때 문자열의 해석에 영향을 줍니다. 날짜 데이터 형식 값의 표시나 데이터베이스 스토리지 형식에 영향을 주지 않습니다.  
  
 예를 들어 ISO 8601과 같은 일부 문자열 형식의 경우 DATEFORMAT 설정과 관계없이 해석됩니다.  
  
 SET DATEFORMAT 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
 SET DATEFORMAT은 [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)의 암시적 날짜 형식 설정보다 우선 적용됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예제는 동일한 `DATEFORMAT` 설정을 가진 세션의 입력으로 다른 날짜 문자열을 사용합니다.  
  
```sql
-- Set date format to day/month/year.  
SET DATEFORMAT dmy;  
GO  
DECLARE @datevar datetime2 = '31/12/2008 09:01:01.1234567';  
SELECT @datevar;  
GO  
-- Result: 2008-12-31 09:01:01.123  
SET DATEFORMAT dmy;  
GO  
DECLARE @datevar datetime2 = '12/31/2008 09:01:01.1234567';  
SELECT @datevar;  
GO  
-- Result: Msg 241: Conversion failed when converting date and/or time -- from character string.  
  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  

