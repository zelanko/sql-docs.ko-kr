---
title: 주요 변경 내용 관리 도구 기능에 SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3ff3fad8-b569-4516-bd58-5a3efeb537e2
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 33e204958f9cea2db092f2a9c4b7d20648e4182c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092705"
---
# <a name="breaking-changes-to-management-tools-features-in-sql-server-2014"></a>SQL Server 2014에서 관리 도구 기능의 주요 변경 내용
  이 항목에서는 관리 도구 기능의 주요 변경 내용을 설명합니다. 이러한 변경 내용에 따라 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 기반을 둔 응용 프로그램, 스크립트 또는 기능을 사용하지 못할 수도 있습니다. 이러한 문제는 업그레이드할 때 발생할 수 있습니다. 자세한 내용은 [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)을 참조하세요.  
  
## <a name="breaking-changes-in-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]의 주요 변경 내용  
 향후 정보 제공 예정  
  
## <a name="breaking-changes-in-includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]의 주요 변경 내용  
  
### <a name="you-cannot-use-includesssql11includessssql11-mdmd-management-tools-to-create-a-utility-control-point-on-a-includesskilimanjaroincludessskilimanjaro-mdmd-instance-of-sql-server"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 관리 도구를 사용하여 SQL Server의 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 인스턴스에 유틸리티 제어 지점을 만들 수 없습니다.  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]의 인스턴스에 유틸리티 제어 지점을 만들려면 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 관리 도구를 사용하십시오.  
  
### <a name="smo-has-been-reversioned-in-includesssql11includessssql11-mdmd"></a>SMO의 버전 변경 되었습니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 또는 이전 버전의 SMO를 사용하여 개발된 코드를 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 에 대해 빌드하려면 약간의 수정이 필요할 수 있습니다. 자세한 내용은 [Backward Compatibility in SMO](../relational-databases/server-management-objects-smo/backward-compatibility-in-smo.md)을(를) 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [이전 버전과의 호환성](../../2014/getting-started/backward-compatibility.md)  
  
  