---
title: Oracle CDC 데이터베이스 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a96486e9-f79b-4b24-bfaf-56203dd0e435
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a4743cd96f3075915bb2ed1071f781e1787cf9b6
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728511"
---
# <a name="the-oracle-cdc-databases"></a>Oracle CDC 데이터베이스

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Oracle CDC 인스턴스는 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 동일한 이름으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 연결됩니다. 이 데이터베이스를 Oracle CDC 데이터베이스 또는 CDC 데이터베이스라고 합니다.  
  
 CDC 데이터베이스는 Oracle CDC Designer 콘솔을 사용하여 만들고 구성하며 다음과 같은 요소를 포함합니다.  
  
-   SQL Server CDC에 데이터베이스를 사용하여 만드는 `cdc` 스키마  
  
-   Oracle CDC 인스턴스에서 사용하는 **cdc.xdbcdc_xxxx** 테이블 집합  
  
-   원본 Oracle 데이터베이스에서 캡처된 테이블에 대한 정의를 포함하는 빈 미러 테이블 집합  
  
-   SQL Server CDC 메커니즘에 의해 생성되고 Oracle 이외의 일반 SQL Server CDC에서 사용되는 것과 동일한 변경 테이블 및 변경 액세스 기능 집합  
  
 처음에는 `cdc` dbowner **고정 데이터베이스 역할의 멤버만** 스키마에 액세스할 수 있습니다. 변경 테이블 및 변경 기능에 대한 액세스는 SQL Server CDC와 동일한 보안 모델에 의해 결정됩니다. 보안 모델에 대한 자세한 내용은 [보안 모델](https://go.microsoft.com/fwlink/?LinkId=231151)을 참조하세요.  
  
## <a name="creating-the-cdc-database"></a>CDC 데이터베이스 만들기  
 대부분의 경우 CDC 데이터베이스는 CDC Designer 콘솔을 사용하여 만들지만, CDC Designer 콘솔을 사용하여 생성되는 CDC 배포 스크립트를 사용하여 만들 수도 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자는 필요한 경우 항목(예: 스토리지, 보안 또는 가용성)에 대한 데이터베이스 설정을 변경할 수 있습니다.  
  
 CDC Designer 콘솔을 사용하여 데이터베이스 테이블 및 필요한 스크립트를 만드는 방법에 대한 자세한 내용은 [새 인스턴스 마법사 사용](../../integration-services/change-data-capture/use-the-new-instance-wizard.md)을 참조하세요.  
  
## <a name="cdc-database-user-roles"></a>CDC 데이터베이스 사용자 역할  
 CDC 데이터베이스를 만들고 CDC에 사용하면 **cdc_service** 라는 데이터베이스 사용자가 CDC 데이터베이스에 만들어진 다음 Oracle CDC Service를 구성할 때 사용한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 연결됩니다. 이 사용자는 **db_datareader**, **db_datawriter**및 **db_ddladmin** 데이터베이스 역할의 멤버가 됩니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 `dbo` 사용자에 연결되면 **cdc_service** 가 만들어지지 않습니다.  
  
 이 역할 할당을 통해 Oracle CDC Service에서 `cdc` 스키마의 테이블을 캡처된 데이터 및 제어 정보로 업데이트할 수 있습니다.  
  
 CDC 데이터베이스가 만들어지고 CDC 원본 Oracle 테이블이 설정된 경우 CDC 데이터베이스 소유자는 미러 테이블의 SELECT 권한을 부여하고 SQL Server CDC 제어 역할을 정의하여 변경 데이터에 액세스하는 사용자를 제어할 수 있습니다.  
  
## <a name="mirror-tables"></a>미러 테이블  
 Oracle 원본 데이터베이스의 각 캡처된 테이블(\<schema-name>.\<table-name>)에 대해 동일한 스키마와 테이블 이름을 가진 유사한 빈 테이블이 CDC 데이터베이스에 만들어집니다. `cdc` 의 `cdc` 스키마는 SQL Server CDC용으로 예약되어 있으므로 스키마 이름이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (대/소문자 구분 없음)인 Oracle 원본 데이터베이스를 캡처할 수 없습니다.  
  
 미러 테이블은 비어 있고 데이터가 저장되어 있지 않습니다. 미러 테이블은 Oracle CDC 인스턴스에 사용되는 표준 SQL Server CDC 인프라를 사용하도록 설정하는 데 사용됩니다. 미러 테이블에서 데이터가 삽입되거나 업데이트되지 않도록 모든 UPDATE, DELETE 및 INSERT 작업이 PUBLIC에 대해 거부됩니다. 따라서 미러 테이블에서 데이터를 수정할 수 없습니다.  
  
## <a name="access-to-change-data"></a>변경 데이터 액세스  
 캡처 인스턴스에 연결된 변경 데이터에 액세스하는 데 사용되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 모델 때문에 연결된 미러 테이블의 모든 캡처된 열에 대한 `select` 권한을 사용자에게 부여해야 합니다. 원본 Oracle 테이블에 대한 액세스 권한으로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 변경 테이블에 액세스할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 모델에 대한 자세한 내용은 [보안 모델](https://go.microsoft.com/fwlink/?LinkId=231151)을 참조하세요.  
  
 또한 캡처 인스턴스를 만들 때 제어 역할을 지정한 경우 호출자도 지정된 제어 역할의 멤버여야 합니다. 메타데이터에 액세스하는 다른 일반적인 변경 데이터 캡처 함수에 모든 데이터베이스 사용자가 PUBLIC 역할을 통해 액세스할 수 있습니다. 물론 반환된 메타데이터에 대한 액세스는 기본 원본 테이블에 대한 선택적 액세스 권한을 사용하거나 정의된 제어 역할의 멤버 자격을 통해 일반적으로 제어됩니다.  
  
 캡처 인스턴스를 만들 때 SQL Server CDC 구성 요소에 의해 생성된 특수 테이블 기반 함수를 호출하여 변경 데이터를 읽을 수 있습니다. 이 함수에 대한 자세한 내용은 [변경 데이터 캡처 함수(Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=231152)를 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] CDC 원본 구성 요소를 통한 CDC 데이터 액세스에도 동일한 규칙이 적용됩니다.  
  
## <a name="the-cdc-database-tables"></a>CDC 데이터베이스 테이블  
 이 섹션에서는 CDC 데이터베이스의 다음 테이블에 대해 설명합니다.  
  
-   [변경 테이블(_CT)](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_Change_Tables_CT)  
  
-   [cdc.lsn_time_mapping](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdclsn_time_mapping)  
  
-   [cdc.xdbcdc_config](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_config)  
  
-   [cdc.xdbcdc_state](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_state)  
  
-   [cdc.xdbcdc_trace](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_trace)  
  
-   [cdc.xdbcdc_staged_transactions](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_staged_transactions)  
  
###  <a name="BKMK_Change_Tables_CT"></a> 변경 테이블(_CT)  
 변경 테이블은 미러 테이블에서 만들어집니다. 변경 테이블은 Oracle 데이터베이스에서 캡처되는 변경 데이터를 포함합니다. 테이블은 다음 규칙에 따라 이름이 지정됩니다.  
  
 **[cdc].[\<capture-instance>_CT]**  
  
 `<schema-name>.<table-name>`테이블에 캡처를 처음 사용하는 경우 기본 캡처 인스턴스 이름은 `<schema-name>_<table-name>`입니다. 예를 들어 Oracle HR.EMPLOYEES 테이블에 대한 기본 캡처 인스턴스 이름은 HR_EMPLOYEES이고 연결된 변경 테이블은 [cdc]입니다. [HR_EMPLOYEES_CT].  
  
 캡처 테이블은 Oracle CDC 인스턴스에 의해 기록됩니다. 캡처 인스턴스를 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 의해 생성되는 특수 테이블 반환 함수를 사용하여 캡처 테이블을 읽습니다. `fn_cdc_get_all_changes_HR_EMPLOYEES`)을 입력합니다. 이러한 CDC 함수에 대한 자세한 내용은 [변경 데이터 캡처 함수(Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=231152)를 참조하세요.  
  
###  <a name="BKMK_cdclsn_time_mapping"></a> cdc.lsn_time_mapping  
 **[cdc].[lsn_time_mapping]** 테이블은 SQL Server CDC 구성 요소에 의해 생성됩니다. Oracle CDC에서의 캡처 테이블 사용은 일반적인 사용과는 다릅니다.  
  
 Oracle CDC의 경우 이 테이블에 저장되는 LSN 값은 변경과 연결된 Oracle SCN(System Change Number) 값을 기반으로 합니다. LSN 값의 처음 6바이트는 원본 Oracle SCN 수입니다.  
  
 또한 Oracle CDC를 사용하는 경우 시간 열(`tran_begin_time` 및 `tran_end_time`)에는 일반 SQL Server CDC에서와 달리 현지 시간이 아닌 변경의 UTC 시간이 저장됩니다. 따라서 일광 절약 시간 변경은 lsn_time_mapping에 저장된 데이터에 영향을 주지 않습니다.  
  
###  <a name="BKMK_cdcxdbcdc_config"></a> cdc.xdbcdc_config  
 이 테이블에는 Oracle CDC 인스턴스에 대한 구성 데이터가 포함되어 있습니다. 이 테이블은 CDC Designer 콘솔을 사용하여 업데이트합니다. 이 테이블에는 행이 하나만 있습니다.  
  
 다음 표에서는 **cdc.xdbcdc_config** 테이블 열에 대해 설명합니다.  
  
|항목|설명|  
|----------|-----------------|  
|version|CDC 인스턴스 구성의 버전을 추적합니다. 테이블이 업데이트되거나, 새 캡처 인스턴스가 추가되거나, 기존 캡처 인스턴스가 제거될 때마다 업데이트됩니다.|  
|connect_string|Oracle 연결 문자열입니다. 기본 예:<br /><br /> `<server>:<port>/<instance>` (예: `erp.contoso.com:1521/orcl`)<br /><br /> 연결 문자열에서 Oracle Net 연결 설명자를 지정할 수도 있습니다(예: `(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp) (HOST=erp.contoso.com) (PORT=1521)) (CONNECT_DATA=(SERVICE_NAME=orcl)))`)<br /><br /> 디렉터리 서버 또는 tnsnames를 사용하는 경우 연결 문자열이 연결의 이름일 수 있습니다.<br /><br /> Oracle CDC Service에서 사용되는 Oracle Instant Client에 대한 Oracle 데이터베이스 연결 문자열에 대한 자세한 내용은 [https://go.microsoft.com/fwlink/?LinkId=231153](https://go.microsoft.com/fwlink/?LinkId=231153)을 참조하세요.|  
|use_windows_authentication|부울 값이며 다음과 같습니다.<br /><br /> **0**: Oracle 사용자 이름 및 암호가 인증을 위해 제공됩니다(기본값).<br /><br /> **1**: Oracle 데이터베이스에 연결하는 데 Windows 인증이 사용됩니다. Windows 인증을 사용하도록 Oracle 데이터베이스를 구성한 경우에만 이 옵션을 사용할 수 있습니다.|  
|username|로그 마이닝 Oracle 데이터베이스 사용자의 이름입니다. **use_windows_authentication = 0인 경우**에만 필수입니다.|  
|password|로그 마이닝 Oracle 데이터베이스 사용자의 암호입니다. **use_windows_authentication = 0**인 경우에만 필수입니다.|  
|transaction_staging_timeout|커밋되지 않은 Oracle 트랜잭션이 **cdc.xdbcdc_staged_transactions** 테이블에 기록되기 전에 메모리에 보관되는 시간(초)입니다. 기본값은 120초입니다.|  
|memory_limit|메모리에 데이터를 캐시하는 데 사용할 수 있는 메모리 양에 대한 제한입니다. 설정값이 낮을수록 더 많은 트랜잭션이 **cdc.xdbcdc_staged_transactions** 테이블에 기록됩니다. 기본값은 50MB입니다.|  
|옵션|이름[=값][; ] 형태의 옵션 목록이며 보조 옵션(예: 추적, 튜닝)을 지정하는 데 사용됩니다. 사용 가능한 옵션에 대한 설명은 아래 표를 참조하십시오.|  
  
 다음 표에서는 사용 가능한 옵션에 대해 설명합니다.  
  
|속성|Default|최소값|최대값|정적|설명|  
|----------|-------------|---------|---------|------------|-----------------|  
|추적|False|-|-|False|사용 가능한 값은<br /><br /> True<br /><br /> False<br /><br /> on<br /><br /> off|  
|cdc_update_state_interval|10|1|120|False|트랜잭션에 대해 할당된 메모리 청크의 크기(KB)입니다. 트랜잭션 하나가 둘 이상의 청크를 할당할 수 있습니다. [cdc.xdbcdc_config](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_config) 테이블의 memory_limit 열을 참조하세요.|  
|target_max_batched_transactions|100|1|1000|True|SQL Server CT 테이블 업데이트에서 하나의 트랜잭션으로 처리될 수 있는 최대 Oracle 트랜잭션 수입니다.|  
|target_idle_lsn_update_interval|10|0|1|False|캡처된 테이블에서 활동이 없을 때 **lsn_time_mapping** 테이블을 업데이트하는 간격(초)입니다.|  
|trace_retention_period|24|1|24*31|False|추적 테이블에서 메시지를 유지하는 시간입니다.|  
|sql_reconnect_interval|2|2|3600|False|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하기 전에 대기할 시간(초)입니다. 이 간격은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 연결 제한 시간과 함께 사용됩니다.|  
|sql_reconnect_limit|-1|-1|-1|False|최대 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다시 연결 횟수입니다. 기본값 -1은 프로세스가 중지될 때까지 재연결을 시도함을 의미합니다.|  
|cdc_restart_limit|6|-1|3600|False|대부분의 경우 CDC Service는 비정상적으로 종료된 CDC 인스턴스를 자동으로 다시 시작합니다. 이 속성은 인스턴스를 다시 시작하기 위해 서비스가 중지되는 오류가 발생하는 시간당 횟수를 정의합니다. 값이 -1이면 인스턴스를 항상 다시 시작합니다.<br /><br /> 구성 테이블을 업데이트한 후에 인스턴스를 다시 시작하도록 서비스가 반환됩니다.|  
|cdc_memory_report|0|0|1000|False|매개 변수 값이 변경된 경우 CDC 인스턴스는 추적 테이블에 메모리 보고서를 인쇄합니다.|  
|target_command_timeout|600|1|3600|False|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용되는 명령 제한 시간입니다.|  
|source_character_set|-|-|-|True|Oracle 데이터베이스 코드 페이지 대신 특정 Oracle 인코딩을 사용하도록 설정할 수 있습니다. 문자 데이터에서 사용 중인 실제 인코딩이 Oracle 데이터베이스 코드 페이지에 표현된 것과 다를 때 사용할 수 있습니다.|  
|source_error_retry_interval|30|1|3600|False|여러 오류(예: 연결 오류, 시스템 테이블 간의 일시적인 동기화 부족)에 대해 다시 시도하기 전에 사용됩니다.|  
|source_prefetch_size|100|1|10000|True|사전 인출 일괄 처리의 크기입니다.|  
|source_max_tables_in_query|100|1|10000|True|테이블을 필터링하지 않고 Oracle 로그 읽기로 전환하기 전에 WHERE 절에 허용되는 최대 테이블 수입니다.|  
|source_read_retry_interval|2|1|3600|False|EOF에서 Oracle 트랜잭션 로그 읽기를 다시 시도하기 전에 원본에서 대기하는 시간입니다.|  
|source_reconnect_interval|30|1|3600|False|원본 데이터베이스에 다시 연결하려고 시도하기 전에 대기하는 시간(초)입니다.|  
|source_reconnect_limit|-1|-1||False|원본 데이터베이스를 다시 연결하는 최대 횟수입니다. 기본값 -1은 프로세스가 중지될 때까지 다시 연결하려고 시도하는 것을 의미합니다.|  
|source_command_timeout|30|1|3600|False|Oracle에 적용되는 연결 제한 시간입니다.|  
|source_connection_timeout|30|1|3600|False|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 적용되는 연결 제한 시간입니다.|  
|trace_data_errors|True|-|-|False|Boolean입니다. **True** 이면 데이터 변환과 잘림 오류를 기록합니다.|  
|CDC_stop_on_breaking_schema_changes|False|-|-|False|Boolean입니다. **True** 이면 주요 스키마 변경이 감지되는 경우에 중지합니다.<br /><br /> **False** 이면 미러 테이블과 캡처 인스턴스를 삭제합니다.|  
|source_oracle_home||-|-|False|CDC 인스턴스가 Oracle에 연결하는 데 사용할 특정 Oracle 홈 경로 또는 Oracle 홈 이름으로 설정할 수 있습니다.|  
  
###  <a name="BKMK_cdcxdbcdc_state"></a> cdc.xdbcdc_state  
 이 테이블에는 Oracle CDC 인스턴스의 지속된 상태에 대한 정보가 포함되어 있습니다. 캡처 상태는 복구 및 장애 조치 시나리오에서 상태 모니터링에 대해 사용됩니다.  
  
 다음 표에서는 **cdc.xdbcdc_state** 테이블 열에 대해 설명합니다.  
  
|항목|설명|  
|----------|-----------------|  
|상태|현재 Oracle CDC 인스턴스에 대한 현재 상태 코드입니다. 상태는 CDC의 현재 상태를 설명합니다.|  
|sub_status|현재 상태에 대한 추가 정보를 제공하는 두 번째 수준 상태입니다.|  
|active|부울 값이며 다음과 같습니다.<br /><br /> **0**: Oracle CDC 인스턴스 프로세스가 활성 상태가 아닙니다.<br /><br /> **1**: Oracle CDC 인스턴스 프로세스가 활성 상태입니다.|  
|error|부울 값이며 다음과 같습니다.<br /><br /> **0**: Oracle CDC 인스턴스 프로세스가 오류 상태가 아닙니다.<br /><br /> **1**: Oracle CDC 인스턴스가 오류 상태입니다.|  
|status_message|오류 또는 상태에 대해 설명하는 문자열입니다.|  
|TIMESTAMP|캡처 상태를 마지막으로 업데이트한 시간(UTC)이 포함된 타임스탬프입니다.|  
|active_capture_node|Oracle 트랜잭션 로그를 처리 중인 Oracle CDC Service 및 Oracle CDC 인스턴스를 현재 실행 중인 호스트의 이름입니다. 호스트는 클러스터 내의 노드일 수 있습니다.|  
|last_transaction_timestamp|마지막 트랜잭션이 변경 테이블에 기록된 시간(UTC)이 포함된 타임스탬프입니다.|  
|last_change_timestamp|원본 Oracle 트랜잭션 로그에서 최신 변경 레코드를 읽은 시간(UTC)이 포함된 타임스탬프입니다. 이 타임스탬프를 통해 CDC 프로세스의 현재 대기 시간을 식별할 수 있습니다.|  
|transaction_log_head_cn|Oracle 트랜잭션 로그에서 읽은 최신 CN(변경 번호)입니다.|  
|transaction_log_tail_cn|다시 시작하거나 복구할 때 Oracle CDC 인스턴스의 위치를 변경할 Oracle 트랜잭션 로그의 CN(변경 번호)입니다.|  
|current_cn|원본 데이터베이스에 있는 것으로 알려진 최신 CN(변경 번호)입니다.|  
|software_version|Oracle CDC Service의 내부 버전입니다.|  
|completed_transactions|CDC를 마지막으로 다시 설정한 이후에 처리된 트랜잭션의 수입니다.|  
|written_changes|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변경 테이블에 기록된 변경 레코드의 수입니다.|  
|read_changes|원본 Oracle 트랜잭션 로그에서 읽은 변경 레코드의 수입니다.|  
|staged_transactions|**cdc.xdbcdc_staged_transactions** 테이블에서 준비된 현재 활성 트랜잭션 수입니다.|  
  
###  <a name="BKMK_cdcxdbcdc_trace"></a> cdc.xdbcdc_trace  
 이 테이블에는 CDC 인스턴스 작업에 대한 정보가 포함되어 있습니다. 이 테이블에 저장되는 정보에는 오류 레코드, 주목할 만한 상태 변경 및 추적 레코드가 포함됩니다. **cdc.xcbcdc_trace** 테이블을 사용할 수 없는 경우에도 정보를 사용할 수 있도록 오류 정보는 Windows 이벤트 로그에도 기록됩니다.  
  
 다음 표에서는 cdc.xdbcdc_trace 테이블 열에 대해 설명합니다.  
  
|항목|설명|  
|----------|-----------------|  
|TIMESTAMP|추적 레코드가 기록된 정확한 UTC 타임스탬프입니다.|  
|유형|다음 값 중 하나가 포함됩니다.<br /><br /> error<br /><br /> INFO<br /><br /> 추적|  
|node|레코드가 기록된 노드의 이름입니다.|  
|상태|상태 테이블에서 사용되는 상태 코드입니다.|  
|sub_status|상태 테이블에서 사용되는 하위 상태 코드입니다.|  
|status_message|상태 테이블에서 사용되는 상태 메시지입니다.|  
|data|오류 또는 추적 레코드에 페이로드가 포함되는 사례에 대한 추가 데이터입니다(예: 손상된 로그 레코드).|  
  
###  <a name="BKMK_cdcxdbcdc_staged_transactions"></a> cdc.xdbcdc_staged_transactions  
 이 테이블에는 큰 트랜잭션 또는 장기 실행 트랜잭션에 대한 변경 레코드가 트랜잭션 커밋 또는 롤백 이벤트가 캡처될 때까지 저장됩니다. Oracle CDC Service는 캡처된 로그 레코드를 트랜잭션 커밋 시간을 기준으로 정렬한 다음 각 트랜잭션에 대한 시간순으로 정렬합니다. 동일한 트랜잭션에 대한 로그 레코드는 트랜잭션이 종료될 때까지 메모리에 저장되었다가 대상 변경 테이블에 기록되거나 삭제(롤백의 경우)됩니다. 사용 가능한 메모리 양이 제한되므로 대형 트랜잭션은 트랜잭션이 완료될 때까지 **cdc.xdbcdc_staged_transactions** 테이블에 기록됩니다. 트랜잭션은 오래 동안 실행될 경우 준비 테이블에도 기록됩니다. 따라서 Oracle CDC 인스턴스를 다시 시작할 때 Oracle 트랜잭션 로그에서 이전 변경 사항을 다시 읽을 필요가 없습니다.  
  
 다음 표에서는 **cdc.xdbcdc_staged_transactions** 테이블 열에 대해 설명합니다.  
  
|항목|설명|  
|----------|-----------------|  
|transaction_id|준비 중인 트랜잭션의 고유 트랜잭션 식별자입니다.|  
|seq_num|현재 트랜잭션에 대한 **xcbcdc_staged_transactions** 행의 번호입니다(0부터 시작).|  
|data_start_cn|이 행에 있는 데이터의 첫 번째 변경에 대한 CN(변경 번호)입니다.|  
|data_end_cn|이 행에 있는 데이터의 마지막 변경에 대한 CN(변경 번호)입니다.|  
|data|트랜잭션에 대해 준비된 변경 사항이며 BLOB 형태입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Change Data Capture Designer for Oracle by Attunity](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)  
  
  
