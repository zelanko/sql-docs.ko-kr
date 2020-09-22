---
description: CREATE RULE(Transact-SQL)
title: CREATE RULE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RULE_TSQL
- CREATE RULE
- CREATE_RULE_TSQL
- RULE
dev_langs:
- TSQL
helpviewer_keywords:
- list rules [SQL Server]
- unbinding rules
- pattern rules [SQL Server]
- range rules [SQL Server]
- alias data types [SQL Server], rules
- CREATE RULE statement
- reports [SQL Server], rules
- status information [SQL Server], rules
- rules [SQL Server], precedence
- binding rules [SQL Server]
- rules [SQL Server], creating
ms.assetid: b016a289-3a74-46b1-befc-a13183be51e4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e0b6c3ae3d269b8617d3d032c8aa2d947c211834
ms.sourcegitcommit: ac9feb0b10847b369b77f3c03f8200c86ee4f4e0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90688779"
---
# <a name="create-rule-transact-sql"></a>CREATE RULE(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  규칙이라는 개체를 만듭니다. 열 또는 별칭 데이터 형식에 바인딩된 경우 규칙은 해당 열에 삽입할 수 있는 값을 지정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 CHECK 제약 조건을 사용하는 것이 좋습니다. CHECK 제약 조건은 CREATE TABLE 또는 ALTER TABLE의 CHECK 키워드를 사용하여 생성됩니다. 자세한 내용은 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)을 참조하세요.  
  
 열 또는 별칭 데이터 형식에는 단 하나의 규칙만 바인딩할 수 있습니다. 그러나 열에는 규칙과 한 개 이상의 CHECK 제약 조건이 모두 연결될 수 있습니다. 이 경우 모든 제한 사항이 평가됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
