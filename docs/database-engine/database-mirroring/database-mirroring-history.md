---
title: "데이터베이스 미러링 기록 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mirroring
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.dbmmonitor.databasemirroringhistory.f1
ms.assetid: 1d6e4b10-4a23-47d7-9918-c417992f09d3
caps.latest.revision: "25"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3e3bf2700f9570a41f07d18d376332080daa99cd
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="database-mirroring-history"></a>데이터베이스 미러링 기록
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 대화 상자를 사용하여 지정된 서버 인스턴스의 미러링된 데이터베이스에 대한 미러링 상태 기록을 볼 수 있습니다.  
  
 **SQL Server Management Studio를 사용하여 데이터베이스 미러링을 모니터링하려면**  
  
-   [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="options"></a>변수  
 **서버 인스턴스**  
 기록이 보고되고 있는 서버 인스턴스의 이름입니다.  
  
 **데이터베이스 백업**  
 해당 기록이 보고되고 있는 데이터베이스의 이름입니다.  
  
 **목록 필터 기준**  
 필터 값을 나열합니다. 새 값을 선택하면 표가 자동으로 새로 고쳐집니다.  
  
 가능한 필터 값은 다음과 같습니다.  
  
-   마지막 2시간  
  
-   마지막 4시간  
  
-   마지막 8시간  
  
-   마지막 1일  
  
-   마지막 2일  
  
-   마지막 100개의 레코드  
  
-   마지막 500개의 레코드  
  
-   마지막 1000개의 레코드  
  
-   모든 레코드  
  
 **새로 고침**  
 기록 목록을 새로 고치려면 클릭합니다.  
  
> [!NOTE]  
>  이 대화 상자는 기록 목록을 자동으로 새로 고치지 않습니다. 목록을 새로 고치려면 **새로 고침** 을 클릭하거나 다른 필터 옵션을 선택합니다. **sysadmin** 고정 서버 역할의 멤버만 미러링 기록을 업데이트할 수 있습니다.  
  
 **기록**  
 기록 목록을 표시합니다. 열 머리글을 클릭하면 해당 열을 기준으로 표가 정렬됩니다. 목록에는 다음 열이 있습니다.  
  
|열 이름|Description|  
|-----------------|-----------------|  
|**기록된 시간**|기록 행의 타임스탬프입니다.|  
|**역할**|이 데이터베이스에 대한 서버 인스턴스의 현재 미러링 역할(주 서버 또는 미러 서버)입니다.|  
|**미러링 상태**|데이터베이스의 상태입니다.<br /><br /> 연결 끊김<br /><br /> 장애 조치(Failover) 보류 중<br /><br /> 일시 중지됨<br /><br /> 동기화됨<br /><br /> 동기화 중<br /><br /> Unknown|  
|**미러링 모니터 서버 연결**|데이터베이스의 미러링 세션에 있는 미러링 모니터 서버 연결의 상태입니다(연결됨 또는 연결 끊김). 미러링 모니터 서버가 없을 경우 값은 NULL입니다.|  
|**보내지 않은 로그**|주 서버 인스턴스의 Send Queue에 있는 보내지 않은 로그의 크기(KB)입니다.|  
|**전송 시간**|주 서버 인스턴스에서 현재 Send Queue에 있는 로그를 미러 서버 인스턴스에 보내는 데 필요한 대략적인 시간입니다( *전송 속도*). 들어오는 트랜잭션의 속도가 크게 달라질 수 있으므로 로그 전송 시간은 예상 시간입니다. 그러나 전송 속도는 수동 장애 조치에 필요한 대략적인 시간을 예상하는 데 유용할 수 있습니다.|  
|**Send Rate**|트랜잭션이 미러 서버 인스턴스로 전송되는 속도(KB/초)입니다.|  
|**새 트랜잭션 속도**|들어오는 트랜잭션이 주 서버의 로그에 들어오는 속도(KB/초)입니다. 미러링 속도가 늦는지, 보통인지 또는 빠른지를 확인하려면 이 값을 **전송 시간** 값과 비교합니다.|  
|**보내지 않은 가장 오래된 트랜잭션**|Send Queue에 있는 보내지 않은 가장 오래된 트랜잭션의 보존 기간입니다. 이 트랜잭션의 보존 기간은 트랜잭션이 미러 서버 인스턴스에 전송되지 않은 채로 경과된 시간(분)을 나타냅니다. 이 값은 시간을 기준으로 발생 가능한 데이터 손실을 측정하는 데 도움이 됩니다.|  
|**복원되지 않은 로그**|Redo Queue에서 대기 중인 로그의 양(KB)입니다.|  
|**복원 시간**|현재 Redo Queue에 있는 로그를 미러 데이터베이스에 적용하는 데 필요한 대략적인 시간(분)입니다.|  
|**복원 속도**|트랜잭션이 미러 데이터베이스로 복원되는 속도(KB/초)입니다.|  
|**미러 커밋 오버헤드**|트랜잭션당 평균 지연 시간(밀리초)입니다(동기 모드에만 해당). 이 지연 시간은 주 서버 인스턴스에서 미리 서버 인스턴스가 트랜잭션 로그 레코드를 Redo Queue에 쓸 때까지 대기하는 동안 발생한 오버헤드 양입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [데이터베이스 미러링 보안 구성 마법사 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
  
