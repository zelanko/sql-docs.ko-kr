---
title: "인덱스 수정 | Microsoft 문서"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- indexes [SQL Server], modifying
- modifying indexes
- index changes [SQL Server]
ms.assetid: 97e3110d-fde7-4f5d-9309-dc1697960aeb
caps.latest.revision: "19"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7125967fca0055537af44460c0c8950ad7d5df9b
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="modify-an-index"></a>인덱스 수정
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 인덱스를 수정하는 방법에 대해 설명합니다.  
  
> [!IMPORTANT]  
>  PRIMARY KEY 또는 UNIQUE 제약 조건의 결과로 생성된 인덱스는 이 방법으로 수정할 수 없으며 대신 제약 조건을 수정해야 합니다.  
  
 **항목 내용**  
  
-   **인덱스를 수정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-modify-an-index"></a>인덱스를 수정하려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 테이블이 속한 데이터베이스를 확장한 다음 **테이블**을 확장합니다.  
  
3.  인덱스가 속한 테이블을 확장하고 **인덱스**를 확장합니다.  
  
4.  수정할 인덱스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
5.  **인덱스 속성** 대화 상자에서 원하는 대로 변경합니다. 예를 들어 인덱스 키에서 열을 추가 또는 제거하거나 인덱스 옵션의 설정을 변경할 수 있습니다.  
  
#### <a name="to-modify-index-columns"></a>인덱스 열을 수정하려면  
  
1.  인덱스 열을 추가 또는 제거하거나 그 위치를 변경하려면 **인덱스 속성** 대화 상자에서 **일반** 페이지를 선택합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-modify-an-index"></a>인덱스를 수정하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 `ProductID` 옵션을 사용하여 `Production.WorkOrder` 테이블의 `DROP_EXISTING` 열에서 기존 인덱스를 삭제하고 다시 만듭니다. `FILLFACTOR` 및 `PAD_INDEX` 옵션도 설정됩니다.  
  
     [!code-sql[IndexDDL#CreateIndex4](../../relational-databases/indexes/codesnippet/tsql/modify-an-index_1.sql)]  
  
     다음 예에서는 ALTER INDEX를 사용하여 `AK_SalesOrderHeader_SalesOrderNumber`인덱스에 몇 가지 옵션을 설정합니다.  
  
     [!code-sql[IndexDDL#AlterIndex4](../../relational-databases/indexes/codesnippet/tsql/modify-an-index_2.sql)]  
  
#### <a name="to-modify-index-columns"></a>인덱스 열을 수정하려면  
  
1.  인덱스 열을 추가 또는 제거하거나 그 위치를 변경하려면 인덱스를 삭제하고 다시 만들어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [INDEXPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [인덱스 옵션 설정](../../relational-databases/indexes/set-index-options.md)   
 [인덱스 이름 바꾸기](../../relational-databases/indexes/rename-indexes.md)  
  
  
