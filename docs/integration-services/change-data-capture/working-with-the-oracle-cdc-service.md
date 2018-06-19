---
title: Oracle CDC Service 작업 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 04be5896-2301-45f5-a8ce-5f4ef2b69aa5
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 769ce099fc299900c93e11222f58389b2c43249b
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35332537"
---
# <a name="working-with-the-oracle-cdc-service"></a>Oracle CDC Service 작업
  이 섹션에서는 Oracle CDC Service의 몇 가지 중요한 개념에 대해 설명합니다. 이 섹션에서 설명하는 개념은 다음과 같습니다.  
  
-   [MSXDBCDC 데이터베이스](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_MSXDBCDC)  
  
     이 섹션에서는 이 데이터베이스에 포함된 테이블과 이 데이터베이스가 CDC에 어떻게 중요한지에 대해 설명합니다.  
  
-   [CDC 데이터베이스](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_CDCdatabase)  
  
     이 섹션에서는 CDC 데이터베이스에 대해 간단히 설명합니다. 이러한 데이터베이스는 Oracle CDC Designer 콘솔을 사용하여 만들어집니다. CDC 데이터베이스에 대한 자세한 내용은 CDC Designer 콘솔 설치 프로그램에 들어 있는 설명서를 참조하십시오.  
  
-   [명령줄을 사용하여 CDC Service 구성](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_CommandConfigCDC)  
  
     이 섹션에서는 Oracle CDC Service를 구성하는 데 사용할 수 있는 명령줄 명령에 대해 설명합니다.  
  
##  <a name="BKMK_MSXDBCDC"></a> MSXDBCDC 데이터베이스  
 MSXDBCDC(Microsoft External-Database CDC) 데이터베이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 Oracle CDC Service를 사용할 때 필요한 특수 데이터베이스입니다.  
  
 이 데이터베이스의 이름은 변경할 수 없습니다. MSXDBCDC라는 데이터베이스가 호스트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 존재하고 Oracle CDC Service에 정의된 것 이외의 다른 테이블을 포함하는 경우 호스트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 사용할 수 없습니다.  
  
 이 데이터베이스의 주요 용도는 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 연결된 Oracle CDC Service의 레지스트리 역할을 합니다. 이 정보는 서비스 구성과 디자인 구성 요소에 사용되며 다양한 노드에서 동일한 이름의 여러 CDC Service가 사용될 경우 어떤 서비스가 활성인지에 대한 조정을 지원하는 데 사용됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 포함된 Oracle CDC 인스턴스, 각 인스턴스를 처리하는 CDC Service 및 각 서비스에 사용되는 구성 버전 등의 레지스트리 역할을 합니다. 이 정보는 master 데이터베이스의 **sys.databases** 테이블에 있는 **is_cdc_enabled** 열과 같은 값입니다. CDC Service는 **dbo.xdbcdc_databases** 테이블을 정기적으로 검색하여 CDC 구성과 캡처된 인스턴스 목록에 대한 변경 사항을 식별합니다.  
  
-   CDC 인스턴스를 만들고 유지 관리하는 데 도움이 되는 **sysadmin**소유의 저장된 프로시저를 보관합니다. 이 역할은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 기능의 구현에 사용되는 시스템 프로시저와 비슷합니다.  
  
### <a name="creating-the-msxdbcdc-database"></a>MSXDBCDC 데이터베이스 만들기  
 Oracle CDC Service를 정의하기 전에 MSXDBCDC 데이터베이스를 만들어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 MSXDBCDC 데이터베이스를 하나만 만들 수 있습니다. MSXDBCDC 데이터베이스는 Oracle CDC용으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 준비할 때 만들어집니다. Oracle CDC Service 구성 콘솔을 사용하거나 CDC Service 구성 콘솔에서 생성되는 생성 스크립트를 실행하여 이 작업을 수행할 수 있습니다.  
  
 이 데이터베이스의 소유자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 호스팅된 Oracle CDC 인스턴스를 모두 제어할 수 있는 Oracle CDC Service 관리자입니다.  
  
 **참고 항목:**  
  
 [CDC를 위해 SQL Server를 준비하는 방법](../../integration-services/change-data-capture/how-to-prepare-sql-server-for-cdc.md)  
  
