---
title: 에지 제약 조건 수정 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- alter edge constraints
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e5b6a471156f0b1371c727ce96aac72f4f812dac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62693320"
---
# <a name="modify-edge-constraints"></a>에지 제약 조건 수정
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)]를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 에지 제약 조건을 수정할 수 있습니다. 에지 제약 조건 절 순서를 변경하거나 새 절을 추가하여 에지 테이블의 에지 제약 조건을 수정할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **에지 제약 조건을 수정하려면 다음을 사용합니다.**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용
 Transact-SQL을 사용하여 에지 제약 조건을 수정하려면 먼저 기존 에지 제약 조건을 삭제하고 새로운 정의를 사용하여 다시 만들어야 합니다. 자세한 내용은 [에지 제약 조건 삭제](../../relational-databases/tables/delete-edge-constraint.md) 및 [에지 제약 조건 만들기](../../relational-databases/tables/create-edge-constraints.md)를 참조하세요.    
 
