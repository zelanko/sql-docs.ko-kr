---
title: 데이터베이스 미러링 모니터 시작(SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- monitoring database mirroring [SQL Server]
- Database Mirroring Monitor [SQL Server], starting
- database mirroring [SQL Server], monitoring
ms.assetid: 53165335-97ca-4f88-8e78-22f1839dee98
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 48773b6f4fadf810f62f681cde45bfcb78206e53
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37205713"
---
# <a name="start-database-mirroring-monitor-sql-server-management-studio"></a>데이터베이스 미러링 모니터 시작(SQL Server Management Studio)
  데이터베이스 미러링 모니터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 시작한 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]모니터의 일부입니다.  
  
> [!NOTE]  
>  일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서는 데이터베이스 미러링 모니터를 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
### <a name="to-launch-the-database-mirroring-monitor"></a>데이터베이스 미러링 모니터를 시작하려면  
  
1.  주 서버 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 모니터링할 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 선택한 다음 **데이터베이스 미러링 모니터 시작**을 클릭합니다.  
  
4.  **데이터베이스 미러링 모니터** 대화 상자에서 **미러된 데이터베이스 등록** 을 클릭하여 미러된 데이터베이스를 하나 이상 등록합니다.  
  
    > [!NOTE]  
    >  한 파트너에서 데이터베이스를 등록하면 다른 파트너에서 해당 데이터베이스가 자동으로 등록됩니다. 모니터에 이미 다른 파트너 인스턴스에 대한 연결 자격 증명이 있으면 연결 시 해당 자격 증명이 사용됩니다. 그렇지 않으면 모니터는 Windows 인증을 사용하여 연결을 시도합니다. 서버 인스턴스 중 하나에 연결하는 데 사용되는 자격 증명을 변경하려는 경우 **[확인]을 클릭할 때 [서버 연결 관리] 대화 상자 표시**를 클릭합니다.  
  
 데이터베이스 미러링 모니터에 대한 자세한 내용은 [데이터베이스 미러링 모니터 개요](database-mirroring-monitor-overview.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 미러링&#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
  
