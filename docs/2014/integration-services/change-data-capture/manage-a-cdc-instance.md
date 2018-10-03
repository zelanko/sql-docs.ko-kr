---
title: CDC 인스턴스 관리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- manIns
ms.assetid: cfed22c8-c666-40ca-9e73-24d93e85ba92
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c51d2242ec06b4cb68cb054f9214566b0dbf3946
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099283"
---
# <a name="manage-a-cdc-instance"></a>CDC 인스턴스 관리
  CDC Designer 콘솔을 사용하여 직접 만든 인스턴스에 대한 정보를 보고 인스턴스 작업을 관리할 수 있습니다.  
  
 왼쪽 창에서 인스턴스의 이름을 클릭하여 인스턴스에 대한 정보를 볼 수 있습니다.  
  
> [!NOTE]  
>  또한 왼쪽 창에서 서비스를 선택하면 사용 가능한 인스턴스의 목록이 CDC Designer 콘솔의 가운데에 표시됩니다. 이 섹션에서 인스턴스 중 하나를 선택한 경우 오른쪽 창에서 태스크를 수행할 수 있지만 속성 탭에서 정보를 볼 수 없습니다.  
  
## <a name="what-you-can-do-when-you-display-the-cdc-instance-information"></a>CDC 인스턴스 정보를 표시할 때 수행할 수 있는 작업  
 오른쪽 창에서 수행되는 동작은 다음과 같습니다.  
  
 **시작**  
 **시작** 을 클릭하여 선택한 CDC 인스턴스에 대한 변경 캡처를 시작할 수 있습니다.  
  
 **중지**  
 **중지** 를 클릭하여 선택한 CDC 인스턴스에 대한 변경 캡처를 중지할 수 있습니다. CDC 인스턴스를 중지할 경우 해당 시점에 캡처된 변경 사항은 손실되지 않고 CDC 인스턴스를 다시 시작하면 제공됩니다.  
  
 **다시 설정**  
 **다시 설정** 을 클릭하여 CDC 인스턴스를 초기(비어 있음) 상태로 다시 설정합니다. 이 옵션은 CDC 인스턴스가 중지된 경우에 사용할 수 있습니다. 변경 테이블의 모든 변경 사항과 CDC 인스턴스 내부 상태가 삭제됩니다. CDC 인스턴스를 나중에 시작하면 변경 캡처가 해당 시점부터 시작되고 CDC 인스턴스가 시작된 후에 시작된 트랜잭션만 포함됩니다.  
  
 확인 대화 상자에서 **확인** 을 클릭하여 CDC 인스턴스를 다시 설정하고 변경 테이블에 기록된 변경 사항을 삭제하도록 확인할 수 있습니다.  
  
 **Delete**  
 **삭제** 를 클릭하여 CDC 인스턴스를 영구히 삭제할 수 있습니다. 이 옵션은 CDC 인스턴스가 중지된 경우에만 사용할 수 있습니다.  
  
 확인 대화 상자에서 **확인** 을 클릭하여 CDC 인스턴스를 삭제하도록 확인할 수 있습니다.  
  
 **Oracle 로깅 스크립트**  
 이 링크를 클릭하여 Oracle 로깅 스크립트 대화 상자를 Oracle 보완 로깅 스크립트와 함께 표시할 수 있습니다. 이 대화 상자에서 수행할 수 있는 작업에 대한 자세한 내용은 [Oracle Supplemental Logging Script](oracle-supplemental-logging-script.md)를 참조하십시오.  
  
