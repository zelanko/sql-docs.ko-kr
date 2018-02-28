---
title: "데이터베이스 미러링 모니터(경고 페이지) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mirroring
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dbmmonitor.warningsandalerts.f1
ms.assetid: 01936122-961d-436b-ba3c-5f79fefe5469
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f150d44a28915741ffd45b4e8c4506deb41a5a51
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
---
# <a name="database-mirroring-monitor-warnings-page"></a>데이터베이스 미러링 모니터(경고 페이지)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
데이터베이스 미러링 이벤트에서 지원되는 경고와 지정된 경고 임계값(사용 가능한 경우)의 읽기 전용 목록을 표시합니다.  
  
 **SQL Server Management Studio를 사용하여 데이터베이스 미러링을 모니터링하려면**  
  
-   [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="columns"></a>열  
 **경고**  
 임계값을 정의할 수 있는 경고는 다음과 같습니다.  
  
|경고|임계값|  
|-------------|---------------|  
|**보내지 않은 로그가 임계값을 초과하는 경우 경고**|주 서버 인스턴스에서 경고를 생성하는 보내지 않은 로그의 크기(KB)를 지정합니다. 이 경고는 KB를 기준으로 발생 가능한 데이터 손실을 측정하는 데 도움이 되며 특히 성능 우선 모드와 관련이 있습니다. 그러나 파트너의 연결이 끊어져 미러링이 일시 중지되거나 일시 중단되면 이 경고는 보호 우선 모드와도 관련이 있습니다.|  
|**복원되지 않은 로그가 임계값을 초과하는 경우 경고**|미러 서버 인스턴스에서 경고를 생성하는 복원되지 않은 로그의 크기(KB)를 지정합니다. 이 경고는 KB를 기준으로 장애 조치(Failover) 시간을 측정하는 데 유용합니다. *장애 조치 시간* 은 주로 이전 미러 서버에서 Redo Queue에 남아 있는 로그를 롤포워드해야 하는 시간과 짧은 추가 시간으로 구성됩니다.<br /><br /> 참고: 자동 장애 조치의 경우 시스템이 오류를 감지하는 데 걸리는 시간은 장애 조치 시간과 관계가 없습니다.<br /><br /> 자세한 내용은 [역할 전환 중 서비스 중단 예측&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/estimate-the-interruption-of-service-during-role-switching-database-mirroring.md)프로세스를 통해 주 역할과 미러 역할을 서로 바꿀 수 있습니다.|  
|**보내지 않은 가장 오래된 트랜잭션 기간이 임계값을 초과하는 경우 경고**|주 서버 인스턴스에서 경고가 생성되기까지 Send Queue에 누적될 수 있는 트랜잭션에 해당하는 시간(분)을 지정합니다. 이 경고는 시간을 기준으로 발생 가능한 데이터 손실을 측정하는 데 도움이 되며 특히 성능 우선 모드와 관련이 있습니다. 그러나 파트너의 연결이 끊어져 미러링이 일시 중지되거나 일시 중단되면 이 경고는 보호 우선 모드와도 관련이 있습니다.|  
|**미러 커밋 오버헤드가 임계값을 초과하는 경우 경고**|주 서버에서 경고가 생성되기까지 허용되는 트랜잭션당 평균 지연 시간(밀리초)을 지정합니다. 이 지연 시간은 주 서버 인스턴스에서 미리 서버 인스턴스가 트랜잭션 로그 레코드를 Redo Queue에 쓸 때까지 대기하는 동안 발생한 오버헤드 양입니다. 이 값은 보호 우선 모드에만 해당됩니다.|  
  
 **임계값 '** *<server_instance>* **'**  
 각 경고에 대해 서버 인스턴스 중 하나에 대한 현재의 사용자 지정 임계값(있을 경우)을 표시합니다. 서버 인스턴스의 전체 인스턴스 이름이 해당 열 머리글에 표시됩니다.  
  
 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
 **임계값 설정**  
 각 장애 조치 파트너에서 경고 하나에 대한 임계값을 설정하려면 이 단추를 클릭합니다.  
  
 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
## <a name="remarks"></a>Remarks  
 서버 인스턴스에 대한 정보를 현재 사용할 수 없는 경우 해당 **임계값** 열의 셀에 회색 배경과 워터마크 텍스트가 표시됩니다. 모니터가 서버 인스턴스에 연결되지 않은 경우 인스턴스가 기본 인스턴스인지 명명된 인스턴스인지에 따라 *<SYSTEM_NAME>***에 연결되지 않음** 또는 *<SYSTEM_NAME>***\\***<instance_name>***에 연결되지 않음**이 표의 모든 셀에 표시됩니다. 모니터에서 쿼리 반환을 기다리고 있는 경우 표의 모든 셀에 **데이터를 기다리는 중...** 이 표시됩니다.  
  
 정보를 사용할 수 있는 경우 각 경고의 셀에 지정된 임계값과 측정 단위 또는 **사용 안 함**이 표시됩니다.  
  
 상태 테이블을 새로 고칠 때 임계값을 초과할 경우 상태 행이 기록될 때 Windows 이벤트 로그에 이벤트가 기록됩니다. 모니터가 실행되고 있지 않을 경우 기본적으로 1분에 한 번씩 상태 행이 기록됩니다. SQL Server 에이전트나 Microsoft MOM(Management Operations Manager)과 같은 다른 프로그램을 사용하여 각 유형의 기록된 이벤트에 대한 경고를 구성할 수 있습니다.  
  
 지정된 파트너에서 기록되는 이벤트는 현재 역할(주 서버 또는 미러 서버)에 따라 달라집니다. 그러나 데이터베이스가 장애 조치될 경우 경고가 유지되도록 두 파트너 모두에 지정된 이벤트에 대한 경고 임계값을 설정하는 것이 좋습니다. 각 파트너에 적합한 임계값은 각 파트너 시스템의 성능 기능에 따라 달라집니다.  
  
> [!NOTE]  
>  또한 **sp_dbmmonitorchangealert** 시스템 저장 프로시저를 사용하여 이러한 이벤트(보내지 않은 로그, 복구되지 않은 로그, 보내지 않은 가장 오래된 트랜잭션 및 미러 커밋 오버헤드)에 대한 임계값을 구성할 수 있습니다. 자세한 내용은 [sp_dbmmonitorchangealert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)를 참조하세요.  
  
 다음 표에서는 각 경고와 연관된 이벤트 ID를 보여 줍니다.  
  
|데이터베이스 미러링 모니터 경고|이벤트 이름|이벤트 ID|  
|----------------------------------------|----------------|--------------|  
|**보내지 않은 로그가 임계값을 초과하는 경우 경고**|보내지 않은 로그|32042|  
|**복원되지 않은 로그가 임계값을 초과하는 경우 경고**|복원되지 않은 로그|32043|  
|**보내지 않은 가장 오래된 트랜잭션 기간이 임계값을 초과하는 경우 경고**|보내지 않은 가장 오래된 트랜잭션|32044|  
|**미러 커밋 오버헤드가 임계값을 초과하는 경우 경고**|미러 커밋 오버헤드|32045|  
  
## <a name="permissions"></a>사용 권한  
 전체 액세스 권한의 경우 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다. **sysadmin** 멤버만 주요 성능 메트릭에 대해 경고 임계값을 구성하고 볼 수 있습니다.  
  
 **dbm_monitor** 역할의 멤버 자격을 사용하면 **경고** 페이지에서 최신 상태 행만 볼 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [데이터베이스 미러링 보안 구성 마법사 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
  
