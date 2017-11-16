---
title: "계산 열의 인덱스 | Microsoft 문서"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- computed columns, index creation
- index creation [SQL Server], computed columns
- imprecise columns
- persisted computed columns
- precise [SQL Server]
ms.assetid: 8d17ac9c-f3af-4bbb-9cc1-5cf647e994c4
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9d41339f5e014e4f957000734d8019b0703f8d42
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="indexes-on-computed-columns"></a>계산 열의 인덱스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  다음 요구 사항을 충족하면 계산 열에 인덱스를 정의할 수 있습니다.  
  
-   소유권 요구 사항  
  
-   결정성 요구 사항  
  
-   정밀도 요구 사항  
  
-   데이터 형식 요구 사항  
  
-   SET 옵션 요구 사항  
  
 **Ownership Requirements**  
  
 계산 열에서 모든 함수 참조의 소유자는 테이블 소유자와 같아야 합니다.  
  
 **Determinism Requirements**  
  
> [!IMPORTANT]  
>  지정된 입력 집합에 대해 항상 같은 결과 집합을 반환하는 식은 결정적입니다. **COLUMNPROPERTY** 함수의 [IsDeterministic](../../t-sql/functions/columnproperty-transact-sql.md) 속성은 *computed_column_expression* 이 결정적인지 여부를 보고합니다.  
  
 *computed_column_expression* 은 결정적이어야 합니다. *computed_column_expression* 은 다음 조건 중 하나 이상이 충족되는 경우 결정적입니다.  
  
