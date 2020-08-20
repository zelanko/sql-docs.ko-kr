---
description: 테이블에서 열 순서 변경
title: 테이블에서 열 순서 변경 | Microsoft 문서
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], change order in a table
- column order, change
ms.assetid: cd99ef56-9085-431a-a0fc-58e7add5399f
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f08a85998f087e6d49e1ae4939e807fb38f6341e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488655"
---
# <a name="change-column-order-in-a-table"></a>테이블에서 열 순서 변경
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

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
  
 Transact-SQL 문을 사용하여 이 작업을 지원하지 않습니다.  
  
###  <a name="TsqlExample"></a>  