### <a name="the-msxdbcdc-database-tables"></a>MSXDBCDC 데이터베이스 테이블  
 이 섹션에서는 MSXDBCDC 데이터베이스에 있는 다음 테이블에 대해 설명합니다.  
  
-   [dbo.xdbcdc_trace](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_trace)  
  
-   [dbo.xdbcdc_databases](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_databases)  
  
-   [dbo.xdbcdc_services](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_services)  
  
###  <a name="BKMK_dboxdbcdc_trace"></a> dbo.xdbcdc_trace  
 이 테이블은 Oracle CDC Service에 대한 추적 정보를 저장합니다. 이 테이블에 저장되는 정보에는 주목할 만한 상태 변경 및 추적 레코드가 포함됩니다.  
  
 Oracle CDC Service는 Windows 이벤트 로그와 추적 테이블에 오류 레코드와 몇 가지 정보 레코드를 기록합니다. 경우에 따라 추적 테이블에 대한 액세스가 불가능할 수 있으며 이 경우 이벤트 로그에서 오류 정보에 액세스할 수 있습니다.  
  
 다음 표에서는 **dbo.xdbcdc_trace** 테이블에 포함된 항목에 대해 설명합니다.  
  
|항목|설명|  
|----------|-----------------|  
|TIMESTAMP|추적 레코드가 기록된 정확한 UTC 타임스탬프입니다.|  
|유형|다음 값 중 하나가 포함됩니다.<br /><br /> error<br /><br /> INFO<br /><br /> 추적|  
|node|레코드가 기록된 노드의 이름입니다.|  
|상태|상태 테이블에서 사용되는 상태 코드입니다.|  
|sub_status|상태 테이블에서 사용되는 하위 상태 코드입니다.|  
|status_message|상태 테이블에서 사용되는 상태 메시지입니다.|  
|원본(source)|추적 레코드를 생성한 Oracle CDC 구성 요소의 이름입니다.|  
|text_data|오류 또는 추적 레코드에 텍스트 페이로드가 포함되는 사례에 대한 추가 텍스트 데이터입니다.|  
|binary_data|오류 또는 추적 레코드에 이진 페이로드가 포함되는 사례에 대한 추가 이진 데이터입니다.|  
  
 Oracle CDC 인스턴스는 변경 테이블 보존 정책에 따라 오래된 추적 테이블 행을 삭제합니다.  
  
###  <a name="BKMK_dboxdbcdc_databases"></a> dbo.xdbcdc_databases  
 이 테이블에는 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 Oracle CDC 데이터베이스에 사용되는 CDC Service의 이름이 들어 있습니다. 각 데이터베이스는 하나의 Oracle CDC 인스턴스에 해당합니다. Oracle CDC Service는 이 테이블을 사용하여 어떤 인스턴스를 시작하거나 중지할지와 어떤 인스턴스를 다시 구성할지를 결정합니다.  
  
 다음 표에서는 **dbo.xdbcdc_databases** 테이블에 포함된 항목에 대해 설명합니다.  
  
|항목|설명|  
|----------|-----------------|  
|NAME|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 Oracle 데이터베이스의 이름입니다.|  
|config_version|해당 CDC 데이터베이스 **xdbcdc_config** 테이블의 마지막 변경에 대한 타임스탬프(UTC) 또는 이 테이블의 현재 행에 대한 타임스탬프(UTC)입니다.<br /><br /> UPDATE 트리거는 이 항목에 대한 GETUTCDATE()의 값을 적용합니다. **config_version** 을 사용하여 CDC Service에서 구성 변경 또는 설정/해제를 확인해야 할 CDC 인스턴스를 식별할 수 있습니다.|  
|cdc_service_name|이 항목은 어떤 Oracle CDC Service가 선택한 Oracle 데이터베이스를 처리할지를 결정합니다.|  
|enabled|Oracle CDC 인스턴스가 활성인지(1) 또는 비활성(0)인지를 나타냅니다. Oracle CDC Service가 시작될 때 사용(1)으로 표시된 인스턴스만 시작됩니다.<br /><br /> **참고**: Oracle CDC 인스턴스는 재시도할 수 없는 오류로 인해 비활성화될 수 있습니다. 이 경우 오류를 해결한 후 수동으로 인스턴스를 다시 시작해야 합니다.|  
  