-   식에서 참조하는 모든 함수가 결정적이고 정확합니다. 이러한 함수에는 사용자 정의 함수와 기본 제공 함수가 포함됩니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요. 계산 열이 PERSISTED일 경우 함수가 정확하지 않을 수 있습니다. 자세한 내용은 이 항목의 뒤에 나오는 [지속형 계산 열에 인덱스 만들기](#BKMK_persisted) 를 참조하십시오.  
  
-   식에서 참조하는 모든 열은 계산 열이 있는 테이블에서 가져옵니다.  
  
-   여러 행에서 데이터를 끌어 오는 열 참조가 없습니다. 예를 들어 SUM 또는 AVG와 같은 집계 함수는 여러 행의 데이터에 의존하므로 *computed_column_expression* 은 비결정적입니다.  
  
-   *computed_column_expression* 에는 시스템 데이터 액세스 또는 사용자 데이터 액세스가 없습니다.  
  
 CLR(공용 언어 런타임) 식이 포함된 계산 열에 인덱스를 만들려면 열이 결정적이어야 하고 PERSISTED로 표시되어야 합니다. CLR 사용자 정의 형식 식은 계산 열 정의에서 허용됩니다. CLR 사용자 정의 형식의 계산 열은 형식이 비교 가능하면 인덱스를 만들 수 있습니다. 자세한 내용은 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 인덱싱된 계산 열의 날짜 데이터 형식의 문자열 리터럴을 참조할 때 결정적 날짜 형식 스타일을 사용하여 리터럴을 원하는 날짜 유형으로 명시적으로 변환하는 것이 좋습니다. 결정적 날짜 형식 스타일 목록은 [CAST 및 CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하십시오. 데이터베이스 호환성 수준이 80 이하로 설정되지 않은 경우 문자열을 날짜 데이터 형식으로 암시적으로 변환하는 작업과 관련된 식은 비결정적인 것으로 간주됩니다. 서버 세션의 [LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) 및 [DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) 설정에 따라 결과가 달라지기 때문입니다. 예를 들어 ' `CONVERT (datetime, '30 listopad 1996', 113)` ' 문자열이 다른 언어에서는 다른 월을 의미하므로`30 listopad 1996`식의 결과는 LANGUAGE 설정에 따라 달라집니다. 마찬가지로 `DATEADD(mm,3,'2000-12-01')`에서는 DATEFORMAT 설정에 따라 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 식의 `'2000-12-01'` 문자열을 해석합니다.  
>   
>  호환성 수준이 80 이하로 설정되지 않은 경우에 데이터 정렬 간의 비유니코드 문자 데이터를 암시적으로 변환하는 작업도 비결정적인 것으로 간주됩니다.  
>   
>  데이터베이스 호환성 수준 설정이 90이면 이러한 식이 포함된 계산 열에 인덱스를 만들 수 없습니다. 그러나 업그레이드된 데이터베이스로부터 이러한 식을 포함하는 기존 계산 열은 유지할 수 있습니다. 문자열에서 날짜로의 암시적 변환이 포함된 인덱싱된 계산 열을 사용하는 경우 인덱스 손상을 방지하려면 데이터베이스와 응용 프로그램에서 LANGUAGE 및 DATEFORMAT 설정이 일치하는지 확인합니다.  
  
 **Precision Requirements**  
  
 *computed_column_expression* 은 정확해야 합니다. *computed_column_expression* 은 다음 조건 중 하나 이상이 충족되는 경우 정확합니다.  
  
-   **float** 또는 **real** 데이터 형식의 식이 아닙니다.  
  
-   정의에 **float** 또는 **real** 데이터 형식을 사용하지 않습니다. 예를 들어 다음 문에서 열 `y` 는 **int** 이고 결정적이지만 정확하지는 않습니다.  
  
    ```  
    CREATE TABLE t2 (a int, b int, c int, x float,   
       y AS CASE x   
             WHEN 0 THEN a   
             WHEN 1 THEN b   
             ELSE c   
          END);  
    ```  
  
> [!NOTE]  
>  **float** 또는 **real** 식은 정확하지 않은 것으로 간주되므로 인덱스의 키가 될 수 없습니다. **float** 또는 **real** 식은 인덱싱된 뷰에서 사용할 수 있지만 키로는 사용할 수 없습니다. 계산 열의 경우에도 마찬가지입니다. 함수, 식 또는 사용자 정의 함수에 **float** 또는 **real** 식이 포함되어 있으면 정확하지 않은 것으로 간주됩니다. 논리 식(비교)이 여기에 포함됩니다.  
  
 COLUMNPROPERTY 함수의 **IsPrecise** 속성은 *computed_column_expression* 이 정확한지 여부를 보고합니다.  
  
 **Data Type Requirements**  
  
-   계산 열에 대해 정의된 *computed_column_expression* 은 **text**, **ntext**또는 **image** 데이터 형식으로 계산할 수 없습니다.  
  
-   **image**, **ntext**, **text**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**및 **xml** 데이터 형식에서 파생된 계산 열의 경우 해당 데이터 형식을 인덱스 키 열로 사용할 수 있으면 인덱스를 만들 수 있습니다.  
  
-   **image**, **ntext**및 **text** 데이터 형식에서 파생된 계산 열의 경우 해당 데이터 형식을 키가 아닌 인덱스 열로 사용할 수 있으면 비클러스터형 인덱스에서 키가 아닌(포함된) 열이 될 수 있습니다.  
  
 **SET Option Requirements**  
  
-   계산 열을 정의하는 CREATE TABLE 또는 ALTER TABLE 문이 실행될 때 ANSI_NULLS 연결 수준 옵션이 ON으로 설정되어야 합니다. [OBJECTPROPERTY](../../t-sql/functions/objectproperty-transact-sql.md) 함수의 **IsAnsiNullsOn** 속성을 통해 이 옵션이 ON으로 설정되었는지 여부를 알 수 있습니다.  
  
-   인덱스가 만들어진 연결과 인덱스에서 값을 변경하는 INSERT, UPDATE 또는 DELETE 문을 실행하려 하는 모든 연결에서 6개의 SET 옵션이 ON으로 설정되어야 하고 하나의 옵션만 OFF로 설정되어야 합니다. 최적화 프로그램은 옵션 설정이 이와 다른 연결에서 실행된 SELECT 문에 대해 계산 열의 인덱스를 무시합니다.  
  
    -   NUMERIC_ROUNDABORT 옵션이 OFF로 설정되어야 하고 다음 옵션이 ON으로 설정되어야 합니다.  
  
    -   ANSI_NULLS  
  
    -   ANSI_PADDING  
  
    -   ANSI_WARNINGS  
  
    -   ARITHABORT  
  
    -   CONCAT_NULL_YIELDS_NULL  
  
    -   QUOTED_IDENTIFIER  
  
     데이터베이스 호환성 수준이 90 이상으로 설정된 경우 ANSI_WARNINGS를 ON으로 설정하면 암시적으로 ARITHABORT가 ON으로 설정됩니다.  
  
##  <a name="BKMK_persisted"></a> 지속형 계산 열에 인덱스 만들기  
 CREATE TABLE 또는 ALTER TABLE 문에서 열이 PERSISTED로 표시된 경우 결정적이지만 정확하지 않은 식으로 정의된 계산 열에 인덱스를 만들 수 있습니다. 즉, [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 계산된 값을 테이블에 저장하고 계산 열이 종속된 다른 열이 업데이트되면 해당 값을 업데이트합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 열에 인덱스를 만들 때와 이 인덱스가 쿼리에서 참조될 때 이러한 지속형 값을 사용합니다. 이 옵션을 사용하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 계산 열 식을 반환하는 함수, 특히 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]에서 생성된 CLR 함수가 결정적이면서 동시에 정확한지 여부를 확실히 판단할 수 없을 때에도 계산 열에 인덱스를 만들 수 있습니다.  
  
## <a name="related-content"></a>관련 내용  
 [COLUMNPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)  
  
  

