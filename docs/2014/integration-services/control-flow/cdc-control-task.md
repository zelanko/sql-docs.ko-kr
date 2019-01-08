---
title: CDC 제어 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdccontroltask.f1
ms.assetid: 6404dc7f-550c-47cc-b901-c072742f430a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fbac13f1d65a984a90ffbeb3ee0b1ae4e0cec719
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376085"
---
# <a name="cdc-control-task"></a>CDC 제어 태스크
  CDC 제어 태스크는 CDC(변경 데이터 캡처) 패키지의 수명 주기를 제어하는 데 사용됩니다. 이 태스크를 사용하면 초기 로드 패키지와의 CDC 패키지 동기화, CDC 패키지 실행 시 처리되는 LSN(로그 시퀀스 번호) 범위의 관리가 처리됩니다. 또한 CDC 제어 태스크는 오류 시나리오 및 복구를 다룹니다.  
  
 CDC 제어 태스크는 CDC 패키지의 상태를 SSIS 패키지 변수에 유지합니다. 그러나 이 태스크는 여러 패키지 활성화와 일반적인 CDC 프로세스(예를 들어 한 태스크는 초기 로드를 수행하고 다른 태스크는 trickle-feed 업데이트를 수행할 수 있음)를 함께 수행하는 여러 패키지 간에 상태가 유지되도록 데이터베이스 테이블에 상태를 유지할 수도 있습니다.  
  
 CDC 제어 태스크는 두 작업 그룹을 지원합니다. 한 그룹은 초기 로드와 변경 처리의 동기화를 처리하며 다른 그룹은 CDC 패키지 실행에 대해 LSN의 변경 처리 범위를 관리하고 처리된 항목을 추적합니다.  
  
 다음 작업은 초기 로드와 변경 처리의 동기화를 처리합니다.  
  
|연산|Description|  
|---------------|-----------------|  
|ResetCdcState|이 작업은 현재 CDC 컨텍스트에 연결된 영구 CDC 상태를 다시 설정하는 데 사용됩니다. 이 작업을 실행하면 LSN 타임스탬프 `sys.fn_cdc_get_max_lsn` 테이블의 현재 최대 LSN이 다음 처리 범위의 시작 부분이 됩니다. 이 작업을 수행하려면 원본 데이터베이스에 대한 연결이 필요합니다.|  
|MarkInitialLoadStart|이 작업은 초기 로드 패키지의 시작 부분에서 초기 로드 패키지가 원본 테이블을 읽기 시작하기 전에 현재 LSN을 원본 데이터베이스에 기록하기 위해 사용됩니다. 이 작업을 수행하려면 `sys.fn_cdc_get_max_lsn`을 호출하기 위해 원본 데이터베이스에 대한 연결이 필요합니다.<br /><br /> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC(즉, Oracle이 아님)에서 작업할 때 MarkInitialLoadStart를 선택하는 경우 연결 관리자에 지정된 사용자는 db_owner 또는 sysadmin이어야 합니다.|  
|MarkInitialLoadEnd|이 작업은 초기 로드 패키지의 끝 부분에서 초기 로드 패키지가 원본 테이블 읽기를 완료한 후 현재 LSN을 원본 데이터베이스에 기록하기 위해 사용됩니다. 이 LSN은 이 작업이 발생한 현재 시간을 기록한 후 CDC 데이터베이스에서 해당 시간 이후에 발생한 변경 내용을 조회하는 `cdc.lsn_time_`매핑 테이블을 쿼리하여 결정됩니다.<br /><br /> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC(즉, Oracle이 아님)에서 작업할 때 MarkInitialLoadEnd를 선택하는 경우 연결 관리자에 지정된 사용자는 db_owner 또는 sysadmin이어야 합니다.|  
|MarkCdcStart|이 작업은 스냅숏 데이터베이스에서 초기 로드가 생성될 때 사용됩니다. 이 경우 스냅숏 LSN 후에 변경 처리가 즉시 시작되어야 합니다. 사용자가 사용할 스냅숏 데이터베이스의 이름을 지정하면 CDC 제어 태스크가 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에 스냅숏 LSN을 쿼리합니다. 사용자가 스냅숏 LSN을 직접 지정할 수도 있습니다.<br /><br /> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC(즉, Oracle이 아님)에서 작업할 때 MarkCdcStart를 선택하는 경우 연결 관리자에 지정된 사용자는 db_owner 또는 sysadmin이어야 합니다.|  
  
 처리 범위를 관리하는 데에는 다음과 같은 작업이 사용됩니다.  
  
