---
title: CREATE DEFAULT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_DEFAULT_TSQL
- CREATE DEFAULT
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], default
- default objects
- CREATE DEFAULT statement
- objects [SQL Server], creating
- DEFAULT definition
ms.assetid: 08475db4-7d90-486a-814c-01a99d783d41
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5116e561889fdd33912650a5daa5a773731f15d3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767159"
---
# <a name="create-default-transact-sql"></a>CREATE DEFAULT(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

기본값 개체를 만듭니다. 열이나 별칭 데이터 형식에 기본값을 바인딩하면 삽입 시 값을 명시적으로 제공하지 않을 경우 개체가 바인딩된 열(별칭 데이터 형식의 경우 모든 열)에 값이 삽입되도록 지정됩니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 ALTER TABLE 또는 CREATE TABLE의 DEFAULT 키워드를 사용하여 만든 기본 정의를 사용하십시오.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
CREATE DEFAULT [ schema_name . ] default_name   
AS constant_expression [ ; ]  
```  
  
## <a name="arguments"></a>인수  
*schema_name*  
 기본값이 속한 스키마의 이름입니다.  
  
*default_name*  
 기본값의 이름입니다. 기본값 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다. 기본 소유자 이름을 지정하는 것은 선택 사항입니다.  
  
*constant_expression*  
상수 값만 포함하는 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. 열 이름이나 다른 데이터베이스 개체의 이름을 포함할 수 없습니다. 별칭 데이터 형식을 포함한 식을 제외하고 모든 종류의 상수, 기본 제공 함수 및 수치 연산 식을 사용할 수 있습니다. 사용자 정의 함수는 사용할 수 없습니다. 문자와 날짜 상수는 작은따옴표( **'** )로 묶어야 하지만 통화, 정수 및 부동 소수점 상수에는 따옴표가 필요 없습니다. 이진 데이터는 0x로 시작해야 하고 통화 데이터는 달러 기호($)로 시작해야 합니다. 기본값은 열 데이터 형식과 호환이 가능해야 합니다.  
  
## <a name="remarks"></a>설명  
 현재 데이터베이스에서는 기본 이름만 만들 수 있습니다. 기본값 이름은 데이터베이스에서 스키마별로 고유해야 합니다. 기본값을 만들 경우 **sp_bindefault**를 사용하여 값을 열이나 별칭 데이터 형식에 바인딩합니다.  
  
 기본값이 바인딩될 열과 호환되지 않으면 기본값을 삽입하려고 할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 오류 메시지가 나타납니다. 예를 들어 N/A는 **numeric** 열의 기본값으로 사용할 수 없습니다.  
  
 기본값이 바인딩될 열에 비해 너무 길면 값이 잘립니다.  
  
 CREATE DEFAULT 문을 한 일괄 처리에서 다른 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문과 결합할 수 없습니다.  
  
 같은 이름을 가진 기본값을 새로 만들려면 먼저 기존 기본값을 삭제해야 합니다. 도한 기본값을 삭제하려면 먼저 **sp_unbindefault**를 실행하여 기본값을 바인딩 해제해야 합니다.  
  
 열에 기본값 및 연관된 규칙이 모두 있을 경우에는 해당 기본값이 규칙을 위반해서는 안 됩니다. 규칙을 위반하는 기본값은 삽입할 수 없으며 이러한 기본값을 삽입하려고 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 오류 메시지가 나타납니다.  
  
 열에 바인딩된 기본값은 다음과 같은 경우 삽입됩니다.  
  
-   값이 명시적으로 삽입되지 않은 경우  
  
-   INSERT에 DEFAULT VALUES 또는 DEFAULT 키워드를 사용하여 기본값이 삽입된 경우  
  
 열을 만들 때 NOT NULL을 지정하고 기본값을 만들지 않은 경우 해당 열에 값을 입력하지 않으면 오류 메시지가 나타납니다. 다음 표에서는 NULL 또는 NOT NULL로 정의된 열과 기본값의 유무에 따른 관계를 표시합니다. 다음 표의 항목이 결과를 보여 줍니다.  
  
|열 정의|입력 안 함, 기본값 없음|입력 안 함, 기본값 있음|NULL 입력, 기본값 없음|NULL 입력, 기본값 있음|  
|-----------------------|--------------------------|-----------------------|----------------------------|-------------------------|  
|**NULL**|NULL|기본값|NULL|NULL|  
|**NOT NULL**|Error|기본값|error|error|  
  
 기본값의 이름을 바꾸려면 **sp_rename**을 사용합니다. 기본값에 대한 보고서를 보려면 **sp_help**를 사용합니다.  
  
## <a name="permissions"></a>사용 권한  
 CREATE DEFAULT를 사용하려면 최소한 현재 데이터베이스에서 CREATE DEFAULT 권한과 기본값이 생성된 스키마에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-simple-character-default"></a>A. 단순한 문자 기본값 만들기  
 다음 예에서는 `unknown`이라는 문자 기본값을 만듭니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE DEFAULT phonedflt AS 'unknown';  
```  
  
### <a name="b-binding-a-default"></a>B. 기본값 바인딩  
 다음 예에서는 예 1에서 만든 기본값을 바인딩합니다. `Phone` 테이블의 `Contact` 열에 항목이 지정되어 있지 않을 때만 기본값이 적용됩니다. 
 
 > [!Note] 
 >  항목을 생략하는 것은 INSERT 문에 명시적으로 NULL을 지정하는 것과는 다릅니다.  
  
 `phonedflt`라는 기본값은 없으므로 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 실패하게 됩니다. 이 예는 설명을 돕기 위해 제공된 것입니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
sp_bindefault 'phonedflt', 'Person.PersonPhone.PhoneNumber';  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE RULE&#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [sp_bindefault&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindefault&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  
