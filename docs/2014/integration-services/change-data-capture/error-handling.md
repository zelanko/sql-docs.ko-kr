---
title: 오류 처리 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ff79e19d-afca-42a4-81b0-62d759380d11
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e9bebcc588a3ccbe522d4747bab2428f5e30973a
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379421"
---
# <a name="error-handling"></a>오류 처리
  Oracle CDC 인스턴스는 단일 Oracle 원본 데이터베이스에서 변경 사항을 마이닝하고(Oracle RAC 클러스터가 단일 데이터베이스로 간주됨) 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 CDC 데이터베이스에 있는 변경 테이블에 커밋된 변경 내용을 기록합니다.  
  
 **cdc.xdbcdc_state**시스템 테이블에서 CDC 인스턴스의 상태가 유지됩니다. 언제든지 이 테이블을 쿼리하여 CDC 인스턴스의 상태를 확인할 수 있습니다. cdc.xdbcdc_state 테이블에 대한 자세한 내용은 [cdc.xdbcdc_state](the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_state)를 참조하세요.  
  
 다음 표에서는 xdbcdc_state 테이블의 CDC 인스턴스 상태에 대해 설명합니다.  
  
 각 상태에 대해 cdc.xdbcdc_state 테이블의 해당 열에 다음과 같이 두 가지 표시가 제공됩니다.  
  
-   인스턴스가 활성화되지 않았습니다(현재 Windows 프로세스에서 인스턴스를 처리 중이 아님). **active** 열의 값이 1이면 이 특정 Oracle CDC 인스턴스를 처리 중인 Oracle CDC Service의 하위 프로세스가 실행 중인 것입니다.  
  
-   **error** 열의 값이 0이면 Oracle CDC 인스턴스가 오류 상태에 있지 않은 것입니다. **error** 열의 값이 1이면 Oracle CDC 인스턴스가 변경 내용을 처리하지 못하게 하는 오류가 발생한 것입니다.  
  
     **error** 열과 **active** 열의 값이 모두 1이면 Oracle CDC 인스턴스에 대해 자동으로 해결될 수 있는 복구할 수 있는 오류가 발생한 것입니다. error 열의 값은 1이고 active 열의 값은 0이면 대부분의 경우 문제를 수동으로 해결한 다음 처리를 다시 시작할 수 있습니다.  
  
 다음 표에서는 Oracle CDC 인스턴스가 상태 테이블에 보고할 수 있는 다양한 상태 코드에 대해 설명합니다.  
  
|상태|활성 상태 코드|오류 상태 코드|설명|  
|------------|------------------------|-----------------------|------------------|  
|ABORTED|0|1|Oracle CDC 인스턴스가 실행되고 있지 않습니다. ABORTED 하위 상태는 Oracle CDC 인스턴스가 ACTIVE 상태에서 예기치 않게 중지되었음을 나타냅니다.<br /><br /> ABORTED 하위 상태는 Oracle CDC 인스턴스가 ACTIVE 상태에서 실행되고 있지 않을 때 Oracle CDC Service 기본 인스턴스에 의해 설정됩니다.|  
|error|0|1|Oracle CDC 인스턴스가 실행되고 있지 않습니다. ERROR 상태는 CDC 인스턴스가 ACTIVE 상태이지만 복구할 수 없는 오류가 발생하여 사용하지 않도록 설정되었음을 나타냅니다. ERROR 상태는 다음과 같은 하위 상태 코드를 포함합니다.<br /><br /> MISCONFIGURED: 복구할 수 없는 구성 오류가 감지되었습니다.<br /><br /> PASSWORD-REQUIRED: Attunity Oracle CDC Designer에 대해 설정된 암호가 없거나 구성된 암호가 잘못되었습니다. 서비스 비대칭 키 암호 변경이 원인일 수 있습니다.|  
|RUNNING|1|0|CDC 인스턴스가 실행 중이며 변경 레코드를 처리하고 있습니다. RUNNING 상태는 다음과 같은 하위 상태 코드를 포함합니다.<br /><br /> IDLE: 모든 변경 레코드가 처리 되어 대상 컨트롤에 저장 된 (**_CT**) 테이블입니다. 제어 테이블이 있는 활성 트랜잭션이 없습니다.<br /><br /> PROCESSING: 컨트롤에 아직 기록 되지 않은 처리 중인 변경 레코드가 있습니다 (**_CT**) 테이블입니다.|  
|STOPPED|0|0|CDC 인스턴스가 실행되고 있지 않습니다. STOP 하위 상태는 CDC 인스턴스가 ACTIVE 상태에서 올바르게 중지되었음을 나타냅니다.|  
|SUSPENDED|1|1|CDC 인스턴스가 실행되고 있지만 복구할 수 있는 오류로 인해 처리가 일시 중지되었습니다. SUSPENDED 상태는 다음과 같은 하위 상태 코드를 포함합니다.<br /><br /> DISCONNECTED: 원본 Oracle 데이터베이스에 연결할 수 없습니다. 연결이 복원되면 처리가 다시 시작됩니다.<br /><br /> STORAGE: 저장소가 꽉 찼습니다. 스토리지를 사용할 수 있게 되면 처리가 다시 시작됩니다. 경우에 따라 상태 테이블을 업데이트할 수 없기 때문에 이 상태가 나타나지 않을 수 있습니다.<br /><br /> LOGGER: 로거가 Oracle에 연결되어 있지만 일시적인 문제로 인해 Oracle 트랜잭션 로그를 읽을 수 없습니다.|  
|DATAERROR|x|x|이 상태 코드는 **xdbcdc_trace** 테이블에 대해서만 사용됩니다. **xdbcdc_state** 테이블에는 이 상태가 나타나지 않습니다. 추적 레코드에 이 상태가 있으면 Oracle 로그 레코드에 문제가 있는 것입니다. 잘못된 로그 레코드가 **data** 열에 BLOB으로 저장됩니다. DATAERROR 상태는 다음과 같은 하위 상태 코드를 포함합니다.<br /><br /> BADRECORD: 연결된 로그 레코드를 구문 분석할 수 없습니다.<br /><br /> CONVERT-ERROR: 일부 열의 데이터를 캡처 테이블의 대상 열로 변환할 수 없습니다. 이 상태는 변환 오류가 발생하면 추적 레코드를 생성하도록 구성에 지정된 경우에만 나타날 수 있습니다.|  
  
 Oracle CDC Service 상태는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장되므로 데이터베이스의 상태 값에 서비스의 실제 상태가 반영되지 않는 경우도 있습니다. 가장 일반적인 시나리오로는 서비스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결이 끊어져서 서비스를 다시 시작할 수 없는 경우가 있습니다. 이 경우 **cdc.xdbcdc_state** 에 이전 상태가 저장되어 있습니다. 마지막 업데이트 타임스탬프(UTC)가 1분을 초과하는 경우 상태가 오래되었을 수 있습니다. 이 경우 Windows 이벤트 뷰어를 사용하여 서비스 상태에 대한 추가 정보를 확인하십시오.  
  
