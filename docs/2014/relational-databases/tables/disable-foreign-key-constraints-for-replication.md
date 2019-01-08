---
title: 복제할 때 FOREIGN KEY 제약 조건 비활성화 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- constraints [SQL Server], foreign keys
- foreign keys [SQL Server], disabling constraints
- disabling constraints
ms.assetid: 4211f2fd-d16a-4081-995c-43f1f0827f0b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2cd2e4f3e5ee16c02ba48c6cd8ced98c06133dfb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52798883"
---
# <a name="disable-foreign-key-constraints-for-replication"></a>복제할 때 FOREIGN KEY 제약 조건 비활성화
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 복제에 대한 FOREIGN KEY 제약 조건을 비활성화할 수 있습니다. 이 기능은 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전의 데이터를 게시하는 경우에 유용할 수 있습니다.  
  
> [!NOTE]  
>  테이블이 복제를 사용하여 게시된 경우 복제 에이전트에 의해 수행된 작업의 FOREIGN KEY 제약 조건은 자동으로 비활성화됩니다. 복제 에이전트가 구독자에서 삽입, 업데이트 또는 삭제를 수행하면 제약 조건이 확인되지 않지만 사용자가 삽입, 업데이트 또는 삭제를 수행하면 제약 조건이 확인됩니다. 데이터가 원래 삽입, 업데이트 또는 삭제될 때 제약 조건이 게시자에 이미 확인되었으므로 복제 에이전트에 대한 제약 조건이 비활성화됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **복제에 대한 FOREIGN KEY 제약 조건을 비활성화하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>복제할 때 FOREIGN KEY 제약 조건을 비활성화하려면  
  
1.  **개체 탐색기**에서 수정할 FOREIGN KEY 제약 조건을 포함하는 테이블을 확장한 다음 **키** 폴더를 확장합니다.  
  
2.  외래 키 제약 조건을 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.  
  
3.  **외래 키 관계** 대화 상자에서 **복제에 적용** 값으로 **아니요**를 선택합니다.  
  
4.  **닫기**를 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>복제할 때 FOREIGN KEY 제약 조건을 비활성화하려면  
  
1.  [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 이 태스크를 수행하려면 FOREIGN KEY 제약 조건을 삭제합니다. 그런 다음 새 FOREIGN KEY 제약 조건을 추가하고 NOT FOR REPLICATION 옵션을 지정합니다.  
  
 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)을 참조하세요.  
  
###  <a name="TsqlExample"></a>  
