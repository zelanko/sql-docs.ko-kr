---
title: "순서 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 04/11/2017
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
- SEQUENCE
- CREATE SEQUENCE
- SEQUENCE_TSQL
- CREATE_SEQUENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE SEQUENCE statement
- sequence number object, creating
- sequence object
- number, sequence
ms.assetid: 419f907b-8a72-4d6c-80cb-301df44c24c1
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 89a96d101c17f528b9ff14ca523e5dc41ada2f4c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-sequence-transact-sql"></a>CREATE SEQUENCE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  시퀀스 개체를 만들고 해당 속성을 지정합니다. 시퀀스는 시퀀스를 만들 때 사용된 사양에 따라 숫자 값의 시퀀스를 생성하는 사용자 정의 스키마 바운드 개체입니다. 숫자 값의 시퀀스는 정의된 간격에 따라 오름차순이나 내림차순으로 생성되며, 시퀀스가 모두 사용되면 다시 시작(순환)되도록 구성할 수 있습니다. ID 열과 달리 시퀀스는 특정 테이블과 연결되지 않습니다. 응용 프로그램에서는 시퀀스 개체를 참조하여 다음 값을 검색합니다. 시퀀스와 테이블 간의 관계는 응용 프로그램에서 제어합니다. 사용자 응용 프로그램에서는 시퀀스 개체를 참조하고 여러 행 및 테이블에서 값을 조정합니다.  
  
 행이 삽입 될 때 생성 되는 id 열 값과 달리 응용 프로그램 가져오려면 먼저 다음 시퀀스 번호를 호출 하 여 행을 삽입 하지 않고는 [NEXT VALUE FOR 함수](../../t-sql/functions/next-value-for-transact-sql.md)합니다. 여러 시퀀스 번호를 한 번에 가져오려면 [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) 를 사용합니다.  
  
 **CREATE SEQUENCE** 및 **NEXT VALUE FOR** 함수를 함께 사용하는 시나리오에 대한 자세한 내용은 [시퀀스 번호](../../relational-databases/sequence-numbers/sequence-numbers.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE SEQUENCE [schema_name . ] sequence_name  
    [ AS [ built_in_integer_type | user-defined_integer_type ] ]  
    [ START WITH <constant> ]  
    [ INCREMENT BY <constant> ]  
    [ { MINVALUE [ <constant> ] } | { NO MINVALUE } ]  
    [ { MAXVALUE [ <constant> ] } | { NO MAXVALUE } ]  
    [ CYCLE | { NO CYCLE } ]  
    [ { CACHE [ <constant> ] } | { NO CACHE } ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *sequence_name*  
 데이터베이스에서 시퀀스를 식별하는 고유 이름을 지정합니다. 형식이 **sysname**합니다.  
  
 [ built_in_integer_type | user-defined_integer_type  
 시퀀스는 모든 정수 유형으로 정의할 수 있습니다. 다음 형식이 허용됩니다.  
  
-   **tinyint** -0에서 255 사이의 범위  
  
-   **smallint** -32, 767 자로-32, 768 범위  
  
-   **int** --2147483648 ~ 2147483647 범위  
  
-   **bigint** -9223372036854775807에-9223372036854775808 범위  
  
-   **10 진수** 및 **숫자** 소수 자릿수가 0 인 합니다.  
  
-   허용되는 형식 중 하나에 기반을 둔 사용자 정의 데이터 형식(별칭 유형)  
  
 데이터 형식이 없는 경우는 **bigint** 데이터 형식이 기본적으로 사용 됩니다.  
  
 START WITH \<상수 >  
 시퀀스 개체가 반환하는 첫 번째 값입니다. **시작** 값 보다 작거나 같은 최대 및 보다 큰 값 이어야 하거나 시퀀스 개체의 최소 값과 일치 해야 합니다. 새 시퀀스 개체의 기본 시작 값은 오름차순 시퀀스 개체에 대해서는 최소값이고, 내림차순 시퀀스 개체에 대해서는 최대값입니다.  
  
 단위로 증가 \<상수 >  
 증가 시키거나 감소 시키는 (음수인 경우) 하는 데 사용 되는 값에 대 한 각 호출 시퀀스 개체의 값은 **NEXT VALUE FOR** 함수입니다. 증가값이 음수이면 시퀀스 개체가 내림차순이고, 그렇지 않으면 오름차순입니다. 증가값은 0일 수 없습니다. 새 시퀀스 개체의 기본 증가분은 1입니다.  
  
 [MINVALUE \<상수 > | **없습니다 MINVALUE** ]  
 시퀀스 개체의 경계를 지정합니다. 새 시퀀스 개체의 기본 최소값은 해당 시퀀스 개체의 데이터 형식에 대한 최소값입니다. **tinyint** 형식에 대해서는 0이고 다른 모든 데이터 형식에 대해서는 음수입니다.  
  
 [MAXVALUE \<상수 > | **MAXVALUE 없음**  
 시퀀스 개체의 경계를 지정합니다. 새 시퀀스 개체의 기본 최대값은 해당 시퀀스 개체의 데이터 형식에 대한 최대값입니다.  
  
 [주기 | **NO CYCLE** ]  
 시퀀스 개체를 최소값 또는 최대값(내림차순 시퀀스 개체의 경우)에서 다시 시작해야 하는지, 아니면 최소값 또는 최대값을 초과하는 경우 예외를 발생시켜야 하는지를 지정하는 속성입니다. 새 시퀀스 개체의 기본 순환 옵션은 NO CYCLE입니다.  
  
 시작 값이 아니라 최소값 또는 최대값에서 순환이 다시 시작됩니다.  
  
 [ **캐시** [\<상수 >] | 캐시 없음]  
 시스템 번호를 생성하는 데 필요한 디스크 IO 수를 최소화하여 시퀀스 개체를 사용하는 응용 프로그램의 성능을 향상시킵니다. 기본값으로 CACHE가 됩니다.  
  
 예를 들어, 캐시 크기 50 선택 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 캐시 된 50 개의 개별 값을 유지 하지 않습니다. 현재 값 및 캐시에 남아 있는 값의 개수만 캐시합니다. 따라서 캐시 저장에 필요한 메모리 양은 항상 시퀀스 개체 데이터 형식의 인스턴스 두 개입니다.  
  
> [!NOTE]  
>  캐시 크기를 지정하지 않고 캐시 옵션을 설정하면 데이터베이스 엔진에서 크기를 선택합니다. 그러나 선택의 일관성이 보장되지 않습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 는 캐시 크기 계산 방법을 예고 없이 변경할 수 있습니다.  
  
 사용 하 여 만든는 **캐시** 옵션을 예기치 않은 종료 (예: 정전) 캐시에 남아 있는 시퀀스 번호가 손실 될 수 있습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 시퀀스 번호는 현재 트랜잭션 범위 외부에서 생성되며, 시퀀스 번호를 사용하는 트랜잭션이 커밋되는지 또는 롤백되는지 여부에 관계없이 사용됩니다.  
  
### <a name="cache-management"></a>캐시 관리  
 성능 향상을 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 미리 시퀀스 번호를 지정 된 수를 할당 된 **캐시** 인수입니다.  
  
 예를 들어 시작 값이 1이고 캐시 크기가 15인 새 시퀀스가 만들어집니다. 첫 번째 값이 필요한 경우 1에서 15 사이의 값을 메모리에서 사용할 수 있습니다. 마지막으로 캐시된 값(15)은 디스크의 시스템 테이블에 기록됩니다. 15개 번호를 모두 사용한 경우 다음 요청(16번) 시 캐시가 다시 할당됩니다. 마지막으로 캐시된 새 값(30)은 시스템 테이블에 기록됩니다.  
  
 22개 번호를 사용한 후에 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 중지된 경우 이전에 저장된 번호 대신 메모리에서 다음에 예정된 시퀀스 번호(23)가 시스템 테이블에 기록됩니다.  
  
 SQL Server를 다시 시작한 후 시퀀스 번호가 필요하면 시스템 테이블에서 시작 번호(23)를 읽습니다. 15개 번호(23-38)의 캐시 양이 메모리에 할당되고 캐시되지 않은 다음 번호(39)가 시스템 테이블에 기록됩니다.  
  
 경우는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] (39) 시스템 테이블에서 읽은 번호로 전원 오류와 같은 이벤트에 대 한 비정상적으로 중지 되는 시퀀스가 다시 시작 합니다. 모든 시퀀스 번호 (않음 사용자 또는 응용 프로그램에서 요청한 적이 없는) 메모리에 할당 된 손실 됩니다. 이 기능은 동일한 값 되지 발생 하는 두 번 단일 시퀀스 개체에 대 한로 정의 되어 있지 않으면 있지만 간격이 생길 수 **주기** 또는 수동으로 다시 시작 합니다.  
  
 캐시는 현재 값(마지막으로 발생한 값) 및 캐시에 남아 있는 값의 개수에 대한 추적을 통해 메모리에서 유지 관리됩니다. 따라서 캐시에서 사용하는 메모리 양은 항상 시퀀스 개체 데이터 형식의 인스턴스 두 개입니다.  
  
 캐시 인수를 설정 **NO CACHE** 현재 시퀀스 값이 시퀀스는 데 사용 될 때마다 시스템 테이블에 기록 합니다. 이로 인해 디스크 액세스가 증가하여 성능이 저하될 수는 있지만 의도하지 않은 간격이 발생할 수 있는 가능성은 줄어듭니다. 사용 하 여 번호를 요청한 경우에 간격이 발생할 수는 **NEXT VALUE FOR** 또는 **sp_sequence_get_range** 함수 하지만 숫자는 사용 되지 않거나 커밋되지 않은 트랜잭션에서 사용 되 합니다.  
  
 시퀀스 개체를 사용 하는 경우는 **캐시** 옵션, 시퀀스 개체를 다시 시작 하거나 변경 하는 경우는 **증분**, **주기**, **MINVALUE**, **MAXVALUE**, 되거나 캐시 크기 속성을 변경 발생 하기 전에 시스템 테이블에 기록할 캐시 발생 됩니다. 그런 다음 건너뛰는 번호 없이 현재 값부터 캐시가 다시 로드됩니다. 캐시 크기 변경은 즉시 적용됩니다.  
  
 **캐시 된 값을 사용할 수 없는 경우 캐시 옵션**  
  
 시퀀스 개체에 대 한 다음 값을 생성 하도록 요청 된 다음 프로세스가 될 때마다 발생 합니다.는 **캐시** 옵션을 선택 된 시퀀스 개체에 대 한 메모리 내 캐시에 사용 되지 않는 값이 있습니다.  
  
1.  시퀀스 개체의 다음 값이 계산됩니다.  
  
2.  시퀀스 개체의 새로운 현재 값이 메모리 내에서 업데이트됩니다.  
  
3.  문 호출 시 계산된 값이 반환됩니다.  
  
 **캐시가 모두 사용 하는 경우의 CACHE 옵션**  
  
 시퀀스 개체는 다음 값을 생성 하도록 요청 될 때마다 다음 프로세스가 발생는 **캐시** 캐시를 모두 사용한 경우 옵션:  
  
1.  시퀀스 개체의 다음 값이 계산됩니다.  
  
2.  새 캐시의 마지막 값이 계산됩니다.  
  
3.  시퀀스 개체에 대한 시스템 테이블 행이 잠기고, 2단계에서 계산된 값(마지막 값)이 시스템 테이블에 기록됩니다. 유지되는 새 값을 사용자에게 알리기 위해 캐시가 모두 사용된 xevent가 실행됩니다.  
  
 **NO CACHE 옵션**  
  
 시퀀스 개체에 대 한 다음 값을 생성 하도록 요청 된 다음 프로세스가 될 때마다 발생 합니다.는 **NO CACHE** 옵션:  
  
1.  시퀀스 개체의 다음 값이 계산됩니다.  
  
2.  시퀀스 개체의 새로운 현재 값이 시스템 테이블에 기록됩니다.  
  
3.  문 호출 시 계산된 값이 반환됩니다.  
  
## <a name="metadata"></a>메타데이터  
 시퀀스에 대한 자세한 내용을 보려면 [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)를 쿼리하십시오.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 SCHEMA에 대한 **CREATE SEQUENCE**, **ALTER**또는 **CONTROL** 권한이 필요합니다.  
  
-   Db_owner 및 db_ddladmin 고정 데이터베이스 역할의 멤버 만들고 하 고 변경 하 고 시퀀스 개체를 삭제할 수 있습니다.  
  
-   Db_owner 및 db_datawriter 고정 데이터베이스 역할의 멤버를 숫자를 생성 하도록 하 여 시퀀스 개체를 업데이트할 수 있습니다.  
  
 다음 예에서는 테스트 스키마의 시퀀스를 만들 수 있는 한 AdventureWorks\Larry 권한이 사용자에 게 부여 합니다.  
  
```  
GRANT CREATE SEQUENCE ON SCHEMA::Test TO [AdventureWorks\Larry]  
```  
  
 사용 하 여 시퀀스 개체의 소유권은 이전할 수 있습니다는 **ALTER AUTHORIZATION** 문.  
  
 시퀀스에서 사용자 정의 데이터 형식을 사용하는 경우에는 시퀀스 작성자에게 해당 형식에 대한 REFERENCES 권한이 있어야 합니다.  
  
### <a name="audit"></a>감사  
 감사 **CREATE SEQUENCE**, 모니터는 **SCHEMA_OBJECT_CHANGE_GROUP**합니다.  
  
## <a name="examples"></a>예  
 시퀀스 만들기 및 사용에 대 한 예제는 **NEXT VALUE FOR** 함수 시퀀스 번호를 생성, 참조를 [시퀀스 번호](../../relational-databases/sequence-numbers/sequence-numbers.md)합니다.  
  
 대부분의 다음 예제는 Test 라는 스키마에 시퀀스 개체를 만듭니다.  
  
 테스트 스키마를 만들려면 다음 문을 실행 합니다.  
  
```  
CREATE SCHEMA Test ;  
GO  
```  
  
### <a name="a-creating-a-sequence-that-increases-by-1"></a>1. 1씩 증가하는 시퀀스 만들기  
 다음 예에서는 thierry 라는 사용자가 사용할 때마다 1 씩 증가 하는 CountBy1 라는 시퀀스를 만듭니다.  
  
```  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="b-creating-a-sequence-that-decreases-by-1"></a>2. 1씩 감소하는 시퀀스 만들기  
 다음 예에서는 0부터 시작하여 사용할 때마다 1씩 음수를 계산합니다.  
  
```  
CREATE SEQUENCE Test.CountByNeg1  
    START WITH 0  
    INCREMENT BY -1 ;  
GO  
```  
  
### <a name="c-creating-a-sequence-that-increases-by-5"></a>3. 5씩 증가하는 시퀀스 만들기  
 다음 예에서는 사용할 때마다 5씩 증가하는 시퀀스를 만듭니다.  
  
```  
CREATE SEQUENCE Test.CountBy1  
    START WITH 5  
    INCREMENT BY 5 ;  
GO  
```  
  
### <a name="d-creating-a-sequence-that-starts-with-a-designated-number"></a>4. 지정된 번호에서 시작하는 시퀀스 만들기  
 Thierry는 테이블을 가져온 후 지금까지 사용된 가장 높은 ID 번호가 24,328임을 알게 됩니다. Thierry에게는 24,329부터 번호를 생성하는 시퀀스가 필요합니다. 다음 코드에서는 24,329부터 시작하여 1씩 증가하는 시퀀스를 만듭니다.  
  
```  
CREATE SEQUENCE Test.ID_Seq  
    START WITH 24329  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="e-creating-a-sequence-using-default-values"></a>5. 기본값을 사용하여 시퀀스 만들기  
 다음 예에서는 기본값을 사용하여 시퀀스를 만듭니다.  
  
```  
CREATE SEQUENCE Test.TestSequence ;  
```  
  
 시퀀스 속성을 보려면 다음 문을 실행합니다.  
  
```  
SELECT * FROM sys.sequences WHERE name = 'TestSequence' ;  
```  
  
 출력의 목록 일부는 기본값을 나타냅니다.  
  
|||  
|-|-|  
|`start_value`|`-9223372036854775808`|  
|`increment`|`1`|  
|`mimimum_value`|`-9223372036854775808`|  
|`maximum_value`|`9223372036854775807`|  
|`is_cycling`|`0`|  
|`is_cached`|`1`|  
|`current_value`|`-9223372036854775808`|  
  
### <a name="f-creating-a-sequence-with-a-specific-data-type"></a>6. 지정한 데이터 형식으로 시퀀스 만들기  
 다음 예제에서는 사용 하 여 시퀀스는 **smallint** -32, 768에서 32,767 사이의 데이터 형식입니다.  
  
```  
CREATE SEQUENCE SmallSeq  
    AS smallint ;  
```  
  
### <a name="g-creating-a-sequence-using-all-arguments"></a>7. 모든 인수를 사용하여 시퀀스 만들기  
 다음 예제에서는 DecSeq를 사용 하 여 라는 시퀀스는 **10 진수** 데이터 형식을 0에서 255 사이입니다. 시퀀스는 125부터 시작하여 번호가 생성될 때마다 25씩 증가합니다. 시퀀스가 순환하도록 구성되었기 때문에 값이 최대값 200을 초과하는 경우 최소값 100에서 시퀀스가 다시 시작됩니다.  
  
```  
CREATE SEQUENCE Test.DecSeq  
    AS decimal(3,0)   
    START WITH 125  
    INCREMENT BY 25  
    MINVALUE 100  
    MAXVALUE 200  
    CYCLE  
    CACHE 3  
;  
```  
  
 첫 번째 값(`START WITH` 옵션 125)을 보려면 다음 문을 실행합니다.  
  
```  
SELECT NEXT VALUE FOR Test.DecSeq;  
```  
  
 150, 175 및 200을 반환하려면 문을 세 번 더 실행합니다.  
  
 시작 값이 `MINVALUE` 옵션 100으로 다시 순환되는 방식을 보려면 문을 다시 실행합니다.  
  
 캐시 크기를 확인하고 현재 값을 보려면 다음 코드를 실행합니다.  
  
```  
SELECT cache_size, current_value   
FROM sys.sequences  
WHERE name = 'DecSeq' ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER sequence&#40; Transact SQL &#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP sequence&#40; Transact SQL &#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [다음 값을 &#40; Transact SQL &#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [시퀀스 번호](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  

