---
title: SET STATISTICS IO (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/10/2016
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
- SET_STATISTICS_IO_TSQL
- IO
- IO_TSQL
- SET STATISTICS IO
dev_langs:
- TSQL
helpviewer_keywords:
- disk I/O statistics [SQL Server]
- I/O [SQL Server], disk activity information
- disks [SQL Server], statement statistics
- STATISTICS IO option
- statements [SQL Server], statistical information
- SET STATISTICS IO statement
- statistical information [SQL Server], disk activity
ms.assetid: 7033aac9-a944-4156-9ff4-6ef65717a28b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3b2aad11610a23c3686e279daa60c57bf7c8154f
ms.sourcegitcommit: b09bccd6dfdba55b022355e892c29cb50aadd795
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2018
---
# <a name="set-statistics-io-transact-sql"></a>SET STATISTICS IO(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문에 의해 생성된 디스크 작동 크기에 대한 정보가 [!INCLUDE[tsql](../../includes/tsql-md.md)]에 표시되도록 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SET STATISTICS IO { ON | OFF }  
```  
  
## <a name="remarks"></a>주의  
 STATISTICS IO 옵션을 ON으로 설정하면 통계 정보가 표시됩니다. OFF로 설정하면 통계 정보가 표시되지 않습니다.  
  
 이 옵션을 ON으로 설정한 후에는 이 옵션을 다시 OFF로 설정할 때까지 이후 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 통계 정보를 반환합니다.  
  
 다음 표에서는 출력 항목을 나열하고 설명합니다.  
  
|출력 항목|의미|  
|-----------------|-------------|  
|**테이블**|테이블 이름입니다.|  
|**검색 수**|출력에 대한 최종 데이터 집합을 생성하도록 모든 값을 검색하기 위해 어느 방향으로든 리프 수준에 도달한 후 시작된 검색/찾기 횟수입니다.<br /><br /> 사용된 인덱스가 고유 인덱스이거나 기본 키의 클러스터형 인덱스이고 값을 하나만 찾는 중인 경우 검색 수가 0입니다. 예를 들면 `WHERE Primary_Key_Column = <value>`입니다.<br /><br /> 기본이 아닌 키 열에 정의 된 고유 하지 않은 클러스터형된 인덱스를 사용 하 여 하나의 값을 검색할 때 검색 수는 1입니다. 이 작업은 검색 중인 키 값의 중복 값을 확인하기 위해 수행됩니다. 예를 들면 `WHERE Clustered_Index_Key_Column = <value>`입니다.<br /><br /> 인덱스 키를 사용하는 키를 찾은 후 리프 수준에서 왼쪽 또는 오른쪽 방향으로 시작된 서로 다른 검색/찾기 횟수가 N인 경우 검색 수가 N이 됩니다.|  
|**논리적 읽기 수**|데이터 캐시에서 읽은 페이지 수입니다.|  
|**물리적 읽기 수**|디스크에서 읽은 페이지 수입니다.|  
|**미리 읽기 수**|쿼리에 대해 캐시에 넣어진 페이지 수입니다.|  
|**lob 논리적 읽기 수**|수가 **텍스트**, **ntext**, **이미지**, 또는 큰 값 유형 (**varchar (max)**, **nvarchar (max)**, **varbinary (max)**) 데이터 캐시에서 읽은 페이지입니다.|  
|**lob 물리적 읽기 수**|수가 **텍스트**, **ntext**, **이미지** 또는 큰 값 유형의 페이지는 디스크에서 읽기입니다.|  
|**lob 미리 읽기 수**|수가 **텍스트**, **ntext**, **이미지** 또는 큰 값 유형의 페이지 쿼리에 대해 캐시에 배치 합니다.|  
  
 SET STATISTICS IO 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
> [!NOTE]  
>  Transact-SQL 문이 LOB 열을 검색할 때 일부 LOB 검색 작업에 대해서는 LOB 트리를 여러 번 이동해야 할 수 있습니다. 이 경우 SET STATISTICS IO에서 예상 논리적 읽기 수보다 많이 보고할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 SET STATISTICS IO 옵션을 사용하려면 사용자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있는 적절한 권한이 있어야 합니다. SHOWPLAN 권한이 필요하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 문을 처리할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 논리적 및 물리적 읽기 수를 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO         
SET STATISTICS IO ON;  
GO  
SELECT *   
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET STATISTICS IO OFF;  
GO  
```  
  
 결과 집합은 다음과 같습니다.  
  
```  
Table 'ProductCostHistory'. Scan count 1, logical reads 5, physical   
reads 0, read-ahead reads 0, lob logical reads 0, lob physical reads 0,   
lob read-ahead reads 0.  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET showplan_all 옵션 &#40; Transact SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [통계 시간 &#40; 설정 합니다. Transact SQL &#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)  
  
  
