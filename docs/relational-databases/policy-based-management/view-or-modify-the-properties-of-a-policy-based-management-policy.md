---
title: 정책 기반 관리 정책의 속성 보기 또는 수정 | Microsoft 문서
ms.custom: ''
ms.date: 10/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, modify policies
- Policy-Based Management, view policies
ms.assetid: ba805504-5db5-4731-a8da-a0e89cb20c37
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d90e4f27ab2ce8d7e33f1b4e83e4f682d8446df9
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-policy"></a>정책 기반 관리 정책의 속성 보기 또는 수정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 정책 기반 관리 정책의 속성을 보거나 수정하는 방법에 대해 설명합니다.  
  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
  
####  <a name="Permissions"></a> Permissions  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-the-properties-of-all-policies-on-an-object"></a>개체에 있는 모든 정책의 속성을 보려면  
  
1.  개체 탐색기에서 서버, 서버 개체, 데이터베이스 또는 데이터베이스 개체를 마우스 오른쪽 단추로 클릭하고 **정책** 을 가리킨 다음 **보기**를 선택합니다. **정책 보기 –***object_name* 대화 상자에서 사용할 수 있는 옵션에 대한 자세한 내용은 [정책 보기 대화 상자](../../relational-databases/policy-based-management/view-policies-dialog-box.md)를 참조하세요.  
  
2.  완료되면 **닫기**를 클릭합니다.  
  
#### <a name="to-view-or-modify-a-specific-policys-properties"></a>특정 정책의 속성을 보거나 수정하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 보거나 수정하려는 정책 기반 관리 정책이 들어 있는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **정책 관리**를 확장합니다.  
  
4.  더하기 기호를 클릭하여 **정책** 폴더를 확장합니다.  
  
5.  보거나 수정하려는 정책을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **정책 열기 –***policy_name* 대화 상자에서 사용할 수 있는 옵션에 대한 자세한 내용은 [새 정책 만들기 또는 정책 열기 대화 상자, 일반 페이지](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-general-page.md) 또는 [새 정책 만들기 또는 정책 열기 대화 상자, 설명 페이지](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-description-page.md)를 참조하세요.  
  
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
  
 자세한 내용은 [syspolicy_policies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syspolicy-policies-transact-sql.md)를 참조하세요.  
  
  
