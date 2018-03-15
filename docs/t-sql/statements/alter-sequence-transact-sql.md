---
title: ALTER SEQUENCE(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/08/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SEQUENCE_TSQL
- ALTER SEQUENCE
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, altering
- ALTER SEQUENCE statement
ms.assetid: decc0760-029e-4baf-96c9-4a64073df1c2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 66960ed0ae27cb7ecbe2d39d0e30d1ec12dcc3cb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="alter-sequence-transact-sql"></a>ALTER SEQUENCE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  기존 시퀀스 개체의 인수를 수정합니다. **CACHE** 옵션을 사용하여 시퀀스를 만든 경우 시퀀스를 변경하면 캐시가 다시 생성됩니다.  
  
 시퀀스 개체는 [CREATE SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md) 문을 사용하여 만듭니다. 시퀀스는 정수 값이며, 정수를 반환하는 데이터 형식일 수 있습니다. 데이터 형식은 ALTER SEQUENCE 문을 사용하여 변경할 수 없습니다. 데이터 형식을 변경하려면 시퀀스 개체를 삭제하고 새로 만들어야 합니다.  
  
 시퀀스는 사양에 따라 일련의 숫자 값을 생성하는 사용자 정의 스키마 바운드 개체입니다. NEXT VALUE FOR 함수를 호출하면 시퀀스에서 새 값이 생성됩니다. 여러 시퀀스 번호를 한 번에 가져오려면 **sp_sequence_get_range** 를 사용합니다. CREATE SEQUENCE, **sp_sequence_get_range** 및 NEXT VALUE FOR 함수를 함께 사용하는 시나리오에 대한 자세한 내용은 [시퀀스 번호](../../relational-databases/sequence-numbers/sequence-numbers.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER SEQUENCE [schema_name. ] sequence_name  
    [ RESTART [ WITH <constant> ] ]  
    [ INCREMENT BY <constant> ]  
    [ { MINVALUE <constant> } | { NO MINVALUE } ]  
    [ { MAXVALUE <constant> } | { NO MAXVALUE } ]  
    [ CYCLE | { NO CYCLE } ]  
    [ { CACHE [ <constant> ] } | { NO CACHE } ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *sequence_name*  
 데이터베이스에서 시퀀스를 식별하는 고유 이름을 지정합니다. 형식은 **sysname**입니다.  
  
 RESTART [ WITH \<constant> ]  
 시퀀스 개체가 반환할 다음 값입니다. RESTART WITH 값은 시퀀스 개체의 최대값보다 작거나 같고 최소값보다 크거나 같아야 합니다. WITH 값을 생략하면 시퀀스 번호 매기기가 원래 CREATE SEQUENCE 옵션을 기반으로 다시 시작됩니다.  
  
 INCREMENT BY \<constant>  
 각각의 NEXT VALUE FOR 함수 호출에 대한 시퀀스 개체의 기준 값을 더하거나 빼는(음수인 경우) 데 사용되는 값입니다. 증가값이 음수이면 시퀀스 개체가 내림차순이고, 그렇지 않으면 오름차순입니다. 증가값은 0일 수 없습니다.  
  
 [ MINVALUE \<constant> | NO MINVALUE ]  
 시퀀스 개체의 경계를 지정합니다. NO MINVALUE를 지정하지 않으면 시퀀스 데이터 형식의 가능한 최소값이 사용됩니다.  
  
 [ MAXVALUE \<constant> | NO MAXVALUE  
 시퀀스 개체의 경계를 지정합니다. NO MAXVALUE를 지정하지 않으면 시퀀스 데이터 형식의 가능한 최대값이 사용됩니다.  
  
 [ CYCLE | NO CYCLE ]  
 이 속성은 시퀀스 개체를 최소값 또는 최대값(내림차순 시퀀스 개체의 경우)에서 다시 시작해야 하는지, 아니면 최소값 또는 최대값을 초과하는 경우 예외를 발생시켜야 하는지를 지정합니다.  
  
> [!NOTE]  
>  순환된 후의 다음 값은 시퀀스의 START VALUE가 아니라 최소값 또는 최대값입니다.  
  
 [ CACHE [\<constant> ] | NO CACHE ]  
 생성된 값을 시스템 테이블에 유지하는 데 필요한 IO 수를 최소화하여 시퀀스 개체를 사용하는 응용 프로그램의 성능을 향상시킵니다.  
  
 캐시 동작에 대한 자세한 내용은 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 시퀀스를 만드는 방법 및 시퀀스 캐시를 관리하는 방법은 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)를 참조하세요.  
  
 오름차순 시퀀스의 MINVALUE와 내림차순 시퀀스의 MAXVALUE는 시퀀스의 START WITH 값이 허용되지 않는 값으로 변경할 수 없습니다. 오름차순 시퀀스의 MINVALUE를 START WITH 값보다 큰 수로 변경하거나 내림차순 시퀀스의 MAXVALUE를 START WITH 값보다 작은 수로 변경하려면 RESTART WITH 인수를 포함하여 최소값과 최대값 사이의 원하는 위치에서 시퀀스를 다시 시작합니다.  
  
## <a name="metadata"></a>메타데이터  
 시퀀스에 대한 자세한 내용을 보려면 [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)를 쿼리하십시오.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 시퀀스에 대한 **ALTER** 권한 또는 스키마에 대한 **ALTER** 권한이 필요합니다. 시퀀스에 대한 **ALTER** 권한을 부여하려면 다음 형식으로 **ALTER ON OBJECT**를 사용합니다.  
  
```  
GRANT ALTER ON OBJECT::Test.TinySeq TO [AdventureWorks\Larry]  
```  
  
 **ALTER AUTHORIZATION** 문을 사용하여 시퀀스 개체의 소유권을 이전할 수 있습니다.  
  
### <a name="audit"></a>감사  
 **ALTER SEQUENCE**를 감사하려면 **SCHEMA_OBJECT_CHANGE_GROUP**을 모니터링합니다.  
  
## <a name="examples"></a>예  
 시퀀스를 만들고 **NEXT VALUE FOR** 함수를 사용하여 시퀀스 번호를 생성하는 방법에 대한 예는 [시퀀스 번호](../../relational-databases/sequence-numbers/sequence-numbers.md)을 참조하세요.  
  
### <a name="a-altering-a-sequence"></a>1. 시퀀스 변경  
 다음 예에서는 범위가 0에서 255인 **int** 데이터 형식을 사용하여 Test라는 스키마와 TestSeq라는 시퀀스를 만듭니다. 시퀀스는 125부터 시작하여 번호가 생성될 때마다 25씩 증가합니다. 시퀀스가 순환하도록 구성되었기 때문에 값이 최대값 200을 초과하는 경우 최소값 100에서 시퀀스가 다시 시작됩니다.  
  
```  
CREATE SCHEMA Test ;  
GO  
  
CREATE SEQUENCE Test.TestSeq  
    AS int   
    START WITH 125  
    INCREMENT BY 25  
    MINVALUE 100  
    MAXVALUE 200  
    CYCLE  
    CACHE 3  
;  
GO  
```  
  
 다음 예에서는 0에서 255 사이의 범위로 TestSeq 시퀀스를 변경합니다. 시퀀스는 100부터 번호가 매겨지도록 다시 시작되며 번호가 생성될 때마다 50씩 증가합니다.  
  
```  
ALTER SEQUENCE Test. TestSeq  
    RESTART WITH 100  
    INCREMENT BY 50  
    MINVALUE 50  
    MAXVALUE 200  
    NO CYCLE  
    NO CACHE  
;  
GO  
```  
  
 시퀀스가 순환하지 않기 때문에 200을 초과하는 경우 **NEXT VALUE FOR** 함수에서 오류가 발생합니다.  
  
### <a name="b-restarting-a-sequence"></a>2. 시퀀스 다시 시작  
 다음 예에서는 CountBy1이라는 시퀀스를 만듭니다. 이 시퀀스는 기본값을 사용합니다.  
  
```  
CREATE SEQUENCE Test.CountBy1 ;  
```  
  
 시퀀스 값을 생성하기 위해 다음 문을 실행합니다.  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1  
```  
  
 **bigint** 데이터 형식의 가능한 최소값인 -9,223,372,036,854,775,808이 반환되었습니다. 시퀀스를 1부터 시작하려고 했지만 시퀀스를 만들 때 **START WITH** 절을 사용하지 않았기 때문에 이러한 결과가 발생한 것입니다. 이 오류를 해결하려면 다음 문을 실행합니다.  
  
```  
ALTER SEQUENCE Test.CountBy1 RESTART WITH 1 ;  
```  
  
 그런 다음 다시 다음 문을 실행하여 시퀀스 번호를 생성합니다.  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1;  
```  
  
 예상대로 1이 반환됩니다.  
  
 CountBy1 시퀀스는 기본값 NO CYCLE을 사용하여 만들었기 때문에 9,223,372,036,854,775,807 번호를 생성한 후에 작동을 중지합니다. 이후에 시퀀스 개체를 호출하면 11728 오류가 반환됩니다. 다음 문은 시퀀스 개체를 순환하도록 변경하고 캐시를 20으로 설정합니다.  
  
```  
ALTER SEQUENCE Test.CountBy1  
    CYCLE  
    CACHE 20 ;  
  
```  
  
 이제 9,223,372,036,854,775,807에 도달한 경우 시퀀스 개체는 데이터 형식의 최소값인 -9,223,372,036,854,775,808부터 순환합니다.  
  
 **bigint** 데이터 형식은 한 번 사용될 때마다 8바이트를 사용합니다. 4바이트를 사용하는 **int** 데이터 형식으로도 충분하지만 시퀀스 개체의 데이터 형식은 변경할 수 없습니다. **int** 데이터 형식으로 변경하려면 시퀀스 개체를 삭제하고 올바른 데이터 형식으로 다시 만들어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [시퀀스 번호](../../relational-databases/sequence-numbers/sequence-numbers.md)   
 [sp_sequence_get_range &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)  
  
  
