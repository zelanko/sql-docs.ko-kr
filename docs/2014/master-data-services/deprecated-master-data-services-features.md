---
title: SQL Server 2014에서 사용 되지 않는 MDS(Master Data Services) 기능 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d8506bda-66dd-45a4-bfc9-3a10fa665acc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: dd6342542da7528fef633ba02a430a8ba2ef5857
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65483062"
---
# <a name="deprecated-master-data-services-features-in-sql-server-2014"></a>SQL Server 2014에서 사용되지 않는 MDS(Master Data Services) 기능
  이 항목에서는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 에서 계속 제공되지만 더 이상 사용되지 않는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]기능에 대해 설명합니다. 이러한 기능은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 이후 릴리스에서 제거될 예정입니다. 새 애플리케이션에는 이러한 기능을 사용하면 안 됩니다.  
  
## <a name="staging-process"></a>준비 프로세스  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 에서 사용된 준비 프로세스는 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션에서 더 이상 사용되지 않습니다. 하지만 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서는 계속 사용할 수 있습니다.  
  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 준비 프로세스의 준비 오류는 더 이상 UI에 표시되지 않습니다. 준비 프로세스 중에 채워지는 오류 코드는 준비 테이블에서 계속 사용할 수 있으며에서 찾을 수 있습니다 [https://msdn.microsoft.com/library/ff487022.aspx](https://msdn.microsoft.com/library/ff487022.aspx).  
  
 준비 테이블(tblStgMember, tblStgMemberAttribute 및 tblStgRelationship)은 여전히 데이터베이스에서 사용할 수 있습니다. 준비 프로세스를 시작하는 데 사용되는 저장 프로시저(mdm.udpStagingSweep)는 여전히 데이터베이스에서 사용할 수 있습니다.  
  
 준비 프로세스를 호출하는 웹 서비스 메서드를 여전히 사용할 수 있습니다.  
  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 에서 설정된 준비 간격이 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 및 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]의 준비 프로세스에도 적용됩니다.  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에는 향상된 성능의 새로운 준비 프로세스가 구현되었습니다. 자세한 내용은 [데이터 가져오기&#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)를 참조하세요.  
  
## <a name="metadata"></a>메타데이터  
 메타데이터 모델은 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션에 계속 표시되지만 더 이상 사용되지 않습니다. 후속 릴리스에서 제거될 예정입니다. 사용자는 **탐색기** 기능 영역에서 더 이상 메타데이터를 볼 수 없으며 더 이상 메타데이터 모델 버전을 만들 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014에서 지원되지 않는 MDS(Master Data Services) 기능](discontinued-master-data-services-features.md)  
  
  
