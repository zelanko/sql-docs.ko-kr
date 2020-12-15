---
description: CHECK 제약 조건 수정
title: CHECK 제약 조건 수정 | Microsoft 문서
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- CHECK constraints, modifying
- modifying constraints
- constraints [SQL Server], check
- constraints [SQL Server], modifying
ms.assetid: f22daef8-e350-40ef-8ff0-b5f87d1d9e56
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: af223b73ec73a4cd52bcf86e389284ad6b383ec4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97403943"
---
# <a name="modify-check-constraints"></a>CHECK 제약 조건 수정
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 특정 조건에 대한 제약 조건을 설정 또는 해제하는 옵션 또는 제약 조건 식을 변경할 때 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하여 CHECK 제약 조건을 수정할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **CHECK 제약 조건을 수정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-modify-a-check-constraint"></a>CHECK 제약 조건을 수정하려면  
  
1.  **개체 탐색기** 에서 CHECK 제약 조건이 포함된 테이블을 마우스 오른쪽 단추로 클릭한 다음 **디자인** 을 클릭합니다.  
  
2.  **테이블 디자이너** 메뉴에서 **CHECK 제약 조건...** 을 클릭합니다.  
  
3.  **CHECK 제약 조건** 대화 상자의 **선택한 CHECK 제약 조건** 아래에서 편집하려는 제약 조건을 선택합니다.  
  
4.  다음 표의 동작을 수행합니다.  
  
    |대상|수행할 단계|  
    |--------|------------------------|  
    |제약 조건 식 편집|**식** 필드에 새 식을 입력합니다.|  
    |제약 조건 이름 바꾸기|**이름** 필드에 새 이름을 입력합니다.|  
    |기존 데이터에 제약 조건 적용|**만들거나 활성화할 때 기존 데이터 검사** 옵션을 선택합니다.|  
    |테이블에 새 데이터를 추가하거나 테이블에서 기존 데이터를 업데이트할 때 제약 조건 비활성화|**INSERT 및 UPDATE에 대해 제약 조건 적용** 옵션을 해제합니다.|  
    |복제 에이전트가 테이블에서 데이터를 삽입하거나 업데이트할 때 제약 조건 비활성화.|**복제에 적용** 옵션을 해제합니다.|  
  
    > [!NOTE]  
    >  일부 데이터베이스의 경우 CHECK 제약 조건의 기능이 다릅니다.  
  
5.  **닫기** 를 클릭합니다.  
  
6.  **파일** 메뉴에서 ‘테이블 이름’ **저장** 을 클릭합니다.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 **CHECK 제약 조건을 수정하려면**  
  
 `CHECK` 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]제약 조건을 수정하려면 먼저 기존 `CHECK` 제약 조건을 삭제하고 새로운 정의를 사용하여 다시 만들어야 합니다. 자세한 내용은 [Check 제약 조건 삭제](../../relational-databases/tables/delete-check-constraints.md) 및 [Check 제약 조건 만들기](../../relational-databases/tables/create-check-constraints.md)를 참조하세요.  
  
###  <a name="TsqlExample"></a>  
