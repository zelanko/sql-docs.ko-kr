---
title: "Microsoft SQL 데이터베이스 기능은 무엇입니까? | Microsoft Docs"
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- built-in functions [SQL Server]
- function [SQL Server] See functions [SQL Server]
- functions [Transact-SQL]
- functions [SQL Server], about functions
- scalar functions
- functions [SQL Server]
ms.assetid: 17186213-5ab5-40b0-b470-b660af1ec44c
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: fa55a0b066db617ef0d6f2f0471ad6866cac2d73
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="what-are-the-sql-database-functions"></a>SQL 데이터베이스 기능은 무엇입니까?
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

SQL 데이터베이스와 함께 사용할 수 있는 기본 제공 함수의 범주에 알아봅니다. 기본 제공 함수를 사용 하거나 사용자 정의 함수를 직접 만들 수 있습니다.
  
## <a name="aggregate-functions"></a>집계 함수

집계 함수는 값 집합에 대한 계산을 수행하고 단일 값을 반환합니다. 선택 목록 또는 SELECT 문의 HAVING 절에서 허용 됩니다. 행의 범주에 대 한 집계를 계산 하는 GROUP BY 절을 함께 집계를 사용할 수 있습니다. 특정 범위의 값에 대 한 집계를 계산 하는 OVER 절을 사용 합니다. OVER 절에 GROUPING 또는 GROUPING_ID 집계 올 수 없습니다.

모든 집계 함수는 결정적 함수가 동일한 입력된 값에 따라 실행 될 때 항상 동일한 값 반환. 자세한 내용은 참조 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md). |

## <a name="analytic-functions"></a>분석 함수
분석 함수는 행 그룹을 기반으로 집계 값을 계산합니다. 그러나 집계 함수와 달리 분석 함수 각 그룹에 대해 여러 행을 반환할 수 있습니다. 분석 함수를 사용 하 여 계산 이동 평균, 누계, 백분율, 프로그램 또는 그룹 내에서 상위 n 개 결과.

## <a name="ranking-functions"></a>순위 함수
순위 함수는 파티션에서 각 행의 순위 값을 반환합니다. 사용하는 함수에 따라 어떤 행은 다른 행과 동일한 값을 받을 수 있습니다. 순위 함수는 확정적이지 않습니다.

## <a name="rowset-functions"></a>행 집합 함수
행 집합 함수는 SQL 문에서 테이블 참조 처럼 사용할 수 있는 개체를 반환 합니다.

## <a name="scalar-functions"></a>스칼라 함수
단일 값에 대해 작동하며 단일 값을 반환합니다. 스칼라 함수는 식이 유효한 경우 언제든지 사용할 수 있습니다.

### <a name="categories-of-scalar-functions"></a>스칼라 함수의 범주
  
|함수 범주|Description|  
|-----------------------|-----------------|  
|[구성 함수](configuration-functions-transact-sql.md)|현재 구성에 대한 정보를 반환합니다.|  
|[변환 함수](conversion-functions-transact-sql.md)|데이터 형식 캐스팅 및 변환을 지원합니다.|  
|[커서 함수](cursor-functions-transact-sql.md)|커서에 대한 정보를 반환합니다.|  
|[날짜 및 시간 데이터 형식 및 함수](date-and-time-data-types-and-functions-transact-sql.md)|날짜 및 시간 입력 값에 대한 작업을 수행하며 문자열, 숫자 또는 날짜와 시간 값을 반환합니다.|  
|[JSON 함수](json-functions-transact-sql.md)|유효성 검사, 쿼리, 또는 JSON 데이터를 변경 합니다.|  
|[논리 함수](http://msdn.microsoft.com/library/5b2b4546-951b-462d-91d5-e41fc5acd6f9)|논리 연산을 수행합니다.|  
|[수치 연산 함수](mathematical-functions-transact-sql.md)|함수에 매개 변수로 제공되는 입력 값을 기반으로 하여 계산 작업을 수행하고 숫자 값을 반환합니다.|  
|[메타 데이터 함수](metadata-functions-transact-sql.md)|데이터베이스와 데이터베이스 개체에 대한 정보를 반환합니다.|  
|[보안 함수](security-functions-transact-sql.md)|사용자와 역할에 대한 정보를 반환합니다.|  
|[문자열 함수](string-functions-transact-sql.md)|문자열에 대 한 작업 수행 (**char** 또는 **varchar**) 값을 입력 하 고 문자열이 나 숫자 값을 반환 합니다.|  
|[시스템 함수](../../relational-databases/system-functions/system-functions-for-transact-sql.md)|작업을 수행하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 값, 개체 및 설정에 대한 정보를 반환합니다.|  
|[시스템 통계 함수](system-statistical-functions-transact-sql.md)|시스템에 대한 통계 정보를 반환합니다.|  
|[텍스트 및 이미지 함수](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)|텍스트 또는 이미지 입력 값이나 열에 대한 작업을 수행하고 그 값에 대한 정보를 반환합니다.|  
  
## <a name="function-determinism"></a>함수 결정성  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 제공 함수는 결정적이거나 비결정적입니다. 특정 입력 값 집합으로 함수를 호출했을 때 항상 동일한 결과를 반환하는 경우에는 함수가 결정적이며 동일한 특정 입력 값 집합으로 함수를 호출할 때마다 다른 결과를 반환할 수 있으면 비결정적입니다. 자세한 내용은 참조 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)  
  
## <a name="function-collation"></a>함수 데이터 정렬  
 입력으로 문자열을 받고 출력으로 문자열을 반환하는 함수는 출력에 입력 문자열의 데이터 정렬을 사용합니다.  
  
 문자가 아닌 항목을 입력으로 받고 문자열을 출력으로 반환하는 함수는 출력에 현재 데이터베이스의 기본 데이터 정렬을 사용합니다.  
  
 입력으로 여러 문자열을 받고 출력으로 문자열을 반환하는 함수는 데이터 정렬 선행 규칙을 사용하여 출력 문자열의 데이터 정렬을 설정합니다. 자세한 내용은 참조 [데이터 정렬 선행 규칙 &#40; Transact SQL &#41; ](../../t-sql/statements/collation-precedence-transact-sql.md).  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [결정적 및 비결 정적 함수](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)   
 [저장된 프로시저 &#40;를 사용 하 여 Mdx&#41;](../../mdx/using-stored-procedures-mdx.md)  
  
  
