---
title: 정책 기반 관리 조건의 속성 보기 또는 수정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view policy conditions
- Policy-Based Management, modify policy conditions
ms.assetid: 890d7384-8444-4767-bb6f-f5debb155747
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9b69bf28cf3c57e51626479396f8cccc00f50477
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43806869"
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-condition"></a>정책 기반 관리 조건의 속성 보기 또는 수정
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 정책 기반 관리 조건의 속성을 보거나 수정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **확인 하거나 조건의 속성을 사용 하 여 수정 합니다.**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-or-modify-a-conditions-properties"></a>조건의 속성을 보거나 수정하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 보거나 수정하려는 조건이 들어 있는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **정책 관리**를 확장합니다.  
  
4.  더하기 기호를 클릭하여 **조건** 폴더를 확장합니다.  
  
5.  보거나 편집하려는 조건을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **조건 열기 –***condition_name* 대화 상자에서 사용 가능한 옵션에 대한 자세한 내용은 [새 조건 만들기 또는 조건 열기 대화 상자, 일반 페이지](../../integration-services/general-page-of-integration-services-designers-options.md), [조건 열기 대화 상자, 종속 정책 페이지](open-condition-dialog-box-dependent-policies-page.md), [새 조건 만들기 또는 조건 열기 대화 상자, 설명 페이지](create-new-condition-or-open-condition-dialog-box-description-page.md) 및 [고급 편집 조건 대화 상자](advanced-edit-condition-dialog-box.md)를 참조하세요.  
  
6.  완료되었으면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-a-conditions-properties"></a>조건의 속성을 보려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       description,  
       facet,  
       expression,  
       is_name_condition,  
       obj_name  
    FROM syspolicy_conditions;  
    GO  
  
    ```  
  
 자세한 내용은 [syspolicy_conditions&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syspolicy-conditions-transact-sql)을 참조하세요.  
  
  
