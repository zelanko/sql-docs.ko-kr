---
title: 정책 기반 관리 정책 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, creating policies
ms.assetid: b28bf963-89f9-4941-b6c1-6004fec347f1
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 43132cbc9dc61ec0782abb01121deff7020d7eeb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-policy-based-management-policy"></a>정책 기반 관리 정책 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 정책 기반 관리 정책을 만드는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 정책을 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-policy"></a>정책을 만들려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 새로운 정책 기반 관리 정책을 만들려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **정책 관리**를 확장합니다.  
  
4.  **정책** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 정책**을 선택합니다.  
  
5.  **새 정책 만들기** 대화 상자의 **이름** 상자에 새 정책의 이름을 입력합니다.  
  
6.  정책을 만든 즉시 사용하려면 **사용** 확인란을 선택합니다. 평가 모드가 **요청 시**인 경우 **사용** 확인란은 사용할 수 없습니다.  
  
7.  **조건 확인** 목록에서 기존 조건 중 하나를 선택하거나 **새 조건**을 선택합니다. 조건을 편집하려면 조건을 선택한 다음 줄임표(**...**)를 클릭합니다. 자세한 내용은 [새로운 정책 기반 관리 조건 만들기](../../relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md) 또는 [정책 기반 관리 조건의 속성 보기 또는 수정](../../relational-databases/policy-based-management/view-or-modify-the-properties-of-a-policy-based-management-condition.md)을 참조하세요.  
  
8.  **적용 대상** 상자에서 이 정책의 대상 유형을 하나 이상 선택합니다. 일부 조건 및 패싯만 특정 대상 유형에 적용될 수 있습니다. 사용 가능한 대상 집합이 관련 상자에 나타납니다. **매** 를 확장하여 일부 대상 유형에 대한 필터링 조건을 선택합니다. 이 상자에 대상이 표시되지 않으면 검사 조건 범위가 서버 수준으로 지정됩니다.  
  
9. **평가 모드** 상자에서 이 정책의 동작 방식을 선택합니다. 서로 다른 조건은 서로 다른 유효한 평가 모드를 포함할 수 있습니다. 유효한 평가 모드에 대한 자세한 내용은 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)를 참조하세요.  
  
10. 일정에 따라 정책이 평가되는 경우 평가 모드를 **예약 시**로 설정하고 **선택** 을 클릭하여 일정을 선택하거나 **새로 만들기** 를 클릭하여 새 일정을 만듭니다.  
  
11. 정책을 대상 유형의 하위 집합으로 제한하려면 **서버 제한** 상자에 있는 제한 조건 중에서 선택하거나 새 조건을 만듭니다.  
  
     **새 정책 만들기** 대화 상자에서 사용할 수 있는 옵션에 대한 자세한 내용은 [새 정책 만들기 또는 정책 열기 대화 상자, 일반 페이지](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-general-page.md) 또는 [새 정책 만들기 또는 정책 열기 대화 상자, 설명 페이지](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-description-page.md)를 참조하십시오.  
  
12. 완료되면 **확인**을 클릭합니다.  
  
  