###  <a name="BKMK_dboxdbcdc_services"></a> dbo.xdbcdc_services  
 이 테이블에는 호스트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 연결된 CDC Service가 나열됩니다. 이 테이블은 CDC Designer 콘솔에서 로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 구성된 CDC Service의 목록을 확인하는 데 사용됩니다. 이 테이블은 CDC Service에서 실행 중인 하나의 Windows 서비스에서만 지정된 Oracle CDC Service 이름이 처리되는지 확인하는 데도 사용됩니다.  
  
 다음 표에서는 **dbo.xdbcdc_databases** 테이블에 포함된 캡처 상태에 대해 설명합니다.  
  
|항목|설명|  
|----------|-----------------|  
|cdc_service_name|Oracle CDC Service의 이름(Windows 서비스 이름)입니다.|  
|cdc_service_sql_login|Oracle CDC Service에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름입니다. cdc_service라는 새 SQL 사용자가 만들어지고 이 로그인 이름에 연결된 다음 서비스에서 처리되는 각 CDC 데이터베이스에 대한 db_ddladmin, db_datareader 및 db_datawriter 고정 데이터베이스 역할의 멤버로 추가됩니다.|  
|ref_count|이 항목은 동일한 Oracle CDC Service가 설치된 컴퓨터의 수를 계산합니다. 이 항목은 동일한 이름의 Oracle 서비스가 추가될 때마다 하나씩 증가하며 이러한 서비스가 제거될 때마다 하나씩 감소합니다. 카운터가 0이 되면 이 행이 삭제됩니다.|  
|active_service_node|CDC Service를 현재 처리하는 Windows 노드의 이름입니다. 서비스가 올바르게 중지되면 이 열은 더 이상 활성 서비스가 없음을 나타내는 null로 설정됩니다.|  
|active_service_heartbeat|이 항목은 현재 CDC Service를 추적하여 아직 활성인지를 확인합니다.<br /><br /> 이 항목은 활성 CDC Service에 대한 현재 데이터베이스 UTC 타임스탬프를 사용하여 정기적인 간격으로 업데이트됩니다. 기본 간격은 30초이지만 간격을 구성할 수 있습니다.<br /><br /> 보류 중인 CDC Service에서 구성된 간격이 경과한 후 하트비트가 업데이트되지 않았음을 발견하면 보류 중인 서비스는 활성 CDC Service 역할을 넘겨 받으려고 시도합니다.|  
|옵션|이 항목은 추적 또는 튜닝과 같은 보조 옵션을 지정합니다. 이 항목은 **이름[=값][; ]** 형태로 기록됩니다. 옵션 문자열은 ODBC 연결 문자열과 동일한 의미 체계를 사용합니다. 옵션이 부울인 경우(예/아니오 값 사용) 값에는 이름만 포함될 수 있습니다.<br /><br /> 추적에 가능한 값은 다음과 같습니다.<br /><br /> **true**<br /><br /> **on**<br /><br /> **false**<br /><br /> **off**<br /><br /> **\<class name>[,class name>]**<br /><br /> <br /><br /> 기본 값은 **false**입니다.<br /><br /> **service_heartbeat_interval** 은 서비스에서 active_service_heartbeat 열을 업데이트하는 시간 간격(초)입니다. 기본값은 **30**입니다. 최대값은 **3600**입니다.<br /><br /> **service_config_polling_interval** 은 CDC Service에서 구성 변경을 확인하는 폴링 간격(초)입니다. 기본값은 **30**입니다. 최대값은 **3600**입니다.<br /><br /> **sql_command_timeout** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 명령 제한 시간입니다. 기본값은 **1**입니다. 최대값은 **3600**입니다.|  
||  
  
