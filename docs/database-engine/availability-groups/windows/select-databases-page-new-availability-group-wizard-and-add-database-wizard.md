---
title: "데이터베이스 선택 페이지(새 가용성 그룹 마법사 및 데이터베이스 추가 마법사) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.adddatabasewizard.selectdatabases.f1
- sql13.swb.newagwizard.selectdatabases.f1
ms.assetid: 929c5e15-d087-438d-b1f2-aa97c5f8bff8
caps.latest.revision: "16"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 078e3295d1f381714f539393d497c7de4c346413
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="select-databases-page-new-availability-group-wizard-and-add-database-wizard"></a>Select Databases Page (New Availability Group Wizard and Add Database Wizard)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 도움말 항목에서는 **데이터베이스 지정** 페이지의 옵션에 대해 설명합니다. 이 항목은 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 의 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] 및 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에 적용됩니다.  
  
##  <a name="PageOptions"></a> 데이터베이스 선택 옵션  
 **이 SQL Server 인스턴스의 사용자 데이터베이스 선택** 표에는 모든 로컬 사용자 데이터베이스가 나열됩니다. 열은 다음과 같습니다.  
  
 **이름**  
 로컬 사용자 데이터베이스의 이름을 표시합니다.  

 **크기**  
 마법사에서 사용할 수 있는 데이터베이스 크기를 표시합니다.  
  
 **상태**  
 지정된 데이터베이스가 가용성 그룹에 추가하기 위한 사전 요구 사항을 충족하는지 여부를 나타내는 텍스트가 있는 하이퍼링크를 표시합니다. 상태가 "**사전 요구 사항 일치**"인 경우 데이터베이스를 가용성 그룹에 추가할 수 있습니다. 데이터베이스가 모든 사전 요구 사항을 충족하지 않는 경우 **상태** 하이퍼링크에 데이터베이스를 사용할 수 없는 이유에 대한 간략한 설명이 제공됩니다. 자세한 내용을 보려면 하이퍼링크를 클릭하세요.  
  
 사전 요구 사항을 충족하기 위해 데이터베이스에서 작업을 수행하는 동안 **데이터베이스 선택** 페이지에서 마법사를 종료할 수 있습니다. **데이터베이스 선택** 페이지로 돌아가서 **새로 고침** 을 클릭하여 표를 업데이트합니다.  
  
 **암호**  
 데이터베이스에 데이터베이스 마스터 키가 들어 있는 경우 데이터베이스 마스터 키에 대한 암호를 입력합니다.  
  
 **새로 고침**  
 표를 새로 고치려면 클릭합니다. 이 기능은 사전 요구 사항을 충족하기 위해 데이터베이스에서 작업을 수행한 이후에 유용합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [가용성 그룹에 데이터베이스 추가 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