CREATE RULE [ schema_name . ] rule_name   
AS condition_expression  
[ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *schema_name*  
 규칙이 속한 스키마의 이름입니다.  
  
 *rule_name*  
 새로운 규칙의 이름입니다. 규칙 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 적용되는 규칙을 준수해야 합니다. 규칙 소유자 이름은 지정하지 않아도 됩니다.  
  
 *condition_expression*  
 규칙을 정의하는 하나 이상의 조건입니다. 규칙은 WHERE 절에서 임의의 유효한 식이 될 수 있으며 산술 연산자, 관계형 연산자 및 조건자(예: IN, LIKE, BETWEEN) 같은 요소를 포함할 수도 있습니다. 규칙은 열 또는 기타 데이터베이스 개체를 참조할 수 없습니다. 데이터베이스 개체를 참조하지 않는 기본 제공 함수는 포함할 수 있습니다. 사용자 정의 함수는 사용할 수 없습니다.  
  
 *condition_expression*에는 하나의 변수가 포함됩니다. 각 지역 변수 앞에는 at 기호( **@** )가 붙습니다. 식은 UPDATE 또는 INSERT 문과 함께 입력된 값을 참조합니다. 규칙을 만들 때는 모든 이름 또는 기호를 사용하여 값을 나타낼 수 있으나 첫 번째 문자는 반드시 at 기호( **@** )를 사용해야 합니다.  
  
> [!NOTE]  
>  별칭 데이터 형식을 사용하는 식에는 규칙을 만들지 않습니다. 별칭 데이터 형식을 사용하는 식에 규칙을 만들 수 있더라도 열이나 별칭 데이터 형식에 규칙을 바인딩하면 식이 참조될 때 컴파일되지 않습니다.  
  
## <a name="remarks"></a>설명  
 CREATE RULE을 다른 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문과 함께 하나의 일괄 처리에서 사용할 수 없습니다. 규칙은 규칙이 작성되는 시점에 이미 데이터베이스에 있는 데이터에는 적용되지 않으며 시스템 데이터 형식에 바인딩할 수 없습니다.  
  
 규칙은 현재 데이터베이스에서만 만들 수 있습니다. 규칙을 만든 다음, **sp_bindrule**을 실행하여 열 또는 별칭 데이터 형식에 규칙을 바인딩합니다. 규칙은 반드시 열 데이터 형식과 호환되어야 합니다. 예를 들어 "\@value LIKE A%"는 숫자 열에 대한 규칙으로 사용할 수 없습니다. 규칙은 **text**, **ntext**, **image**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **xml**, CLR 사용자 정의 형식 또는 **timestamp** 열에 바인딩할 수 없습니다. 계산 열에 규칙을 바인딩할 수 없습니다.  
  
 문자 및 날짜 상수는 작은따옴표(')로 묶고 이진 상수는 앞에 0x를 붙여야 합니다. 바인딩된 열과 해당 규칙이 호환되지 않는 경우에는 규칙을 바인딩할 때가 아니라 값을 삽입할 때 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 오류 메시지를 반환합니다.  
  
 별칭 데이터 형식에 바인딩된 규칙은 별칭 데이터 형식의 데이터베이스 열을 업데이트하거나 그 안에 값을 삽입하려고 시도할 때만 활성화됩니다. 규칙은 변수를 테스트하지 않으므로 동일한 데이터 형식의 열에 바인딩된 규칙에 의해 거부될 수 있는 별칭 데이터 형식 변수에는 값을 할당하지 마십시오.  
  
 규칙에 대한 보고서를 만들려면 **sp_help**를 사용하십시오. 규칙 텍스트를 표시하려면 규칙 이름을 매개 변수로 사용하여 **sp_helptext**를 실행하십시오. 규칙의 이름을 바꾸려면 **sp_rename**을 사용하십시오.  
  
 이름이 같은 새 규칙을 만들려면 DROP RULE을 사용하여 규칙을 먼저 삭제해야 하며 삭제하기 전에 **sp_unbindrule**을 사용하여 규칙의 바인딩을 해제해야 합니다. 열에서 규칙의 바인딩을 해제하려면 **sp_unbindrule**을 사용하십시오.  
  
 이전 규칙의 바인딩을 해제하지 않고도 열 또는 데이터 형식에 새 규칙을 바인딩할 수 있습니다. 새 규칙은 이전 규칙을 덮어씁니다. 열에 바인딩된 규칙은 별칭 데이터 형식에 바인딩된 규칙보다 항상 우선합니다. 열에 규칙을 바인딩하면 해당 열의 별칭 데이터 형식에 이미 바인딩된 규칙이 대체됩니다. 그러나 데이터 형식에 규칙을 바인딩하면 해당 별칭 데이터 형식의 열에 바인딩된 규칙은 대체되지 않습니다. 다음 표에서는 규칙이 이미 있는 별칭 데이터 형식과 열에 규칙을 바인딩할 때 적용되는 선행 규칙을 보여 줍니다.  
  
|새 규칙이 바인딩되는 대상|이전 규칙이 바인딩된 대상이<br /><br /> 별칭 데이터 형식인 경우|이전 규칙이 바인딩된 대상이<br /><br /> 열|  
|-----------------------|-------------------------------------------|----------------------------------|  
|별칭 데이터 형식|이전 규칙이 대체됨|변경 내용 없음|  
|열|이전 규칙이 대체됨|이전 규칙이 대체됨|  
  
 열에 기본값과 연결된 규칙이 모두 있는 경우에는 해당 기본값이 규칙에 의해 정의된 도메인 내에 있어야 합니다. 규칙과 충돌하는 기본값은 삽입할 수 없습니다. SQL Server 데이터베이스 엔진에서는 이러한 기본값을 삽입하려고 할 때마다 오류 메시지를 생성합니다.  
  
## <a name="permissions"></a>사용 권한  
 CREATE RULE을 실행하려면 최소한 사용자는 현재 데이터베이스의 CREATE RULE 권한 및 규칙이 생성되는 스키마에 대한 ALTER 권한이 있어야 합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-creating-a-rule-with-a-range"></a>A. 범위가 있는 규칙 만들기  
 다음 예에서는 규칙이 바인딩된 열에 삽입되는 정수의 범위를 제한하는 규칙을 만듭니다.  
  
```sql  
CREATE RULE range_rule  
AS   
@range>= $1000 AND @range <$20000;  
```  
  
### <a name="b-creating-a-rule-with-a-list"></a>B. 목록이 있는 규칙 만들기  
 다음 예에서는 해당 규칙이 바인딩된 열에 입력하는 실제 값을 규칙에 나열된 값으로 제한하는 규칙을 만듭니다.  
  
```sql  
CREATE RULE list_rule  
AS   
@list IN ('1389', '0736', '0877');  
```  
  
### <a name="c-creating-a-rule-with-a-pattern"></a>C. 패턴이 있는 규칙 만들기  
 다음 예에서는 하이픈(`-`) 다음에 임의의 두 문자, 임의의 문자 수(또는 0개 문자) 및 `0`부터 `9`까지의 정수로 끝나는 패턴의 규칙을 만듭니다.  
  
```sql  
CREATE RULE pattern_rule   
AS  
@value LIKE '__-%[0-9]'  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE DEFAULT&#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [sp_bindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