## <a name="error-handling"></a>오류 처리  
 이 섹션에서는 Oracle CDC Service에서 오류를 처리하는 방법에 대해 설명합니다.  
  
### <a name="logging"></a>로깅  
 Oracle CDC Service는 다음 위치 중 하나에서 오류 정보를 만듭니다.  
  
-   Windows 이벤트 로그: 오류를 기록하는 데 사용되며 Oracle CDC Service 수명 주기 이벤트(대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 시작, 중지, 연결 및 다시 연결)를 나타냅니다.  
  
-   MSXDBCDC.dbo.xdbcdc_trace 테이블: Oracle CDC Service 주 프로세스의 일반 로깅 및 추적에 사용됩니다.  
  
-   \<cdc-database>.cdc.xdbcdc_trace 테이블: Oracle CDC 인스턴스의 일반 로깅 및 추적에 사용됩니다. 특정 Oracle CDC 인스턴스 관련 오류가 해당 인스턴스의 추적 테이블에 기록된다는 것을 의미합니다.  
  
 다음과 같은 경우에 Oracle CDC Service에 의해 정보가 기록됩니다.  
  
-   서비스 제어 관리자가 서비스를 시작하거나 중지한 경우  
  
-   연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 없으며 오류가 발생한 이후에 성공적으로 연결된 경우  
  
-   Oracle CDC Service 인스턴스를 시작하는 중에 오류가 발생한 경우  
  
-   Oracle CDC 인스턴스가 중단된 경우  
  
-   오류가 발생한 경우  
  
 다음과 같은 경우에 CDC 인스턴스에 의해 정보가 기록됩니다.  
  
-   인스턴스를 사용 또는 사용 안 함으로 설정할 때  
  
-   오류가 발생한 경우  
  
-   복구할 수 있는 오류에서 복구된 경우  
  
 추적 테이블은 문제 해결을 위해 자세한 추적 정보를 기록하는 데에도 사용됩니다.  
  
### <a name="handling-source-oracle-connection-errors"></a>원본 Oracle 연결 오류 처리  
 Oracle CDC Service는 원본 Oracle 데이터베이스와 지속적으로 연결되어야 합니다. 서비스 구성과 관련 없는 대부분의 연결 오류(예: 네트워킹 오류)는 일시적인 것으로 간주됩니다. 따라서 Oracle CDC Service에서 연결 해제 후에 작업을 시작하거나 작업 중에 Oracle 데이터베이스에 연결할 수 없는 경우 서비스의 상태가 SUSPENDED/DISCONNECTED로 변경되고 연결이 정기적으로 다시 시도되는 다시 시도 루프가 시작됩니다. 다시 연결되면 처리가 계속됩니다.  
  
 다른 유형의 연결 오류(예: 잘못된 자격 증명, 권한 부족, 잘못된 데이터베이스 주소 등)는 일시적인 오류가 아닙니다. 이러한 오류가 발생하면 Oracle CDC Service 상태가 ERROR/MISCONFIGURED 또는 ERROR/PASSWORD-REQUIRED로 설정되고 서비스를 사용할 수 없습니다. 사용자가 기본 오류를 수정할 때 처리를 다시 시작하도록 Oracle CDC 인스턴스를 수동으로 다시 설정해야 합니다.  
  
 일시적인 오류인지 확실하지 않은 경우 일시적인 오류라고 가정하는 것이 좋습니다.  
  
