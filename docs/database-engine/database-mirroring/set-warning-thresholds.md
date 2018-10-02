---
title: 경고 임계값 설정 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dbmmonitor.setwarningthreshold.f1
ms.assetid: 17f93147-e7d9-4092-b4c2-c11b38051171
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2883f607a56da0e30067180854c289625ae11dd0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47753913"
---
# <a name="set-warning-thresholds"></a>경고 임계값 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 대화 상자를 사용하여 **데이터베이스 미러링 모니터** 대화 상자의 탐색 트리에서 선택한 데이터베이스에 대한 하나 이상의 경고 임계값을 설정 및 구성할 수 있습니다.  
  
 이 대화 상자는 두 서버 인스턴스에 연결을 시도합니다. 이러한 연결은 비동기적으로 설정됩니다. 이 대화 상자에는 각 파트너의 연결 상태가 표시됩니다. 파트너가 연결되지 않은 경우 **연결**을 클릭할 수 있습니다.  
  
 **SQL Server Management Studio를 사용하여 데이터베이스 미러링을 모니터링하려면**  
  
-   [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="options"></a>Options  
 *서버 인스턴스 및 서버 인스턴스의 연결 상태*  
 *SYSTEM***\\***INSTANCE_NAME*형식으로 된 파트너 서버 인스턴스의 이름입니다. 기본 서버 인스턴스의 경우 시스템 이름만 표시됩니다.  
  
 또한 이 필드는 모니터가 이 서버 인스턴스에 현재 연결되어 있는지 여부를 나타냅니다. 가능한 연결 상태는 다음과 같습니다.  
  
-   *server_instance_name***에 연결되지 않음**  
  
-   *server_instance_name***에 연결하는 중**  
  
-   *server_instance_name***에 연결됨**  
  
    > [!NOTE]  
    >  **sysadmin** 고정 서버 역할의 멤버가 아닌 경우 이 상태는 *server_instance_name***에 연결됨****(제한된 사용 권한)** 입니다.  
  
 각 파트너 서버 인스턴스의 이름이 별도의 *서버 인스턴스 및 서버 인스턴스의 연결 상태* 필드에 표시됩니다. 모니터 실행이 시작되면 맨 위 필드에 주 서버가 나열됩니다.  
  
 **연결**/**취소**  
 **연결**/**취소** 단추는 각 *서버 인스턴스 및 서버 인스턴스의 연결 상태* 필드와 연결되어 있습니다. 단추의 상태는 연결 상태에 따라 달라집니다.  
  
-   서버 인스턴스에 대한 연결이 없을 경우 단추 텍스트는 **연결**입니다. 서버 인스턴스에 연결하려면 클릭합니다.  
  
-   연결 시도가 진행 중이면 단추 텍스트는 **취소**입니다. 연결 시도를 취소하려면 클릭합니다.  
  
-   서버가 연결된 경우 단추 텍스트는 **연결됨**이고 단추는 흐리게 표시됩니다.  
  
 **임계값**  
 **임계값** 표에는 두 서버 인스턴스에 대한 경고 설정이 표시됩니다.  
  
> [!NOTE]  
>  서버 인스턴스가 연결되지 않은 경우 해당 열에는 빈 셀과 회색 배경이 표시됩니다. 연결이 열리면 해당 인스턴스의 내용이 표에 자동으로 표시됩니다.  
  
 표에는 다음 열이 있습니다.  
  
 **경고**  
 지원되는 경고를 나열합니다.  
  
|경고|설명|  
|-------------|-----------------|  
|**보내지 않은 로그가 임계값을 초과하는 경우 경고**|임계값은 주 서버의 Send Queue에 있는 보내지 않은 로그의 크기(KB)를 나타냅니다.|  
|**복원되지 않은 로그가 임계값을 초과하는 경우 경고**|임계값은 미러 서버 인스턴스에 있는 Redo Queue의 크기(KB)를 나타냅니다.|  
|**보내지 않은 가장 오래된 트랜잭션 기간이 임계값을 초과하는 경우 경고**|임계값은 Send Queue에서 미러 서버 인스턴스로 아직 보내지 않은 트랜잭션의 시간(분)을 나타냅니다. 이 값은 시간을 기준으로 발생 가능한 데이터 손실을 측정하는 데 도움이 됩니다.|  
|**미러 커밋 오버헤드가 임계값을 초과하는 경우 경고**|임계값은 트랜잭션당 지연 시간(밀리초)을 나타냅니다(보호 우선 모드에만 관련됨). 이 지연 시간은 주 서버 인스턴스에서 미리 서버 인스턴스가 트랜잭션 로그 레코드를 Redo Queue에 쓸 때까지 대기하는 동안 발생한 오버헤드 양입니다.|  
  
 **'** *\<서버 인스턴스>* **'에서 활성화됨**  
 빈 확인란은 서버 인스턴스에서 경고가 현재 비활성화되었음을 나타냅니다. 경고를 활성화하려면 해당 확인란을 클릭합니다.  
  
 **'** *\<서버 인스턴스>* **'의 임계값**  
 경고가 활성화된 경우 이 열의 왼쪽에서 임계값을 설정합니다. 상태 테이블을 업데이트할 때 지정된 임계값에 도달한 경우 이벤트가 발생합니다. 값을 구성한 후 임계값을 비활성화하면 해당 값은 이 필드에 남아 있으며 경고를 다시 활성화할 경우 사용됩니다.  
  
 경고가 활성화되지 않은 경우 이 필드는 비활성 상태입니다.  
  
 **확인**  
 **확인** 을 클릭하면 이 대화 상자가 닫히고 경고 임계값의 현재 지정된 값이 **경고** 탭 페이지의 **임계값**표에 표시됩니다.  
  
## <a name="remarks"></a>Remarks  
 임계값은 한 번에 한 파트너에만 적용할 수 있지만 데이터베이스가 장애 조치될 경우 경고가 유지되도록 두 파트너 모두에 지정된 이벤트에 대한 임계값을 설정하는 것이 좋습니다. 각 파트너에 적합한 임계값은 각 파트너 시스템의 성능 기능에 따라 달라집니다.  
  
 상태 테이블을 업데이트할 때 해당 값이 임계값보다 크거나 같을 경우에만 성능의 이벤트 로그에 이벤트가 기록됩니다. 상태 업데이트 사이에 최대값이 일시적으로 임계값에 도달할 경우 해당 값은 누락됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [데이터베이스 미러링 보안 구성 마법사 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
  
