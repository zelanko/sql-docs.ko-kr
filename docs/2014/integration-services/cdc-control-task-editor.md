---
title: CDC 제어 태스크 편집기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdccontroltask.config.f1
ms.assetid: 4f09d040-9ec8-4aaa-b684-f632d571f0a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a87af3febdab1e98dac0b1546b8b2b8939b739d6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66061122"
---
# <a name="cdc-control-task-editor"></a>CDC 제어 태스크 편집기
  **CDC 제어 태스크 편집기** 대화 상자를 사용하여 CDC 제어 태스크를 구성할 수 있습니다. CDC 제어 태스크 구성에는 CDC 데이터베이스, CDC 태스크 작업 및 상태 관리 정보에 대한 연결을 정의하는 작업이 포함됩니다.  
  
 CDC 제어 태스크에 대한 자세한 내용은 [CDC Control Task](control-flow/cdc-control-task.md)를 참조하세요.  
  
 **CDC 제어 태스크 편집기를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 CDC 제어 태스크가 있는 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 패키지를 엽니다.  
  
2.  **제어 흐름** 탭에서 CDC 제어 태스크를 두 번 클릭합니다.  
  
## <a name="options"></a>옵션  
 **SQL Server CDC 데이터베이스 ADO.NET 연결 관리자**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결을 만듭니다. CDC에 사용할 수 있고 선택한 변경 테이블이 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 연결해야 합니다.  
  
 **CDC 제어 작업**  
 이 태스크에 대해 실행할 작업을 선택합니다. 모든 작업은 상태를 저장하고 패키지의 다른 구성 요소 간에 전달하는 SSIS 패키지 변수에 저장되는 상태 변수를 사용합니다.  
  
-   **초기 로드 시작 표시**: 이 작업은 스냅샷 없이 활성 데이터베이스에서 초기 로드를 실행할 때 사용됩니다. 이 작업은 초기 로드 패키지의 시작 부분에서 초기 로드 패키지가 원본 테이블을 읽기 시작하기 전에 현재 LSN을 원본 데이터베이스에 기록하기 위해 호출됩니다. 이 작업을 수행하려면 원본 데이터베이스에 대한 연결이 필요합니다.  
  
     **CDC(즉, Oracle이 아님)에서 작업할 때** 초기 로드 시작 표시 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 를 선택하는 경우 연결 관리자에 지정된 사용자는  **db_owner** 또는 **sysadmin**이어야 합니다.  
  
-   **초기 로드 끝 표시**: 이 작업은 스냅샷 없이 활성 데이터베이스에서 초기 로드를 실행할 때 사용됩니다. 이 작업은 초기 로드 패키지의 끝 부분에서 초기 로드 패키지가 원본 테이블 읽기를 완료한 후 현재 LSN을 원본 데이터베이스에 기록하기 위해 호출됩니다. 이 LSN은 이 작업이 발생한 현재 시간을 기록한 후 CDC 데이터베이스에서 해당 시간 이후에 발생한 변경 내용을 조회하는 `cdc.lsn_time_`매핑 테이블을 쿼리하여 결정됩니다.  
  
     **CDC(즉, Oracle이 아님)에서 작업할 때** 초기 로드 끝 표시 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 를 선택하는 경우 연결 관리자에 지정된 사용자는  **db_owner** 또는 **sysadmin**이어야 합니다.  
  
-   **CDC 시작 표시**: 이 작업은 스냅샷 데이터베이스 또는 정지 데이터베이스에서 초기 로드를 수행할 때 사용됩니다. 이 작업은 초기 로드 패키지 내의 어느 지점에서나 호출됩니다. 이 작업에는 스냅샷 LSN이거나 스냅샷 LSN이 자동으로 파생될 스냅샷 데이터베이스의 이름이거나 비워 둘 수 있는 매개 변수가 허용됩니다. 매개 변수를 비워둘 경우 현재 데이터베이스 LSN이 변경 내용 처리 패키지의 시작 LSN으로 사용됩니다.  
  
     이 작업은 초기 로드 시작/끝 표시 작업 대신 사용됩니다.  
  
     **CDC(즉, Oracle이 아님)에서 작업할 때** CDC 시작 표시 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 를 선택하는 경우 연결 관리자에 지정된 사용자는  **db_owner** 또는 **sysadmin**이어야 합니다.  
  
-   **처리 범위 가져오기**: 이 작업은 CDC 원본 데이터 흐름을 사용하는 데이터 흐름을 호출하기 전에 변경 내용 처리 패키지 내에서 사용됩니다. 이 작업은 호출될 때 CDC 원본 데이터 흐름에서 읽는 LSN의 범위를 설정합니다. 범위는 데이터 흐름을 처리하는 동안 CDC 원본에서 사용되는 SSIS 패키지 변수에 저장됩니다.  
  
     저장 가능한 CDC 상태에 대한 자세한 내용은 [상태 변수 정의](data-flow/define-a-state-variable.md)를 참조하세요.  
  
