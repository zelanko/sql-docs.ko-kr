---
title: 정책 기반 관리 정책의 정책 평가 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: 0b3214bd-d0ab-45ab-9281-3d95507abe54
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4820426060069c805bd0391fa2f1f135f2766ed3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48228143"
---
# <a name="evaluate-a-policy-based-management-policy-from-that-policy"></a>정책 기반 관리 정책의 정책 평가
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 정책을 통해 해당 정책을 평가하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 정책을 평가하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-evaluate-a-policy"></a>정책을 평가하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 평가할 정책이 들어 있는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **정책 관리**를 확장합니다.  
  
4.  더하기 기호를 클릭하여 **정책** 폴더를 확장합니다.  
  
5.  평가할 정책을 마우스 오른쪽 단추로 클릭하고 **평가**를 선택합니다.  
  
6.  **평가 결과**  대화 상자에 정책 평가의 결과가 표시됩니다. 정책을 따르지 않고 정책 기반 관리로 다시 구성할 수 있는 속성이 있는 대상의 경우 **적용**을 클릭하여 준수를 강제할 수 있습니다. **정책 평가** 대화 상자에서 사용할 수 있는 옵션에 대한 자세한 내용은 [Evaluate Policies Dialog Box, Policy Selection Page](evaluate-policies-dialog-box-policy-selection-page.md) 및 [Evaluate Policies Dialog Box, Evaluation Results Page](evaluate-policies-dialog-box-evaluation-results-page.md)를 참조하세요.  
  
7.  완료되면 **닫기**를 클릭합니다.  
  
  
