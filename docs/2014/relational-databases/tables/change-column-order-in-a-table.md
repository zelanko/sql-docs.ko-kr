---
title: 테이블에서 열 순서 변경 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], change order in a table
- column order, change
ms.assetid: cd99ef56-9085-431a-a0fc-58e7add5399f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 63ac48034879edc245a429778de8347bed2de13e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85047210"
---
# <a name="change-column-order-in-a-table"></a>테이블에서 열 순서 변경
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 테이블 디자이너에서 열 순서를 변경할 수 있습니다.  
  
> [!CAUTION]  
>  테이블의 열 순서를 변경하면 특정 열 순서에 의존하는 코드나 애플리케이션에 영향을 줄 수 있습니다. 여기에는 쿼리, 뷰, 저장 프로시저, 사용자 정의 함수, 클라이언트 애플리케이션 등이 포함됩니다. 따라서 열 순서를 변경할 때는 이러한 결과를 미리 신중하게 고려해야 합니다. 가장 좋은 방법은 애플리케이션 및 쿼리 수준에서 반환된 열에서 순서를 지정하는 것입니다. SELECT *를 사용해도 테이블에 정의된 순서에 따라 모든 열이 순서대로 반환된다고 가정해서는 안됩니다. 항상 열을 표시하려는 순서에 따라 쿼리 및 애플리케이션에서 이름으로 열을 지정하세요.  
  
 **항목 내용**  
  
-   **열 순서를 변경하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-change-the-column-order"></a>열 순서를 변경하려면  
  
1.  **개체 탐색기**에서 순서를 바꾸려는 열이 있는 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 선택합니다.  
  
2.  순서를 바꾸려는 열 이름의 왼쪽에 있는 상자를 선택합니다.  
  
3.  테이블 내에 다른 위치로 열을 끌어 놓습니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 **열 순서를 변경하려면**  
  
 이 작업은 Transact-SQL 문을 사용하여 수행할 수 없습니다.  
  
###  <a name="TsqlExample"></a>  