-   **처리된 범위 표시**: 이 작업은 CDC 실행의 끝 부분에서 CDC 데이터 흐름이 성공적으로 완료된 후 CDC 실행 중에 완전히 처리된 마지막 LSN을 기록하기 위해 변경 내용 처리 패키지에서 사용됩니다. 다음에 `GetProcessingRange` 를 실행하면 이 위치에 따라 다음 처리 범위의 시작 부분이 결정됩니다.  
  
-   **CDC 상태 다시 설정**: 이 작업은 현재 CDC 컨텍스트에 연결된 영구 CDC 상태를 다시 설정하는 데 사용됩니다. 이 작업을 실행하면 LSN 타임스탬프 `sys.fn_cdc_get_max_lsn` 테이블의 현재 최대 LSN이 다음 처리 범위의 시작 부분이 됩니다. 이 작업을 수행하려면 원본 데이터베이스에 대한 연결이 필요합니다.  
  
     이 작업을 사용하는 예로는 새로 만든 변경 레코드만 처리하고 이전 변경 레코드는 모두 무시하려는 경우가 있습니다.  
  
 **CDC 상태를 포함하는 변수**  
 태스크 작업에 대한 상태 정보를 저장하는 SSIS 패키지 변수를 선택합니다. 시작하기 전에 변수를 정의해야 합니다. **자동 상태 지속**을 선택하는 경우 상태 변수가 로드되고 자동으로 저장됩니다.  
  
 상태 변수를 정의하는 방법에 대한 자세한 내용은 [상태 변수 정의](data-flow/define-a-state-variable.md)를 참조하세요.  
  
 **CDC/스냅샷 이름을 시작하는 SQL Server LSN:**  
 CDC가 시작되는 위치를 결정하기 위해 초기 로드가 수행되는 스냅샷 데이터베이스의 이름 또는 현재 원본 데이터베이스 LSN을 입력합니다. 이 작업은 **CDC 제어 작업** 이 **CDC 시작 표시**로 설정되어 있는 경우에만 사용할 수 있습니다.  
  
 이러한 작업에 대한 자세한 내용은 [CDC Control Task](control-flow/cdc-control-task.md)를 참조하세요.  
  
 **데이터베이스 테이블에 자동으로 상태 저장**  
 CDC 제어 태스크를 통해 지정한 데이터베이스에 포함된 상태 테이블에 CDC 상태를 로드하고 저장하는 작업을 자동으로 처리하려면 이 확인란을 선택합니다. 이 확인란이 선택되어 있지 않으면 개발자가 패키지가 시작될 때 CDC 상태를 로드하고 CDC 상태가 변경될 때마다 해당 상태를 저장해야 합니다.  
  
 **상태가 저장되는 데이터베이스에 대한 연결 관리자**  
 목록에서 기존 ADO.NET 연결 관리자를 선택하거나 새로 만들기를 클릭하여 새 연결을 만듭니다. 이 연결은 상태 테이블을 포함하고 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 대한 연결입니다. 상태 테이블은 상태 정보를 포함합니다.  
  
 상태 테이블은 **자동 상태 지속** 이 선택되어 있는 경우에만 사용할 수 있으며 필수 매개 변수입니다.  
  
 **상태를 저장하는 데 사용할 테이블**  
 CDC 상태를 저장하는 데 사용할 상태 테이블의 이름을 입력합니다. 지정한 테이블에는 **이름** 열과 **상태** 열이 있어야 하며 두 열 모두 데이터 형식이 **varchar(256)** 야 합니다.  
  
 필요에 따라 **새로 만들기** 를 선택하여 필수 열이 포함된 새 상태 테이블을 작성하는 SQL 스크립트를 가져올 수도 있습니다. **자동 상태 지속** 이 선택되어 있으면 개발자가 위에 나열된 요구 사항에 따라 상태 테이블을 작성해야 합니다.  
  
 상태 테이블은 **자동 상태 지속** 이 선택되어 있는 경우에만 사용할 수 있으며 필수 매개 변수입니다.  
  
 **상태 이름**  
 영구 CDC 상태에 연결할 이름을 입력합니다. 동일한 CDC 컨텍스트를 사용하는 CDC 패키지 및 전체 로드는 일반적인 상태 이름을 지정합니다. 이 이름은 상태 테이블에서 상태 행을 조회하는 데 사용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [CDC 제어 태스크 사용자 지정 속성](control-flow/cdc-control-task-custom-properties.md)  
  
  
