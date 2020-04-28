---
title: sp_get_query_template (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_get_query_template
- sp_get_query_template_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_get_query_template
ms.assetid: 85e9bef7-2417-41a8-befa-fe75507d9bf2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9841e7815f31af26aeeb3ed0f4783d3a36d83030
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68124076"
---
# <a name="sp_get_query_template-transact-sql"></a>sp_get_query_template(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  매개 변수가 있는 쿼리 형식을 반환합니다. 반환된 결과는 강제 매개 변수화를 사용한 매개 변수가 있는 형식의 쿼리 결과와 비슷합니다. sp_get_query_template은 주로 TEMPLATE 계획 지침을 만들 때 사용됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_get_query_template  
   [ @querytext = ] N'query_text'  
   , @templatetext OUTPUT   
   , @parameters OUTPUT   
```  
  
## <a name="arguments"></a>인수  
 '*query_text*'  
 매개 변수가 있는 버전을 생성할 쿼리입니다. '*query_text*'는 작은따옴표로 묶고 N 유니코드 지정자 뒤에와 야 합니다. N '*query_text*'은 (는) @querytext 매개 변수에 할당 된 값입니다. **Nvarchar (max)** 형식입니다.  
  
 @templatetext  
 는 표시 된 대로 제공 된 **nvarchar (max)** 형식의 출력 매개 변수 이며, 매개 변수가 있는 형식의 *query_text* 를 문자열 리터럴로 받습니다.  
  
 @parameters  
 는 지정 된 대로 제공 된 **nvarchar (max)** 형식의 출력 매개 변수 이며 매개 변수가 있는 @templatetext매개 변수 이름 및 데이터 형식의 문자열 리터럴을 수신 합니다.  
  
## <a name="remarks"></a>설명  
 다음 경우 sp_get_query_template은 오류를 반환합니다.  
  
-   *Query_text*에서 상수 리터럴 값을 매개 변수화 하지 않습니다.  
  
-   *QUERY_TEXT* NULL 이거나 유니코드 문자열이 아니거나 구문이 올바르지 않거나 컴파일될 수 없습니다.  
  
 Sp_get_query_template에서 오류를 반환 하는 경우 @templatetext 및 @parameters 출력 매개 변수의 값을 수정 하지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 public 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 두 상수 리터럴 값이 포함된 쿼리를 매개 변수가 있는 형식으로 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @my_templatetext nvarchar(max)  
DECLARE @my_parameters nvarchar(max)  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
        FROM Production.ProductModel pm   
        INNER JOIN Production.ProductInventory pi  
        ON pm.ProductModelID = pi.ProductID  
        WHERE pi.ProductID = 2  
        GROUP BY pi.ProductID, pi.Quantity  
        HAVING SUM(pi.Quantity) > 400',  
@my_templatetext OUTPUT,  
@my_parameters OUTPUT;  
SELECT @my_templatetext;  
SELECT @my_parameters;  
```  
  
 `@my_templatetext``OUTPUT` 매개 변수의 매개 변수가 있는 결과는 다음과 같습니다.  
  
 `select pi . ProductID , SUM ( pi . Quantity ) as Total`  
  
 `from Production . ProductModel pm`  
  
 `inner join Production . ProductInventory pi`  
  
 `on pm . ProductModelID = pi . ProductID`  
  
 `where pi . ProductID = @0`  
  
 `group by pi . ProductID , pi . Quantity`  
  
 `having SUM ( pi . Quantity ) > 400`  
  
 첫 번째 상수 리터럴 `2`는 매개 변수로 변환됩니다. 두 번째 리터럴 `400`은 `HAVING` 절 안에 있으므로 매개 변수로 변환되지 않습니다. sp_get_query_template에 의해 반환된 결과는 ALTER DATABASE의 PARAMETERIZATION 옵션이 FORCED로 설정된 경우의 매개 변수가 있는 쿼리 형식과 유사합니다.  
  
 `@my_parameters OUTPUT` 매개 변수의 매개 변수가 있는 결과는 다음과 같습니다.  
  
```  
@0 int  
```  
  
> [!NOTE]  
>  sp_get_query_template의 출력에서 매개 변수의 순서와 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 QFE(Quick-Fix Engineering), 서비스 팩 및 버전 업그레이드에 따라 변경될 수 있습니다. 또한 업그레이드를 수행하면 다른 상수 리터럴 집합은 같은 쿼리에 대한 매개 변수가 있을 수 있고 두 출력 매개 변수의 결과에 다른 간격이 적용될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [계획 지침을 사용하여 쿼리 매개 변수화 동작 지정](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)  
  
  