|연산|Description|  
|---------------|-----------------|  
|GetProcessingRange|이 작업은 CDC 원본 데이터 흐름을 사용하는 데이터 흐름을 호출하기 전에 사용됩니다. 이 작업은 호출될 때 CDC 원본 데이터 흐름에서 읽는 LSN의 범위를 설정합니다. 범위는 데이터 흐름을 처리하는 동안 CDC 원본에서 사용되는 SSIS 패키지 변수에 저장됩니다.<br /><br /> 저장된 상태에 대한 자세한 내용은 [상태 변수 정의](../data-flow/define-a-state-variable.md)를 참조하세요.|  
|MarkProcessedRange|: 이 작업은 각 CDC 실행 후(CDC 데이터 흐름이 성공적으로 완료된 후) CDC 실행 중에 완전히 처리된 마지막 LSN을 기록하기 위해 실행됩니다. 다음에 GetProcessingRange를 실행하면 이 위치가 처리 범위의 시작 부분이 됩니다.|  
  
## <a name="handling-cdc-state-persistency"></a>CDC 상태 지속성 처리  
 CDC 제어 태스크는 활성화 간에 영구 상태를 유지합니다. CDC 상태에 저장되는 정보는 CDC 패키지의 처리 범위를 결정 및 유지하고 오류 상태를 검색하는 데 사용됩니다. 영구 상태는 문자열로 저장됩니다. 자세한 내용은 [상태 변수 정의](../data-flow/define-a-state-variable.md)를 참조하세요.  
  
 CDC 제어 태스크는 두 가지 유형의 상태 지속성을 지원합니다.  
  
-   수동 상태 지속성: 이 경우 CDC 제어 태스크가 패키지 변수에 저장된 상태를 관리하지만 패키지 개발자가 CDC 제어를 호출하기 전에 영구 저장소에서 변수를 읽은 다음 CDC 제어가 마지막으로 호출되고 CDC 실행이 완료된 후에 해당 영구 저장소에 변수를 다시 써야 합니다.  
  
-   자동 상태 지속성: CDC 상태가 데이터베이스의 테이블에 저장됩니다. 상태는 **상태를 저장하는 데 사용할 테이블** 속성(상태 저장을 위해 선택한 연결 관리자에 있음)으로 지정한 테이블의 **StateName** 속성에 제공된 이름으로 저장됩니다. 기본값은 원본 연결 관리자이지만 대상 연결 관리자를 사용하는 것이 일반적입니다. CDC 제어 태스크는 상태 테이블에서 상태 값을 업데이트하며 이는 앰비언트 트랜잭션의 일환으로 커밋됩니다.  
  
## <a name="error-handling"></a>오류 처리  
 CDC 제어 태스크는 다음과 같은 경우 오류를 보고할 수 있습니다.  
  
-   영구 CDC 상태를 읽지 못하거나 영구 상태를 업데이트하지 못할 경우  
  
-   원본 데이터베이스에서 현재 LSN 정보를 읽지 못할 경우  
  
-   CDC 상태 읽기가 일관되지 않을 경우  
  
 이러한 모든 경우 CDC 제어 태스크는 오류를 보고합니다. 이러한 오류는 SSIS가 제어 흐름 오류를 처리하는 표준 방식으로 처리할 수 있습니다.  
  
 CDC 제어 태스크는 처리된 범위 표시가 호출되지 않은 채 처리 범위 가져오기 작업 직후에 다른 처리 범위 가져오기 작업이 호출될 때도 경고를 보고할 수 있습니다. 이는 이전 실행이 실패했거나 동일한 CDC 상태 이름을 사용하는 다른 CDC 패키지가 실행되고 있을 수 있음을 나타냅니다.  
  
## <a name="configuring-the-cdc-control-task"></a>CDC 제어 태스크 구성  
 SSIS 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [CDC 제어 태스크 편집기](../cdc-control-task-editor.md)  
  
-   [CDC 제어 태스크 사용자 지정 속성](cdc-control-task-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 [상태 변수 정의](../data-flow/define-a-state-variable.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   social.technet.microsoft.com의 기술 문서, [Attunity Oracle을 위한 Microsoft SQL Server 2012 변경 데이터 캡처 설치](https://go.microsoft.com/fwlink/?LinkId=252958)  
  
-   social.technet.microsoft.com의 기술 문서, [Attunity Oracle용 Microsoft 변경 데이터 캡처의 구성 문제 해결](https://go.microsoft.com/fwlink/?LinkId=252960)  
  
-   social.technet.microsoft.com의 기술 문서, [Attunity Oracle용 Microsoft 변경 데이터 캡처의 CDC 인스턴스 오류 문제 해결](https://go.microsoft.com/fwlink/?LinkId=252961)  
  
  
