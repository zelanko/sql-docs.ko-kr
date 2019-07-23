---
title: SET SHOWPLAN_ALL(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET SHOWPLAN_ALL
- SET_SHOWPLAN_ALL_TSQL
- SHOWPLAN_ALL
- SHOWPLAN_ALL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- SET SHOWPLAN_ALL statement
- SHOWPLAN_ALL option
- canceling statement execution
- stopping statement execution
- estimated execution information [SQL Server]
ms.assetid: a500b682-bae4-470f-9e00-47de905b851b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 063c4c94fc457b6b9bb69fa0395398c62bf49516
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941698"
---
# <a name="set-showplanall-transact-sql"></a>SET SHOWPLAN_ALL(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하지 않도록 합니다. 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 문이 실행된 방법에 대한 자세한 정보를 반환하고 해당 문에 대한 예상 리소스 요구 사항을 제공합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SET SHOWPLAN_ALL { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 SET SHOWPLAN_ALL 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
 SET SHOWPLAN_ALL 옵션을 ON으로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 각 문을 실행하지 않고 문에 대한 실행 정보를 반환하고 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 실행되지 않습니다. 이 옵션을 ON으로 설정할 경우 다시 OFF로 설정할 때까지 이후 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 대한 정보가 반환됩니다. 예를 들어, SET SHOWPLAN_ALL을 ON으로 설정한 상태에서 CREATE TABLE 문을 실행하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 같은 테이블이 사용되는 이후 SELECT 문에서 지정한 테이블이 없음을 알리는 오류 메시지를 반환합니다. 따라서 이후 이 테이블을 참조하는 작업은 실패합니다. SET SHOWPLAN_ALL 옵션을 OFF로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 보고서를 생성하지 않고 문을 실행합니다.  
  
 SET SHOWPLAN_ALL은 그 출력을 처리하도록 작성된 응용 프로그램에서 사용하기 위한 옵션입니다. SET SHOWPLAN_TEXT 옵션을 사용하여 **osql** 유틸리티와 같은 Microsoft Win32 명령 프롬프트 애플리케이션에 읽을 수 있는 출력을 반환할 수 있습니다.  
  
 SET SHOWPLAN_TEXT와 SET SHOWPLAN_ALL 옵션을 저장 프로시저 내에 지정할 수 없으며 일괄 처리에서 유일한 문이어야 합니다.  
  
 SET SHOWPLAN_ALL은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 프로세서가 각 문을 실행할 때 취한 단계를 나타내는 계층적 트리를 이루는 행 집합으로 정보를 반환합니다. 출력에 반영된 각 문에는 문의 텍스트가 있는 단일 행이 포함되고, 이 단일 행 뒤에는 실행 단계에 대한 자세한 정보가 있는 몇 개의 행이 있습니다. 아래 표에서는 출력에 포함된 열을 보여 줍니다.  
  
|열 이름|설명|  
|-----------------|-----------------|  
|**StmtText**|PLAN_ROW 형식이 아닌 행에 대해 이 열에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 텍스트가 포함됩니다. PLAN_ROW 유형의 행에 대해서는 이 열에 작업의 설명이 포함됩니다. 이 열에는 물리적 연산자가 포함되며 논리 연산자가 포함될 경우도 있습니다. 이 열 다음에 물리적 연산자가 결정한 설명이 나올 경우도 있습니다. 자세한 내용은 [실행 계획 논리 및 물리 연산자 참조](../../relational-databases/showplan-logical-and-physical-operators-reference.md)를 참조하세요.|  
|**StmtId**|현재 일괄 처리에 있는 문의 수입니다.|  
|**NodeId**|현재 쿼리의 노드 ID입니다.|  
|**Parent**|부모 단계의 노드 ID입니다.|  
|**PhysicalOp**|노드에 대한 물리적 구현 알고리즘입니다. PLAN_ROWS 형식의 행에만 해당됩니다.|  
|**LogicalOp**|이 노드가 나타내는 관계형 대수 연산자입니다. PLAN_ROWS 형식의 행에만 해당됩니다.|  
|**Argument**|수행되는 작업에 대한 추가 정보를 제공합니다. 물리적 연산자에 따라 이 열의 내용이 달라집니다.|  
|**DefinedValues**|이 연산자가 사용하는 값에 대한 쉼표로 구분된 목록을 포함합니다. 이 값은 현재 쿼리에 있었던 계산된 식(예: SELECT 목록이나 WHERE 절에 있음)이거나 이 쿼리를 처리하기 위해 쿼리 프로세서에서 사용한 내부 값입니다. 쿼리 내의 어디에서든 정의된 이 값이 참조될 수 있습니다. PLAN_ROWS 형식의 행에만 해당됩니다.|  
|**EstimateRows**|이 연산자가 생성한 출력의 예상 행 수입니다. PLAN_ROWS 형식의 행에만 해당됩니다.|  
|**EstimateIO**|이 연산자의 예상 I/O 비용입니다. PLAN_ROWS 형식의 행에만 해당됩니다.|  
|**EstimateCPU**|이 연산자의 예상 CPU 비용입니다. PLAN_ROWS 형식의 행에만 해당됩니다.|  
|**AvgRowSize**|이 연산자를 통해 통과되는 행의 예상 평균 행 크기(바이트)입니다.|  
|**TotalSubtreeCost**|이 작업과 모든 자식 작업의 예상(누적) 비용입니다.|  
|**OutputList**|현재 작업에서 예상하고 있는 열에 대한 쉼표로 구분된 목록을 포함합니다.|  
|**경고**|현재 작업과 연관된 경고 메시지에 대한 쉼표로 구분된 목록을 포함합니다. 경고 메시지에 열 목록과 함께 "NO STATS:()" 문자열이 포함될 경우도 있습니다. 이 경고 메시지는 쿼리 최적화 프로그램이 이 열의 통계에 기초하여 결정을 내리려고 했지만 사용 가능한 통계가 없었음을 나타냅니다. 따라서 쿼리 최적화 프로그램이 추측을 해야 했고 결과적으로 비효율적인 쿼리 계획을 선택했을 수도 있습니다. 쿼리 최적화 프로그램이 더 효율적인 쿼리 계획을 선택할 수 있도록 통계를 만들거나 업데이트하는 방법은 [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md)를 참조하세요. 어떤 경우에는 이 열에 조인 조건자 없이 조인(테이블을 수반하는)이 일어났음을 나타내는 "MISSING JOIN PREDICATE" 문자열이 포함되기도 합니다. 실수로 조인 조건자를 삭제하면 예상보다 실행 시간이 긴 쿼리가 만들어지고 큰 결과 집합이 반환됩니다. 이 경고가 나타나면 조인 조건자를 의도적으로 사용하지 않았는지 확인하세요.|  
|**형식**|노드 유형. 각 쿼리의 부모 노드에 대해서는 노드 유형이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 유형(예: SELECT, INSERT, EXECUTE 등)입니다. 실행 계획을 나타내는 하위 노드에 대해서는 PLAN_ROW 유형입니다.|  
|**Parallel**|**0** = 연산자가 병렬로 실행되지 않습니다.<br /><br /> **1** = 연산자가 병렬로 실행됩니다.|  
|**EstimateExecutions**|현재 쿼리를 실행하는 동안 이 연산자가 실행될 예상 횟수입니다.|  
  
 비용 단위는 벽 시계 시간(wall-clock time)이 아닌 내부 측정 시간을 기반으로 합니다. 다른 계획과 비교하여 계획의 상대 비용을 결정하는 데 사용합니다.  
  
## <a name="permissions"></a>사용 권한  
 SET SHOWPLAN_ALL을 사용하려면 SET SHOWPLAN_ALL이 실행되는 문을 실행할 수 있는 권한이 있어야 하며 참조된 개체를 포함하는 모든 데이터베이스에 대한 SHOWPLAN 권한이 있어야 합니다.  
  
 SELECT, INSERT, UPDATE, DELETE, EXEC *stored_procedure* 및 EXEC *user_defined_function* 문의 경우 실행 계획을 생성하려면 사용자에게 다음 권한이 있어야 합니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있는 적절한 권한  
  
-   테이블이나 뷰와 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 참조하는 개체를 포함한 모든 데이터베이스에 대해 SHOWPLAN 권한이 있어야 합니다.  
  
 DDL, USE *database_name*, SET, DECLARE, 동적 SQL 등과 같은 다른 모든 문의 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있는 권한만 있으면 됩니다.  
  
## <a name="examples"></a>예  
 다음의 두 문은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 쿼리에서의 인덱스 사용을 분석하고 최적화하는 방법을 보여 주기 위해 SET SHOWPLAN_ALL 설정을 사용합니다.  
  
 첫 번째 쿼리에서는 인덱싱된 열의 WHERE 절에 Equals 비교 연산자(=)를 사용합니다. 그 결과 **LogicalOp** 열에 클러스터형 인덱스 검색 값이 들어가고 **Argument** 열에는 인덱스 이름이 들어갑니다.  
  
 두 번째 쿼리에서는 WHERE 절에 LIKE 연산자를 사용합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 클러스터형 인덱스 검색을 사용하여 WHERE 절 조건을 충족하는 데이터를 찾을 수 있습니다. 그 결과 **Argument** 열에 인덱스 이름이 있는 상태에서 **LogicalOp** 열에 클러스터형 인덱스 검색 값이 들어가고, **Argument** 열에 WHERE 절 조건이 있는 상태에서 **LogicalOp** 열에 필터 값이 들어갑니다.  
  
 처음 인덱싱된 쿼리의 경우에는 **EstimateRows** 및 **TotalSubtreeCost** 특성의 값이 더 작습니다. 즉, 인덱싱된 쿼리가 인덱싱되지 않은 쿼리에 비해 훨씬 빨리 처리되고 리소스도 더 적게 사용한다는 의미입니다.  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_ALL ON;  
GO  
-- First query.  
SELECT BusinessEntityID   
FROM HumanResources.Employee  
WHERE NationalIDNumber = '509647174';  
GO  
-- Second query.  
SELECT BusinessEntityID, EmergencyContactID   
FROM HumanResources.Employee  
WHERE EmergencyContactID LIKE '1%';  
GO  
SET SHOWPLAN_ALL OFF;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_TEXT&#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-text-transact-sql.md)   
 [SET SHOWPLAN_XML&#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-xml-transact-sql.md)  
  
  