> [!NOTE]  
>  보완 로깅 스크립트를 실행하면 유효한 Oracle 사용자 이름과 암호를 입력할 수 있는 스크립트 실행을 위한 Oracle 자격 증명 대화 상자가 열립니다. 적절한 Oracle 자격 증명을 제공하는 방법은 [Oracle Credentials for Running Script](oracle-credentials-for-running-script.md)을 참조하십시오.  
  
 **CDC 인스턴스 배포 스크립트**  
 이 링크를 클릭하면 CDC 인스턴스 배포 스크립트가 표시된 CDC 인스턴스 배포 스크립트 대화 상자가 표시됩니다. 이 대화 상자에 대한 자세한 내용은 [CDC Instance Deployment Script](cdc-instance-deployment-script.md)를 참조하십시오.  
  
 **Properties**  
 이 링크를 클릭하여 속성 편집기를 열 수 있습니다. 속성 편집기를 사용하여 CDC 인스턴스 구성을 편집합니다. CDC 인스턴스에 대한 속성을 편집하는 방법은 [Edit Instance Properties](edit-instance-properties.md)을 참조하십시오.  
  
 **뷰어 탭**  
  
 CDC 인스턴스에 대한 정보를 볼 때 다음 뷰어 탭을 사용할 수 있습니다. 이러한 탭에 표시된 정보는 읽기 전용입니다.  
  
 **상태**  
 이 탭은 CDC 인스턴스의 현재 상태에 대한 정보와 통계를 제공합니다. 포함되는 정보는 다음과 같습니다.  
  
-   **상태**: CDC 인스턴스의 현재 상태를 나타내는 아이콘입니다. 다음과 같이 상태를 설명합니다.  
  
    |||  
    |-|-|  
    |![오류](../media/error.gif "오류")|**오류**: 다시 시도할 수 없는 오류가 발생하여 Oracle CDC 인스턴스가 실행되지 않습니다. 다음과 같은 하위 상태를 사용할 수 있습니다.<br /><br /> **잘못 구성됨**: 수동 작업이 필요한 구성 오류가 발생했습니다.<br /><br /> **암호 필요**: Oracle CDC 인스턴스에 대해 암호를 설정하지 않았거나 암호가 올바르지 않습니다.<br /><br /> **예기치 않은 오류**: 복구할 수 없는 다른 모든 오류입니다.|  
    |![확인](../media/okay.gif "확인")|**실행 중**: CDC 인스턴스가 실행 중이며 변경 레코드를 처리하고 있습니다. 다음과 같은 하위 상태를 사용할 수 있습니다.<br /><br /> **유휴 상태**: 모든 변경 레코드가 처리되어 대상 변경 테이블에 저장되었습니다. 활성 트랜잭션이 더 이상 없습니다.<br /><br /> **처리 중**: 변경 테이블에 아직 기록되지 않은 처리 중인 변경 레코드가 있습니다.|  
    |![중지](../media/stop.gif "중지")|**중지됨**: CDC 인스턴스가 실행되고 있지 않습니다. 중지됨 상태는 CDC 인스턴스가 정상적인 방법으로 중지되었음을 나타냅니다.|  
    |![일시 중지](../media/paused.gif "일시 중지")|**일시 중지됨**: CDC 인스턴스가 실행되고 있지만 다시 실행 가능한 오류로 인해 처리가 일시 중지되었습니다. 다음과 같은 하위 상태를 사용할 수 있습니다.<br /><br /> **연결 끊김**: 원본 Oracle 데이터베이스에 연결할 수 없습니다. 연결이 복원되면 처리가 다시 시작됩니다.<br /><br /> **저장소**: 저장소가 꽉 찼습니다. 추가 저장소를 사용할 수 있게 되면 처리가 다시 시작됩니다.<br /><br /> **로거**: 로거가 Oracle에 연결되어 있지만 일시적인 문제(예: 필요한 트랜잭션 로그를 사용할 수 없음)로 인해 Oracle 트랜잭션 로그를 읽을 수 없습니다.|  
  
-   **자세한 상태**: 현재 하위 상태입니다.  
  
-   **상태 메시지**: 현재 상태에 대한 자세한 정보를 제공합니다.  
  
-   **타임스탬프**: 상태 테이블에서 CDC 상태를 마지막으로 읽은 UTC 시간입니다.  
  