### <a name="handling-target-sql-server-connection-errors"></a>대상 SQL Server 연결 오류 처리  
 Oracle CDC Service는 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 지속적으로 연결해야 합니다. 이 연결은 다음과 같은 용도로 사용됩니다.  
  
-   현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 사용 중인 동일한 이름을 가진 다른 서비스가 없는지 확인합니다.  
  
-   사용 또는 사용 안 함으로 설정된 Oracle CDC 인스턴스를 확인하고 하위 프로세스를 시작 또는 중지합니다.  
  
 서비스가 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결되어 있고 이 이름으로 사용 중인 유일한 Oracle CDC Service일 때 사용하도록 설정된 Oracle CDC 인스턴스를 확인하고 처리 중인 프로세스(서비스에서 비활성화된 프로세스를 중단한 경우)를 시작할 수 있습니다. Oracle CDC 인스턴스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결을 사용하여 Oracle CDC 인스턴스의 CDC 데이터베이스 작업을 수행합니다.  
  
 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 연결이 실패한 경우에 오류를 처리하는 방법은 오류가 일시적인 오류인지 여부에 따라 달라집니다.  
  
 일시적이지 않은 알려진 오류(예: 잘못된 자격 증명, 권한 부족, 잘못된 연결 정보)인 경우 서비스는 Windows 이벤트 로그에 오류를 기록하고 중지됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 수 없기 때문에 추적 테이블에 오류를 기록할 수 없습니다. 이 경우 사용자가 오류를 해결하고 Oracle CDC Windows 서비스를 다시 시작해야 합니다.  
  
 일시적인 오류 및 예기치 못한 오류의 경우 작업이 여러 번 다시 시도되고 오류가 오래 동안 지속될 경우 CDC Service에서 CDC 인스턴스 하위 프로세스를 중지하고 초기 연결 시도로 돌아갑니다. 이 때 다른 시스템의 Oracle CDC Service에서 명명된 CDC Service를 이미 제어하고 있을 수 있습니다.  
  
### <a name="handling-target-sql-server-storage-full-errors"></a>대상 SQL Server 스토리지 꽉 참 오류 처리  
 Oracle CDC Service는 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 데이터베이스에 새 변경 데이터를 삽입할 수 없을 경우 이벤트 로그에 경고를 기록하고 추적 레코드 삽입을 다시 시도합니다. 그렇지만 이 시도도 동일한 이유로 실패할 수 있습니다. 그런 다음 작업이 성공할 때까지 특정 간격으로 작업을 다시 시도합니다.  
  
### <a name="handling-oracle-cdc-errors"></a>Oracle CDC 오류 처리  
 Oracle CDC 인스턴스는 Oracle 트랜잭션 로그를 읽은 다음 처리합니다. CDC 처리 중에 오류가 발생하면 **cdc.xdbcdc_state** 테이블에 오류가 보고되며 사용자가 보고된 오류를 기반으로 수동으로 작업해야 합니다.  
  
 예를 들어 Oracle CDC 인스턴스를 오래 동안 활성화할 수 없고 필요한 Oracle 트랜잭션 로그 파일을 더 이상 사용할 수 없는 경우가 있습니다. 이 경우 Oracle DBA는 Oracle CDC 인스턴스에서 처리를 다시 시작하는 데 필요한 로그를 복원해야 합니다.  
  
### <a name="handling-unexpected-oracle-cdc-instance-failures"></a>예기치 않은 Oracle CDC 인스턴스 오류 처리  
 Oracle CDC Service는 CDC 인스턴스 하위 프로세스를 모니터링합니다. CDC 인스턴스 하위 프로세스가 중단되면 CDC Service는 MSXDBCDC.dbo.xdbcdc_databases 테이블에서 해당 프로세스를 비활성화하고 cdc.xdbcdc_state 상태를 ABORTED로 업데이트합니다. 이 경우 표준 Windows 오류 보고 대화 상자는 추가 분석을 위해 이 오류를 보고하는 데 사용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [Change Data Capture Designer for Oracle by Attunity](change-data-capture-designer-for-oracle-by-attunity.md)   
 [Oracle CDC 인스턴스](the-oracle-cdc-instance.md)  
  
  
