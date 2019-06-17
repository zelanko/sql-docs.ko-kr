---
title: COLUMNPROPERTY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COLUMNPROPERTY
- COLUMNPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column properties [SQL Server]
- parameters [SQL Server], properties
- COLUMNPROPERTY function
ms.assetid: 2408c264-6eca-4120-bb71-df043c7c2792
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6211f2b47aebc2c4087cc2ed4fe5b068a8686292
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65943979"
---
# <a name="columnproperty-transact-sql"></a>COLUMNPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 함수는 열 또는 매개 변수 정보를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
COLUMNPROPERTY ( id , column , property )   
```  
  
## <a name="arguments"></a>인수  
*id*  
테이블 또는 프로시저의 식별자(ID)가 포함된 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.
  
*column*  
열 또는 매개 변수의 이름이 포함된 식입니다.
  
*property*  
*id* 인수를 사용하는 경우 *property* 인수는 `COLUMNPROPERTY` 함수에서 반환할 정보 유형을 지정합니다. *property* 인수에는 다음 값 중 하나가 있을 수 있습니다.
  
|값|설명|반환 값|  
|---|---|---|
|**AllowsNull**|Null 값을 허용합니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
|**ColumnId**|**sys.columns.column_id**에 해당하는 열 ID 값입니다.|열 ID<br /><br /> **참고:** 여러 열을 쿼리할 때 열 ID 값의 시퀀스에 간격이 나타날 수 있습니다.|  
|**FullTextTypeColumn**|*열*의 문서 종류 정보를 보관하는 테이블의 TYPE COLUMN입니다.|이 함수의 두 번째 매개 변수로 전달된 열 이름 식에 대한 전체 텍스트 TYPE COLUMN의 ID입니다.|  
|**GeneratedAlwaysType**|시스템에서 생성된 열 값입니다. **sys.columns.generated_always_type**에 해당합니다.|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 0: 항상 생성되지 않음<br /><br /> 1: 항상 행 시작에 생성됨<br /><br /> 2: 항상 행 끝에 생성됨|  
|**IsColumnSet**|열이 열 집합입니다. 자세한 내용은 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)을 참조하세요.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
|**IsComputed**|열이 계산 열입니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
|**IsCursorType**|프로시저 매개 변수가 CURSOR 형식입니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
|**IsDeterministic**|열이 결정적입니다. 이 속성은 계산 열과 뷰 열에만 적용됩니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력 계산 열 또는 뷰 열이 아닙니다.|  
|**IsFulltextIndexed**|열이 전체 텍스트 인덱싱을 위해 등록됩니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
|**IsHidden**|시스템에서 생성된 열 값입니다. **sys.columns.is_hidden**에 해당합니다.|**적용 대상**: [!INCLUDE[ssCurrentLong](../../includes/sscurrent-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 0: 숨기지 않음<br /><br /> 1: 숨김|  
|**IsIdentity**|IDENTITY 속성을 사용하는 열입니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
|**IsIdNotForRepl**|IDENTITY_INSERT 설정을 확인하는 열입니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
|**IsIndexable**|열을 인덱싱할 수 있습니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
|**IsOutParam**|프로시저 매개 변수가 출력 매개 변수입니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
|**IsPrecise**|열이 정확합니다. 이 속성은 확정적인 열에만 적용할 수 있습니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력 확정적인 열이 아닙니다.|  
|**IsRowGuidCol**|열이 **uniqueidentifier** 데이터 형식이며, ROWGUIDCOL 속성으로 정의됩니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
|**IsSparse**|열이 스파스 열입니다. 자세한 내용은 [스파스 열 사용](../../relational-databases/tables/use-sparse-columns.md)을 참조하세요.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
|**IsSystemVerified**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 열의 결정성과 전체 자릿수 속성을 확인할 수 있습니다. 이 속성은 계산 열과 뷰 열에만 적용됩니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
|**IsXmlIndexable**|XML 인덱스에서 XML 열을 사용할 수 있습니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
|**정밀도**|열 또는 매개 변수의 데이터 형식 길이입니다.|지정한 열 데이터 형식의 길이<br /><br /> -1 = **xml** 또는 큰 값 형식<br /><br /> NULL = 잘못된 입력|  
|**소수 자릿수**|열 또는 매개 변수 데이터 형식에 대한 소수 자릿수입니다.|소수 자릿수 값<br /><br /> NULL = 잘못된 입력|  
|**StatisticalSemantics**|열에 의미 체계 인덱싱을 사용하도록 설정되어 있습니다.|1: TRUE<br /><br /> 0: FALSE|  
|**SystemDataAccess**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 시스템 카탈로그나 가상 시스템 테이블에 있는 데이터에 액세스하는 함수에서 열이 파생됩니다. 이 속성은 계산 열과 뷰 열에만 적용됩니다.|1: TRUE(읽기 전용 액세스를 나타냅니다.)<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
|**UserDataAccess**|뷰와 임시 테이블을 포함하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로컬 인스턴스에 저장된 사용자 테이블의 데이터에 액세스하는 함수에서 열이 파생됩니다. 이 속성은 계산 열과 뷰 열에만 적용됩니다.|1: TRUE(읽기 전용 액세스를 나타냅니다.)<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
|**UsesAnsiTrim**|테이블을 만들 때 ANSI_PADDING이 ON으로 설정되었습니다. 이 속성은 **char** 또는 **varchar** 형식의 열 또는 매개 변수에만 적용됩니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = 잘못된 입력|  
  
## <a name="return-types"></a>반환 형식
 **ssNoversion**  
  
## <a name="exceptions"></a>예외  
오류가 발생하거나 호출자에게 개체를 볼 수 있는 권한이 없으면 NULL을 반환합니다.
  
사용자는 소유하고 있거나 사용 권한을 부여 받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자에게 개체에 대한 올바른 권한이 없으면 `COLUMNPROPERTY`와 같은 메타데이터 내보내기 기본 제공 함수에서 NULL을 반환할 수 있습니다. 자세한 내용은 [메타데이터 표시 유형 구성](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.
  
## <a name="remarks"></a>Remarks  
열의 결정적 속성을 확인하는 경우 먼저 해당 열이 계산 열인지 확인하세요. **IsDeterministic** 인수는 계산되지 않은 열에 대해 NULL을 반환합니다. 계산 열을 인덱스 열로 지정할 수 있습니다.
  
## <a name="examples"></a>예  
다음 예제에서는 `LastName` 열의 길이를 반환합니다.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT COLUMNPROPERTY( OBJECT_ID('Person.Person'),'LastName','PRECISION')AS 'Column Length';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Column Length
-------------
50
```  
  
## <a name="see-also"></a>관련 항목:
[메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)
  
  
