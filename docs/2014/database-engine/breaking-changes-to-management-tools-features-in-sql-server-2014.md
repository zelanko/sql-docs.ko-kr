---
title: SQL Server 2014의에서 기능을 도구 관리의 주요 변경 내용 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 3ff3fad8-b569-4516-bd58-5a3efeb537e2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9f3e0df9dc3f9c81907d4c230a36586a5953baf9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079433"
---
# <a name="breaking-changes-to-management-tools-features-in-sql-server-2014"></a>SQL Server 2014에서 관리 도구 기능의 주요 변경 내용
  이 항목에서는 관리 도구 기능의 주요 변경 내용을 설명합니다. 이러한 변경 내용에 따라 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 기반을 둔 애플리케이션, 스크립트 또는 기능을 사용하지 못할 수도 있습니다. 이러한 문제는 업그레이드할 때 발생할 수 있습니다. 자세한 내용은 [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)을 참조하세요.  
  
## <a name="breaking-changes-in-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]의 주요 변경 내용  
 향후 정보 제공 예정  
  
## <a name="breaking-changes-in-includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]의 주요 변경 내용  
  
### <a name="you-cannot-use-includesssql11includessssql11-mdmd-management-tools-to-create-a-utility-control-point-on-a-includesskilimanjaroincludessskilimanjaro-mdmd-instance-of-sql-server"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 관리 도구를 사용하여 SQL Server의 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 인스턴스에 유틸리티 제어 지점을 만들 수 없습니다.  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]의 인스턴스에 유틸리티 제어 지점을 만들려면 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 관리 도구를 사용하십시오.  
  
### <a name="smo-has-been-reversioned-in-includesssql11includessssql11-mdmd"></a>Smo에서 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 또는 이전 버전의 SMO를 사용하여 개발된 코드를 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 에 대해 빌드하려면 약간의 수정이 필요할 수 있습니다. 자세한 내용은 [Backward Compatibility in SMO](../relational-databases/server-management-objects-smo/backward-compatibility-in-smo.md)을(를) 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [이전 버전과의 호환성](../../2014/getting-started/backward-compatibility.md)  
  
  
