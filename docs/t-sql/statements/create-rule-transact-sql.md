---
title: "규칙 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f1893007dd699ffb002884a153ac72fa90fcd103
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-rule-transact-sql"></a>CREATE RULE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  규칙이라는 개체를 만듭니다. 열 또는 별칭 데이터 형식에 바인딩된 경우 규칙은 해당 열에 삽입할 수 있는 값을 지정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 CHECK 제약 조건을 사용하는 것이 좋습니다. CHECK 제약 조건은 CREATE TABLE 또는 ALTER TABLE의 CHECK 키워드를 사용하여 생성됩니다. 자세한 내용은 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)을 참조하세요.  
  
 열 또는 별칭 데이터 형식에는 단 하나의 규칙만 바인딩할 수 있습니다. 그러나 열에는 규칙과 한 개 이상의 CHECK 제약 조건이 모두 연결될 수 있습니다. 이 경우 모든 제한 사항이 평가됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE RULE [ schema_name . ] rule_name   
AS condition_expression  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *schema_name*  
 규칙이 속한 스키마의 이름입니다.  
  
 *rule_name*  
 새로운 규칙의 이름입니다. 규칙 이름에 대 한 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다. 규칙 소유자 이름은 지정하지 않아도 됩니다.  
  
 *condition_expression*  
 규칙을 정의하는 하나 이상의 조건입니다. 규칙은 WHERE 절에서 임의의 유효한 식이 될 수 있으며 산술 연산자, 관계형 연산자 및 조건자(예: IN, LIKE, BETWEEN) 같은 요소를 포함할 수도 있습니다. 규칙은 열 또는 기타 데이터베이스 개체를 참조할 수 없습니다. 데이터베이스 개체를 참조하지 않는 기본 제공 함수는 포함할 수 있습니다. 사용자 정의 함수는 사용할 수 없습니다.  
  
 *condition_expression* 하나의 변수를 포함 합니다. at 기호 (**@**) 각 지역 변수 앞에 옵니다. 식은 UPDATE 또는 INSERT 문과 함께 입력된 값을 참조합니다. 모든 이름 또는 기호 값을 나타내는 규칙을 만들 때 사용할 수 있지만 첫 번째 문자 여야는 at 기호 (**@**).  
  
> [!NOTE]  
>  별칭 데이터 형식을 사용하는 식에는 규칙을 만들지 않습니다. 별칭 데이터 형식을 사용하는 식에 규칙을 만들 수 있더라도 열이나 별칭 데이터 형식에 규칙을 바인딩하면 식이 참조될 때 컴파일되지 않습니다.  
  
