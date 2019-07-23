---
title: 가용성 그룹에 포함된 데이터베이스 사용
description: Always On 가용성 그룹에 포함된 데이터베이스를 사용하는 방법
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- contained database, AlwaysOnAvailabilityGroups
ms.assetid: cacce3ae-e940-4566-8298-6607c4268e74
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 26e92d38188b02c5a2ce0025cc2d33fccc5c6728
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988418"
---
# <a name="use-contained-databases-with-always-on-availability-groups"></a>Always On 가용성 그룹에 포함된 데이터베이스 사용 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 의 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 포함된 데이터베이스를 사용하는 방법에 대한 정보를 제공합니다.  
  
##  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   포함된 데이터베이스를 가용성 그룹에 추가하기 전에 가용성 그룹에 대한 가용성 복제본을 호스팅하는 모든 서버 인스턴스에서 **contained database authentication** 서버 옵션이 **1** 로 설정되어 있는지 확인합니다. 자세한 내용은 [contained database authentication 서버 구성 옵션](../../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md) 및 [서버 구성 옵션&#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)에서 포함된 데이터베이스를 사용하는 방법에 대한 정보를 제공합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [서버 구성 옵션&#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [포함된 데이터베이스](../../../relational-databases/databases/contained-databases.md)  
  
  
