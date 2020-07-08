---
title: 개체의 정책 기반 관리 정책 평가
description: SSMS(SQL Server Management Studio)를 사용하여 SQL Server 인스턴스, 데이터베이스 또는 데이터베이스 개체의 정책을 평가하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: b9e9d646-4894-4dee-a02a-0c71a8dc020e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 66171e02a8a33ff96d6de6ecb3e4a2c990c9affb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85654246"
---
# <a name="evaluate-a-policy-based-management-policy-from-an-object"></a>개체의 정책 기반 관리 정책 평가
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 서버 인스턴스, 데이터베이스 또는 데이터베이스 개체의 정책을 평가하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 개체의 정책을 평가하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   실행 모드는 정책의 일부로 정의되어 있으며 **정책 평가** 대화 상자에서 변경할 수 없습니다.  
  
-   **정책 평가** 대화 상자에는 데이터베이스 개체에 적합한 정책만 표시됩니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-evaluate-a-policy-from-an-object"></a>개체의 정책을 평가하려면  
  
1.  개체 탐색기에서 서버 인스턴스, 데이터베이스 또는 데이터베이스 개체를 마우스 오른쪽 단추로 클릭하고 **정책**을 가리킨 다음 **평가**를 선택합니다.  
  
2.  **정책 평가** 대화 상자에서 하나 이상의 정책을 선택하고 **평가** 를 클릭하여 평가 모드에서 정책을 실행합니다. 이렇게 하면 대상 집합에 대한 준수 보고서가 생성되지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 다시 구성되거나 앞으로 정책이 준수되도록 하지는 않습니다. 선택한 정책을 따르지 않고 정책 기반 관리로 다시 구성할 수 있는 속성이 있는 대상의 경우 **적용**을 클릭하여 정책 준수를 강제할 수 있습니다. **정책 평가** 대화 상자에서 사용할 수 있는 옵션에 대한 자세한 내용은 [Evaluate Policies Dialog Box, Policy Selection Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-policy-selection-page.md), [Evaluate Policies Dialog Box, Evaluation Results Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-evaluation-results-page.md)및 [Results Detailed View Dialog Box](../../relational-databases/policy-based-management/results-detailed-view-dialog-box.md)를 참조하십시오.  
  
3.  완료되면 **닫기**를 클릭합니다.  
  
  
