---
title: sp_get_query_template (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_get_query_template
- sp_get_query_template_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_get_query_template
ms.assetid: 85e9bef7-2417-41a8-befa-fe75507d9bf2
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3fac47c5b84894f681ffc9c6729dd526f9e8488c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spgetquerytemplate-transact-sql"></a>sp_get_query_template(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  매개 변수가 있는 쿼리 형식을 반환합니다. 반환된 결과는 강제 매개 변수화를 사용한 매개 변수가 있는 형식의 쿼리 결과와 비슷합니다. TEMPLATE 계획 지침을 만들 때는 주로 sp_get_query_template는 사용 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_get_query_template  
   [ @querytext = ] N'query_text'  
   , @templatetext OUTPUT   
   , @parameters OUTPUT   
```  
  
## <a name="arguments"></a>인수  
 '*query_text*'  
 매개 변수가 있는 버전을 생성할 쿼리입니다. '*query_text*' N 유니코드 지정자 뒤에 야 하 고 작은따옴표로 묶어야 합니다. N'*query_text*'에 할당 된 값은 @querytext 매개 변수입니다. 형식임 **nvarchar (max)** 합니다.  
  
 @templatetext  
 Output 매개 변수 형식의 **nvarchar (max)** 받을 매개 변수가 있는 형식으로 표시 된 바와 같이 제공 *query_text* 문자열 리터럴로 합니다.  
  
 @parameters  
 Output 매개 변수 형식의 **nvarchar (max)** 표시 된 바에서 매개 변수가 매개 변수 이름과 데이터 형식 문자열 리터럴로 같이 제공 @templatetext합니다.  
  
## <a name="remarks"></a>주의  
 다음 경우 sp_get_query_template은 오류를 반환합니다.  
  
-   모든 상수 리터럴 값에 매개 변수가 없는 *query_text*합니다.  
  
-   *query_text* 가 null 인 경우 유니코드 문자열이 아니거나, 구문상 유효 하지, 또는 컴파일할 수 없습니다.  
  
 Sp_get_query_template 오류를 반환 하는 경우의 값을 수정 하지 않습니다는 @templatetext 및 @parameters 출력 매개 변수입니다.  
  
## <a name="permissions"></a>Permissions  
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
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터베이스 엔진 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [계획 지침을 사용하여 쿼리 매개 변수화 동작 지정](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)  
  
  
