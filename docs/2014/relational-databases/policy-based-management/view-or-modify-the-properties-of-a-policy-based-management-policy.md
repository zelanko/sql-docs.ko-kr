---
title: 정책 기반 관리 정책의 속성 보기 또는 수정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, modify policies
- Policy-Based Management, view policies
ms.assetid: ba805504-5db5-4731-a8da-a0e89cb20c37
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6d5b5b5ee05f467c0881b38108d126da523ea2e7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62676938"
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-policy"></a>정책 기반 관리 정책의 속성 보기 또는 수정
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 정책 기반 관리 정책의 속성을 보거나 수정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **확인 하거나 정책의 속성을 사용 하 여 수정 합니다.**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-the-properties-of-all-policies-on-an-object"></a>개체에 있는 모든 정책의 속성을 보려면  
  
1.  개체 탐색기에서 서버, 서버 개체, 데이터베이스 또는 데이터베이스 개체를 마우스 오른쪽 단추로 클릭하고 **정책** 을 가리킨 다음 **보기**를 선택합니다. **정책 보기 –**_object_name_ 대화 상자에서 사용할 수 있는 옵션에 대한 자세한 내용은 [정책 보기 대화 상자](view-policies-dialog-box.md)를 참조하세요.  
  
2.  완료되면 **닫기**를 클릭합니다.  
  
#### <a name="to-view-or-modify-a-specific-policys-properties"></a>특정 정책의 속성을 보거나 수정하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 보거나 수정하려는 정책 기반 관리 정책이 들어 있는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **정책 관리**를 확장합니다.  
  
4.  더하기 기호를 클릭하여 **정책** 폴더를 확장합니다.  
  
5.  보거나 수정하려는 정책을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **정책 열기 –**_policy_name_ 대화 상자에서 사용할 수 있는 옵션에 대한 자세한 내용은 [새 정책 만들기 또는 정책 열기 대화 상자, 일반 페이지](../../integration-services/general-page-of-integration-services-designers-options.md) 또는 [새 정책 만들기 또는 정책 열기 대화 상자, 설명 페이지](create-new-policy-or-open-policy-dialog-box-description-page.md)를 참조하세요.  
  
6.  완료되었으면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-a-policys-properties"></a>정책의 속성을 보려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       execution_mode,  
       description,  
       is_enabled,  
       job_id  
    FROM syspolicy_policies;  
    GO  
    ```  
  
 자세한 내용은 [syspolicy_policies&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syspolicy-policies-transact-sql)를 참조하세요.  
  
  
