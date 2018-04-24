---
title: 개체의 정책 기반 관리 정책 평가 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
- Policy-Based Management, evaluate policy
ms.assetid: b9e9d646-4894-4dee-a02a-0c71a8dc020e
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b709891fe0702bdb95aa8c858d31efcccebcfd64
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="evaluate-a-policy-based-management-policy-from-an-object"></a>개체의 정책 기반 관리 정책 평가
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 서버 인스턴스, 데이터베이스 또는 데이터베이스 개체의 정책을 평가하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 개체의 정책을 평가하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   실행 모드는 정책의 일부로 정의되어 있으며 **정책 평가** 대화 상자에서 변경할 수 없습니다.  
  
-   **정책 평가** 대화 상자에는 데이터베이스 개체에 적합한 정책만 표시됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-evaluate-a-policy-from-an-object"></a>개체의 정책을 평가하려면  
  
1.  개체 탐색기에서 서버 인스턴스, 데이터베이스 또는 데이터베이스 개체를 마우스 오른쪽 단추로 클릭하고 **정책**을 가리킨 다음 **평가**를 선택합니다.  
  
2.  **정책 평가** 대화 상자에서 하나 이상의 정책을 선택하고 **평가** 를 클릭하여 평가 모드에서 정책을 실행합니다. 이렇게 하면 대상 집합에 대한 준수 보고서가 생성되지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 다시 구성되거나 앞으로 정책이 준수되도록 하지는 않습니다. 선택한 정책을 따르지 않고 정책 기반 관리로 다시 구성할 수 있는 속성이 있는 대상의 경우 **적용**을 클릭하여 정책 준수를 강제할 수 있습니다. **정책 평가** 대화 상자에서 사용할 수 있는 옵션에 대한 자세한 내용은 [Evaluate Policies Dialog Box, Policy Selection Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-policy-selection-page.md), [Evaluate Policies Dialog Box, Evaluation Results Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-evaluation-results-page.md)및 [Results Detailed View Dialog Box](../../relational-databases/policy-based-management/results-detailed-view-dialog-box.md)를 참조하십시오.  
  
3.  완료되면 **닫기**를 클릭합니다.  
  
  