-   **현재 처리 중**: 이 섹션에서 다음 정보를 모니터링합니다.  
  
    -   **마지막 트랜잭션 타임스탬프**: 변경 테이블에 기록된 마지막 트랜잭션의 현지 시간입니다.  
  
    -   **마지막 변경 타임스탬프**: 원본 Oracle 데이터베이스 트랜잭션 로그에서 Oracle CDC 인스턴스에 의해 표시된 최신 변경의 현지 시간입니다. Oracle 트랜잭션 로그를 읽을 때 CDC 인스턴스의 현재 대기 시간에 대한 정보를 제공합니다.  
  
    -   **트랜잭션 로그 헤드 CN**: Oracle 트랜잭션 로그에서 읽은 최신 CN(변경 번호)입니다.  
  
    -   **트랜잭션 비상 로그CN**: CDC 인스턴스를 복구하거나 다시 시작하기 위한 변경 번호입니다. Oracle CDC 인스턴스는 다시 시작되거나 다른 유형의 오류(예: 클러스터 장애 조치)가 발생할 경우 이 위치로 다시 설정됩니다.  
  
    -   **현재 CN**: 원본 Oracle 데이터베이스(트랜잭션 로그 아님)에 표시된 마지막 변경 번호(SCN)입니다.  
  
    -   **활성 트랜잭션**: Oracle CDC 인스턴스에서 처리 중인 아직 결정(커밋/롤백)되지 않은 원본 Oracle 트랜잭션의 현재 번호입니다.  
  
    -   **준비된 트랜잭션**: [cdc.xdbcdc_staged_transactions](the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_staged_transactions) 테이블에 준비되어 있는 원본 Oracle 트랜잭션의 현재 번호입니다.  
  
-   **카운터**: 이 섹션에서 다음 정보를 모니터링합니다.  
  
    -   **료된 트랜잭션**: CDC 인스턴스를 마지막으로 다시 설정한 이후에 완료된 트랜잭션의 수입니다. 관련 테이블을 포함하지 않는 트랜잭션은 포함되지 않습니다.  
  
    -   **기록된 변경**: SQL Server 변경 테이블에 기록된 변경 사항의 수입니다.  
  
 **Oracle**  
 CDC 인스턴스 및 Oracle 데이터베이스에 대한 연결 관련 정보를 표시합니다. 이 탭은 읽기 전용입니다. 이 속성을 편집하려면 왼쪽 창에서 인스턴스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택하거나 오른쪽 창에서 **속성**을 클릭하여 \<instance> 속성 대화 상자를 엽니다.  
  
 이러한 속성에 대한 자세한 내용과 속성을 편집하는 방법은 [Edit the Oracle Database Properties](edit-the-oracle-database-properties.md)을 참조하십시오.  
  
 **테이블**  
 CDC 인스턴스에 포함된 테이블에 대한 정보를 표시합니다. 여기에서 열 정보도 사용할 수 있습니다. 이 탭은 읽기 전용입니다. 이 속성을 편집하려면 왼쪽 창에서 인스턴스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택하거나 오른쪽 창에서 **속성**을 클릭하여 \<instance> 속성 대화 상자를 엽니다.  
  
 이러한 속성에 대한 자세한 내용과 속성을 편집하는 방법은 [Edit Tables](edit-tables.md)을 참조하십시오.  
  
 **고급**  
 CDC 인스턴스에 대한 고급 속성과 속성 값을 표시합니다. 이 탭은 읽기 전용입니다. 이 속성을 편집하려면 왼쪽 창에서 인스턴스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택하거나 오른쪽 창에서 **속성**을 클릭하여 \<instance> 속성 대화 상자를 엽니다.  
  
 이러한 속성에 대한 자세한 내용과 속성을 편집하는 방법은 [Edit the Advanced Properties](edit-the-advanced-properties.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 변경 데이터베이스 인스턴스를 만드는 방법](how-to-create-the-sql-server-change-database-instance.md)   
 [CDC 인스턴스 속성을 보는 방법](how-to-view-the-cdc-instance-properties.md)   
 [CDC 인스턴스 속성을 편집 하는 방법](how-to-edit-the-cdc-instance-properties.md)   
 [새 인스턴스 마법사 사용](use-the-new-instance-wizard.md)  
  
  