### <a name="the-msxdbcdc-database-stored-procedures"></a>MSXDBCDC 데이터베이스 저장 프로시저  
 이 섹션에서는 MSXDBCDC 데이터베이스에 있는 다음 저장 프로시저에 대해 설명합니다.  
  
-   [dbo.xcbcdc_reset_db(Database Name)](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxcbcdc_reset_db)  
  
-   [dbo.xdbcdc_disable_db(dbname)](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_disable_db)  
  
-   [dbo.xcbcdc_add_service(svcname,sqlusr)](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxcbcdc_add_service)  
  
-   [dbo.xdbcdc_start(dbname)](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_start)  
  
-   [dbo.xdbcdc_stop(dbname)](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_stop)  
  
###  <a name="BKMK_dboxcbcdc_reset_db"></a> dbo.xcbcdc_reset_db(Database Name)  
 이 프로시저는 Oracle CDC 인스턴스의 데이터를 지웁니다. 다음과 같은 용도로 사용됩니다.  
  
-   예를 들어 원본 데이터베이스 복구 이후 또는 일부 Oracle 트랜잭션 로그를 사용할 수 없는 비활성 상태 이후에 이전 데이터를 무시하고 데이터 캡처를 시작합니다.  
  
-   CDC 상태(특히 cdc.*tables 데이터)가 손상된 경우에 사용합니다.  
  
 **Dbo.xcbcdc_reset_db** 프로시저는 다음 태스크를 수행합니다.  
  
-   CDC 인스턴스를 중지합니다(활성인 경우).  
  
-   변경 테이블, **cdc_lsn_mapping** 테이블 및 **cdc_ddl_history** 테이블을 자릅니다.  
  
-   **cdc_xdbcdc_state** 테이블을 지웁니다.  
  
-   **cdc_change_table**의 각 행에 대한 start_lsn 열을 지웁니다.  
  
 **dbo.xcbcdc_reset_db** 프로시저를 사용하려면 사용자는 이름 지정되는 CDC 인스턴스 데이터베이스에 대한 **db_owner** 데이터베이스 역할의 멤버이거나 **sysadmin** 또는 **serveradmin** 고정 서버 역할의 멤버여야 합니다.  
  
 CDC 테이블에 대한 자세한 내용은 CDC Designer 콘솔의 도움말 시스템에서 *CDC 데이터베이스* 를 참조하세요.  
  
###  <a name="BKMK_dboxdbcdc_disable_db"></a> dbo.xdbcdc_disable_db(dbname)  
 **dbo.xcbcdc_disable_db** 프로시저는 다음 태스크를 수행합니다.  
  
-   MSXDBCDC.xdbcdc_databases 테이블에서 선택한 CDC 데이터베이스의 항목을 제거합니다.  
  
 **dbo.xcbcdc_disable_db** 프로시저를 사용하려면 사용자는 이름을 지정 중인 CDC 인스턴스에 대한 **db_owner** 데이터베이스 역할의 멤버이거나 **sysadmin** 또는 **serveradmin** 고정 서버 역할의 멤버여야 합니다.  
  
 CDC 테이블에 대한 자세한 내용은 CDC Designer 콘솔의 도움말 시스템에서 CDC 데이터베이스를 참조하십시오.  
  
###  <a name="BKMK_dboxcbcdc_add_service"></a> dbo.xcbcdc_add_service(svcname,sqlusr)  
 **dbo.xcbcdc_add_service** 프로시저는 **MSXDBCDC.xdbcdc_services** 테이블에 항목을 추가하고 **MSXDBCDC.xdbcdc_services** 테이블의 서비스 이름에 대한 ref_count 열에 증가분 하나를 추가합니다. **ref_count**가 0이면 행이 삭제됩니다.  
  
 **dbo.xcbcdc_add_service\<service name, username>** 프로시저를 사용하려면 사용자는 이름 지정되는 CDC 인스턴스 데이터베이스에 대한 **db_owner** 데이터베이스 역할의 멤버이거나 **sysadmin** 또는 **serveradmin** 고정 서버 역할의 멤버여야 합니다.  
  
