---
title: "미러된 데이터베이스 상태 보기(SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mirroring
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- states [SQL Server], database mirroring
- database mirroring [SQL Server], states
ms.assetid: 544f4194-253e-4c57-96ca-31c16301434f
caps.latest.revision: "25"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2f4a85274aa0f8c971ee59a816913786fad5ea84
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="view-the-state-of-a-mirrored-database-sql-server-management-studio"></a>미러된 데이터베이스의 상태 보기(SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 데이터베이스 미러링 세션 동안 **데이터베이스 속성** 대화 상자의 **미러링** 페이지에서 상태를 확인할 수 있습니다.  
  
### <a name="to-view-the-status-of-a-database-mirroring-session"></a>데이터베이스 미러링 세션 상태를 보려면  
  
1.  주 서버 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 미러링할 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 선택한 다음 **미러**를 클릭합니다. **데이터베이스 속성** 대화 상자의 **미러링** 페이지가 열립니다.  
  
4.  미러링이 시작된 다음 **상태** 패널에는 **미러링** 페이지를 선택하거나 **새로 고침** 단추를 클릭한 경우와 같은 데이터베이스 미러링 세션 상태가 표시됩니다. 가능한 상태는 다음과 같습니다.  
  
    |상태|설명|  
    |------------|-----------------|  
    |\<비어 있음>|데이터베이스 미러링 세션이 없으며 **미러링** 페이지에 대해 보고할 활동이 없습니다.|  
    |일시 중지됨|주 데이터베이스가 실행되고 있지만 미러 서버로 로그를 보내지 않습니다. 데이터베이스의 미러 복사본을 사용할 수 없습니다.|  
    |연결 없음|주 서버 인스턴스는 해당 파트너나 미러링 모니터 서버 인스턴스(있는 경우)에 연결할 수 없습니다.|  
    |동기화 중|미러 데이터베이스의 내용이 주 데이터베이스의 내용보다 오래된 것입니다. 주 서버 인스턴스에서 로그 레코드를 미러 서버 인스턴스로 보내면 미러 서버 인스턴스에서 변경 사항을 미러 데이터베이스에 적용하여 롤포워드합니다.<br /><br /> 데이터베이스 미러링 세션을 시작할 때는 미러 데이터베이스와 주 데이터베이스가 동기화하는 중입니다.|  
    |장애 조치|주 서버 인스턴스에서 수동 장애 조치(역할 교체)가 시작되었지만 미러 서버 인스턴스에서 아직 수락하지 않았습니다.|  
    |동기화됨|미러 데이터베이스에 주 데이터베이스와 동일한 데이터가 들어 있습니다. 수동 장애 조치와 자동 장애 조치는 동기화 *상태에서만* 가능합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [미러링 상태&#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
  
