---
title: 정책 기반 관리 패싯의 속성 보기
description: SSMS(SQL Server Management Studio)를 사용하여 SQL Server 정책 기반 관리 패싯의 속성을 보는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view facet properties
ms.assetid: 022a244c-c2e7-4467-b9a2-c7a27859be22
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3a5a938928817b8ffb5282b2af7d2a505b442302
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75558098"
---
# <a name="view-the-properties-of-a-policy-based-management-facet"></a>정책 기반 관리 패싯의 속성 보기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 정책 기반 관리 패싯의 속성을 보는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 패싯의 속성을 보려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-the-properties-of-a-facet"></a>패싯의 속성을 보려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 보려는 속성이 지정된 패싯이 들어 있는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **정책 관리**를 확장합니다.  
  
4.  더하기 기호를 클릭하여 **패싯** 폴더를 확장합니다.  
  
5.  보려는 속성이 지정된 패싯을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **패싯 속성 –** _facet_name_ 대화 상자에서 사용 가능한 옵션에 대한 자세한 내용은 [패싯 속성 대화 상자, 일반 페이지](../../relational-databases/policy-based-management/facet-properties-dialog-box-general-page.md), [패싯 속성 대화 상자, 종속 정책 페이지](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-policies-page.md) 및 [패싯 속성 대화 상자, 종속 조건 페이지](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-conditions-page.md)를 참조하세요.  
  
6.  완료되면 **닫기**를 클릭합니다.  