## <a name="remarks"></a>주의  
 CREATE RULE을 다른 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문과 함께 하나의 일괄 처리에서 사용할 수 없습니다. 규칙은 규칙이 작성되는 시점에 이미 데이터베이스에 있는 데이터에는 적용되지 않으며 시스템 데이터 형식에 바인딩할 수 없습니다.  
  
 규칙은 현재 데이터베이스에서만 만들 수 있습니다. 규칙을 만든 후에 실행 **sp_bindrule** 열 또는 별칭 데이터 형식에 규칙을 바인딩할 합니다. 규칙은 반드시 열 데이터 형식과 호환되어야 합니다. 예를 들어 "@value LIKE는 %"는 숫자 열에 대 한 규칙으로 사용할 수 없습니다. 규칙에 바인딩할 수 없습니다는 **텍스트**, **ntext**, **이미지**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, CLR 사용자 정의 형식 또는 **타임 스탬프**열입니다. 계산 열에 규칙을 바인딩할 수 없습니다.  
  
 문자 및 날짜 상수는 작은따옴표(')로 묶고 이진 상수는 앞에 0x를 붙여야 합니다. 바인딩된 열과 해당 규칙이 호환되지 않는 경우에는 규칙을 바인딩할 때가 아니라 값을 삽입할 때 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 오류 메시지를 반환합니다.  
  
 별칭 데이터 형식에 바인딩된 규칙은 별칭 데이터 형식의 데이터베이스 열을 업데이트하거나 그 안에 값을 삽입하려고 시도할 때만 활성화됩니다. 규칙은 변수를 테스트하지 않으므로 동일한 데이터 형식의 열에 바인딩된 규칙에 의해 거부될 수 있는 별칭 데이터 형식 변수에는 값을 할당하지 마십시오.  
  
 규칙에 대 한 보고서를 가져오려면 **sp_help**합니다. 실행 규칙의 텍스트를 표시 하려면 **sp_helptext** 규칙 이름을 매개 변수로 사용 합니다. 규칙의 이름을 바꾸려면 사용 **sp_rename**합니다.  
  
 이름이 같은 새 인덱스를 만들면 하 고 규칙의 바인딩을 해제 해야 하기 전에 DROP RULE을 사용 하 여 규칙을 삭제 해야 **sp_unbindrule** 중단 되기 전에 합니다. 열에서 규칙 바인딩 해제를 사용 하 여 **sp_unbindrule**합니다.  
  
 이전 규칙의 바인딩을 해제하지 않고도 열 또는 데이터 형식에 새 규칙을 바인딩할 수 있습니다. 새 규칙은 이전 규칙을 덮어씁니다. 열에 바인딩된 규칙은 별칭 데이터 형식에 바인딩된 규칙보다 항상 우선합니다. 열에 규칙을 바인딩하면 해당 열의 별칭 데이터 형식에 이미 바인딩된 규칙이 대체됩니다. 그러나 데이터 형식에 규칙을 바인딩하면 해당 별칭 데이터 형식의 열에 바인딩된 규칙은 대체되지 않습니다. 다음 표에서는 규칙이 이미 있는 별칭 데이터 형식과 열에 규칙을 바인딩할 때 적용되는 선행 규칙을 보여 줍니다.  
  
|새 규칙이 바인딩되는 대상|이전 규칙이 바인딩된 대상이<br /><br /> 별칭 데이터 형식인 경우|이전 규칙이 바인딩된 대상이<br /><br /> 열|  
|-----------------------|-------------------------------------------|----------------------------------|  
|별칭 데이터 형식|이전 규칙이 대체됨|변경 내용 없음|  
|열|이전 규칙이 대체됨|이전 규칙이 대체됨|  
  
 열에 기본값과 연결된 규칙이 모두 있는 경우에는 해당 기본값이 규칙에 의해 정의된 도메인 내에 있어야 합니다. 규칙과 충돌하는 기본값은 삽입할 수 없습니다. SQL Server 데이터베이스 엔진에서는 이러한 기본값을 삽입하려고 할 때마다 오류 메시지를 생성합니다.  
  
## <a name="permissions"></a>Permissions  
 CREATE RULE을 실행하려면 최소한 사용자는 현재 데이터베이스의 CREATE RULE 권한 및 규칙이 생성되는 스키마에 대한 ALTER 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-rule-with-a-range"></a>1. 범위가 있는 규칙 만들기  
 다음 예에서는 규칙이 바인딩된 열에 삽입되는 정수의 범위를 제한하는 규칙을 만듭니다.  
  
```  
CREATE RULE range_rule  
AS   
@range>= $1000 AND @range <$20000;  
```  
  
### <a name="b-creating-a-rule-with-a-list"></a>2. 목록이 있는 규칙 만들기  
 다음 예에서는 해당 규칙이 바인딩된 열에 입력하는 실제 값을 규칙에 나열된 값으로 제한하는 규칙을 만듭니다.  
  
```  
CREATE RULE list_rule  
AS   
@list IN ('1389', '0736', '0877');  
```  
  
### <a name="c-creating-a-rule-with-a-pattern"></a>3. 패턴이 있는 규칙 만들기  
 다음 예에서는 하이픈(`-`) 다음에 임의의 두 문자, 임의의 문자 수(또는 0개 문자) 및 `0`부터 `9`까지의 정수로 끝나는 패턴의 규칙을 만듭니다.  
  
```  
CREATE RULE pattern_rule   
AS  
@value LIKE '__-%[0-9]'  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE DEFAULT&#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [기본 &#40; 삭제 Transact SQL &#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [DROP 규칙 &#40; Transact SQL &#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [sp_bindrule &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindrule &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

