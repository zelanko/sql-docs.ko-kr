---
title: COLUMNPROPERTY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: c6c2af8d231f03c40ee87d3468977c3b66cbeeb4
ms.contentlocale: ko-kr
ms.lasthandoff: 10/05/2017

---
# <a name="columnproperty-transact-sql"></a>COLUMNPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

열 또는 매개 변수에 대한 정보를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
COLUMNPROPERTY ( id , column , property )   
```  
  
## <a name="arguments"></a>인수  
*id*  
이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 테이블이 나 프로시저의 식별자 (ID)를 포함 하 합니다.
  
*열*  
열이나 매개 변수의 이름이 포함된 식입니다.
  
*속성*  
에 대해 반환 될 정보를 포함 하는 식 *id*, 이며 다음 값 중 하나를 사용할 수 있습니다.
  
|값|Description|반환 값|  
|---|---|---|
|**AllowsNull**|Null 값을 허용합니다.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**ColumnId**|에 해당 하는 열 ID 값 **sys.columns.column_id**합니다.|열 ID<br /><br /> **참고:** 여러 열을 쿼리할 열 ID 값의 시퀀스에 간격이 나타날 수 있습니다.|  
|**FullTextTypeColumn**|열의 문서 유형 정보를 보관 하는 테이블의 유형 열은 *열*합니다.|이 속성의 두 번째 매개 변수로 전달된 열에 대한 전체 텍스트 TYPE COLUMN의 ID입니다.|  
|**계산 됨**|열이 계산 열입니다.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsCursorType**|프로시저 매개 변수가 CURSOR 형식입니다.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsDeterministic**|열이 결정적입니다. 이 속성은 계산 열과 뷰 열에만 적용됩니다.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 입력이 잘못되었습니다. 계산 열 또는 뷰 열이 아닙니다.|  
|**IsFulltextIndexed**|전체 텍스트 인덱싱을 위해 등록된 열입니다.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsIdentity**|IDENTITY 속성을 사용하는 열입니다.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsIdNotForRepl**|IDENTITY_INSERT 설정을 확인하는 열입니다.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsIndexable**|열을 인덱싱할 수 있습니다.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsOutParam**|프로시저 매개 변수가 출력 매개 변수입니다.|1 = TRUE<br /><br /> 0 = FALSE NULL = 입력이 잘못되었습니다.|  
|**IsPrecise**|열이 정확합니다. 이 속성은 확정적인 열에만 적용할 수 있습니다.|1 = TRUE<br /><br /> 0 = FALSE NULL = 입력이 잘못되었습니다. 확정적인 열이 아닙니다.|  
|**IsRowGuidCol**|열에는 **uniqueidentifier** 데이터 형식이 며 ROWGUIDCOL 속성이 정의 됩니다.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsSystemVerified**|열의 확정성과 전체 자릿수 속성은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 확인할 수 있습니다. 이 속성은 계산 열과 뷰 열에만 적용됩니다.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsXmlIndexable**|XML 인덱스에서 XML 열을 사용할 수 있습니다.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**정밀도**|열 또는 매개 변수 데이터 형식의 길이입니다.|지정한 열 데이터 형식의 길이<br /><br /> -1 = **xml** 또는 큰 값 형식<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**소수 자릿수**|열 또는 매개 변수 데이터 형식의 소수 자릿수입니다.|소수 자릿수<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**StatisticalSemantics**|열에 의미 체계 인덱싱을 사용하도록 설정되어 있습니다.|1 = TRUE<br /><br /> 0 = FALSE|  
|**SystemDataAccess**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 시스템 카탈로그나 가상 시스템 테이블에 있는 데이터에 액세스하는 함수에서 열이 파생됩니다. 이 속성은 계산 열과 뷰 열에만 적용됩니다.|1 = TRUE(읽기 전용 액세스)<br /><br /> 0 = FALSE<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**UserDataAccess**|뷰와 임시 테이블을 포함하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로컬 인스턴스에 저장된 사용자 테이블의 데이터에 액세스하는 함수에서 열이 파생됩니다. 이 속성은 계산 열과 뷰 열에만 적용됩니다.|1 = TRUE(읽기 전용 액세스)<br /><br /> 0 = FALSE<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**UsesAnsiTrim**|테이블을 처음 만들었을 때 ANSI_PADDING을 ON으로 설정했습니다. 이 속성은 형식의 매개 변수 또는 열에만 적용 됩니다. **char** 또는 **varchar**합니다.|1= TRUE<br /><br /> 0= FALSE<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsSparse**|열이 스파스 열입니다. 자세한 내용은 [스파스 열 사용](../../relational-databases/tables/use-sparse-columns.md)을 참조하세요.|1= TRUE<br /><br /> 0= FALSE<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsColumnSet**|열이 열 집합입니다. 자세한 내용은 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)을 참조하세요.|1= TRUE<br /><br /> 0= FALSE<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**GeneratedAlwaysType**|열 값은 시스템에서 생성 합니다. 에 해당 **sys.columns.generated_always_type**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 0 = 항상 생성 되지 않음<br /><br /> 1 = 행 시작으로 항상 생성 됨<br /><br /> 2-generatedalways 마지막 행|  
|**IsHidden**|열 값은 시스템에서 생성 합니다. 에 해당 **sys.columns.is_hidden**|**적용 대상**: [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 0 = 숨겨진 되지 않음<br /><br /> 1 = 숨김|  
  
## <a name="return-types"></a>반환 형식
 **int**  
  
## <a name="exceptions"></a>예외  
오류가 발생하거나 호출자가 개체를 볼 수 있는 권한을 갖고 있지 않으면 NULL을 반환합니다.
  
사용자는 소유하고 있거나 사용 권한을 부여 받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자가 개체에 대한 사용 권한이 없으면 COLUMNPROPERTY와 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.
  
## <a name="remarks"></a>주의  
어떤 열의 확정적 속성을 확인할 때는 먼저 그 열이 계산 열인지 확인하세요. **IsDeterministic** 비계산된 열에 대 한 NULL을 반환 합니다. 계산 열을 인덱스 열로 지정할 수 있습니다.
  
## <a name="examples"></a>예  
다음 예에서는 `LastName` 열의 길이를 반환하는 방법을 보여 줍니다.
  
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
  
## <a name="see-also"></a>참고 항목
[메타 데이터 함수 &#40; Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[TYPEPROPERTY &#40; Transact SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)
  
  