###  <a name="BKMK_dboxdbcdc_start"></a> dbo.xdbcdc_start(dbname)  
 **dbo.xdbcdc_start** 프로시저는 선택한 CDC 인스턴스를 처리하는 CDC Service에 시작 요청을 전송하여 변경 처리를 시작합니다.  
  
 **dbo.xcdcdc_start** 프로시저를 사용하려면 사용자는 CDC 데이터베이스에 대한 **db_owner** 데이터베이스 역할의 멤버이거나 **인스턴스에 대한** sysadmin **또는** serveradmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 역할의 멤버여야 합니다.  
  
###  <a name="BKMK_dboxdbcdc_stop"></a> dbo.xdbcdc_stop(dbname)  
 **dbo.xdbcdc_stop** 프로시저는 선택한 CDC 인스턴스를 처리하는 CDC Service에 중지 요청을 전송하여 변경 처리를 중지합니다.  
  
 **dbo.xcdcdc_stop** 프로시저를 사용하려면 사용자는 CDC 데이터베이스에 대한 **db_owner** 데이터베이스 역할의 멤버이거나 **인스턴스에 대한** sysadmin **또는** serveradmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 역할의 멤버여야 합니다.  
  
##  <a name="BKMK_CDCdatabase"></a> CDC 데이터베이스  
 CDC Service에서 사용되는 각 Oracle CDC 인스턴스는 CDC Database라는 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 연결됩니다. 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스는 Oracle CDC Service와 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 호스팅됩니다.  
  
 CDC 데이터베이스에는 특별 cdc 스키마가 포함되어 있습니다. Oracle CDC Service는 접두사가 **xdbcdc_** 인 테이블 이름에 이 스키마를 사용합니다. 이 스키마는 보안 및 일관성을 위해 사용됩니다.  
  
 Oracle CDC 인스턴스와 CDC 데이터베이스는 모두 Oracle CDC Designer 콘솔을 사용하여 만들어집니다. CDC 데이터베이스에 대한 자세한 내용은 Oracle CDC Designer 콘솔 설치 프로그램에 들어 있는 설명서를 참조하십시오.  
  
##  <a name="BKMK_CommandConfigCDC"></a> 명령줄을 사용하여 CDC Service 구성  
 명령줄에서 Oracle CDC Service 프로그램(xdbcdcsvc.exe)를 작동할 수 있습니다. CDC Service 프로그램은 네이티브 32비트/64비트 Windows 실행 파일입니다.  
  
 **참고 항목**  
  
 [CDC Service 명령줄 인터페이스를 사용하는 방법](../../integration-services/change-data-capture/how-to-use-the-cdc-service-command-line-interface.md)  
  
### <a name="service-program-commands"></a>서비스 프로그램 명령  
 이 섹션에서는 CDC Service를 구성하는 데 사용되는 다음 명령에 대해 설명합니다.  
  
-   [Config](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_config)  
  
-   [만들기](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_create)  
  
-   [Delete](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_delete)  
  
###  <a name="BKMK_config"></a> Config  
 `Config` 를 사용하여 스크립트에서 Oracle CDC Service 구성을 업데이트합니다. 이 명령은 CDC Service 구성의 특정 부분만(예: 비대칭 키 암호를 모르는 상태에서 연결 문자열만) 업데이트하는 데 사용할 수 있습니다. 컴퓨터 관리자가 명령을 실행해야 합니다. 다음은 `Config` 명령의 예입니다.  
  
```  
"<path>xdbcdcsvc.exe" config  
     <cdc-service-name>  
     [connect= <sql-server-connection-string>]  
     [key= <asym-key-password>]  
     [svcacct= <windows-account> <windows-password>]  
     [sqlacct= <sql-username> <sql-password>]  
  
```  
  
 각 항목이 나타내는 의미는 다음과 같습니다.  
  
 **cdc-service-name** 은 업데이트할 CDC Service의 이름입니다. 필수 매개 변수입니다.  
  
 **sql-server-connection-string** 은 업데이트해야 할 연결 문자열입니다. 연결 문자열에 공백이나 따옴표가 포함되는 경우 큰따옴표(")로 묶어야 합니다. 따옴표를 이중으로 사용하면 포함된 따옴표가 이스케이프됩니다.  
  
 **asym-key-password** 는 업데이트해야 할 암호입니다.  
  
 **windows-account**, **windows-password** 는 업데이트되는 서비스에 대한 Windows 계정 자격 증명입니다.  
  
 **sql-username**, **sql-password** 는 업데이트되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 자격 증명입니다. sqlacct에서 사용자 이름과 암호가 모두 비어 있는 경우 Oracle CDC Service는 Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결합니다.  
  
 **참고**: 공백이나 따옴표가 포함된 매개 변수는 큰따옴표(")로 묶어야 합니다. 포함된 큰따옴표는 이중으로 사용해야 합니다(예: **"A#B" D** 를 암호로 사용하려면 **""A#B"" D"** 입력).  
  
###  <a name="BKMK_create"></a> 만들기  
 `Create` 를 사용하여 스크립트에서 Oracle CDC Service를 만듭니다. 컴퓨터 관리자가 명령을 실행해야 합니다. 다음은 `Create` 명령의 예입니다.  
  
```  
"<path>xdbcdcsvc.exe" create  
     <cdc-service-name>  
     [connect= "<sql-server-connection-string>"]  
     [key= <asym-key-password>]  
     [svcacct <windows-account> <windows-password>]  
     [sqlacct <sql-username> <sql-password>]  
```  
  
 각 항목이 나타내는 의미는 다음과 같습니다.  
  
 **cdc-service-name** 은 새로 만든 서비스의 이름입니다. 이 이름을 사용하는 서비스가 이미 있는 경우 프로그램에서 오류가 반환됩니다. 긴 이름이나 공백이 있는 이름은 사용하지 마십시오. "/" 및 "\\" 문자는 서비스 이름에 올바른 문자가 아닙니다. 필수 매개 변수입니다.  
  
 **sql-server-connection-string** 은 새 Oracle CDC Service와 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 연결 문자열입니다.  
  
 **asym-key-password** 는 원본 데이터베이스 로그 마이닝 자격 증명을 저장하는 데 사용된 비대칭 키를 보호하는 암호입니다.  
  
 **windows-account**, **windows-password** 는 만들어지는 Oracle CDC Service와 연결된 계정 이름과 암호입니다.  
  
 **sql-username**, **sql-password** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정 이름과 암호입니다. 이 두 매개 변수가 모두 비어 있으면 Oracle CDC Service는 Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결합니다.  
  
 **참고**: 공백이나 따옴표가 포함된 매개 변수는 큰따옴표(")로 묶어야 합니다. 포함된 큰따옴표는 이중으로 사용해야 합니다(예: **"A#B" D** 를 암호로 사용하려면 **""A#B"" D"** 입력).  
  
###  <a name="BKMK_delete"></a> Delete  
 `Delete` 를 사용하여 스크립트에서 Oracle CDC Service를 완전히 삭제합니다. 컴퓨터 관리자가 이 명령을 실행해야 합니다. 다음은 `Delete` 명령의 예입니다.  
  
```  
"<path>xdbcdcsvc.exe" delete  
    <cdc-service-name>  
  
```  
  
 각 항목이 나타내는 의미는 다음과 같습니다.  
  
 **cdc-service-name** 삭제할 CDC Service의 이름입니다.  
  
 **참고**: 공백이나 따옴표가 포함된 매개 변수는 큰따옴표(")로 묶어야 합니다. 포함된 큰따옴표는 이중으로 사용해야 합니다(예: **"A#B" D** 를 암호로 사용하려면 **""A#B"" D"** 입력).  
  
## <a name="see-also"></a>참고 항목  
 [CDC Service 명령줄 인터페이스를 사용하는 방법](../../integration-services/change-data-capture/how-to-use-the-cdc-service-command-line-interface.md)   
 [CDC를 위해 SQL Server를 준비하는 방법](../../integration-services/change-data-capture/how-to-prepare-sql-server-for-cdc.md)  
  
  
