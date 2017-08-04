---
title: "ssbdiagnose 유틸리티 (Service Broker) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Service Broker, runtime reports
- Service Broker, command prompt utilities
- troubleshooting [Service Broker], conversations
- troubleshooting [Service Broker], configurations
- command prompt utilities [Service Broker]
- Service Broker, troubleshooting
- Service Broker, configuration reports
- Service Broker, tools
- troubleshooting [Service Broker], runtime
- conversations [Service Broker], troubleshooting
- troubleshooting [Service Broker], ssbdiagnose utility
- tools [Service Broker], ssbdiagnose
- Service Broker, ssbdiagnose utility
- ssbdiagnose
ms.assetid: 0c1636e8-a3db-438e-be4c-1ea40d1f4877
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 84a8489536783d1a9cb1d97aa95022ca7e952118
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="ssbdiagnose-utility-service-broker"></a>ssbdiagnose 유틸리티(Service Broker)
  **ssbdiagnose** 유틸리티는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 서비스 구성이나 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화의 문제를 보고합니다. 이때 두 서비스나 한 서비스에 대한 구성 검사를 수행할 수 있습니다. 오류는 명령 프롬프트 창에 사람이 읽을 수 있는 텍스트 또는 다른 응용 프로그램으로 리디렉션될 수 있는 서식이 설정된 XML로 보고됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ssbdiagnose   
[ [ -XML ]  
    [ -LEVEL { ERROR | WARNING | INFO } ]  
  [-IGNORE error_id ] [ ...n]  
    [ <baseconnectionoptions> ]  
  { <configurationreport> | <runtimereport> }  
]  
| -?  
  
<configurationreport> ::=  
    CONFIGURATION  
  { [ FROM SERVICE service_name  
      [ <fromconnectionoptions> ]  
      [ MIRROR <mirrorconnectionoptions> ]  
    ]  
    [ TO SERVICE service_name[, broker_id ]  
      [ <toconnectionoptions> ]  
      [ MIRROR <mirrorconnectionoptions> ]  
    ]  
  }  
    ON CONTRACT contract_name  
  [ ENCRYPTION { ON | OFF | ANONYMOUS } ]  
  
<runtime_report> ::=  
    RUNTIME  
    [-SHOWEVENTS ]  
        [ -NEW  
         [ -ID { conversation_handle  
                | conversation_group_id  
                 | conversation_id  
                  }  
        ] [ ...n]  
        ]  
    [ -TIMEOUT timeout_interval ]  
    [ <runtimeconnectionoptions> ]  
  
<baseconnectionoptions> ::=  
  <connectionoptions>  
  
<fromconnectionoptions> ::=  
  <connectionoptions>  
  
<toconnectionoptions> ::=  
  <connectionoptions>  
  
<mirrorconnectionoptions> ::=  
  <connectionoptions>  
  
<runtimeconnectionoptions> ::=  
  [ CONNECT TO <connectionoptions> ] [ ...n]  
  
<connectionoptions> ::=  
    [ –E | { -U login_id [ -P password ] } ]  
  [ -S server_name[\instance_name] ]  
  [ -d database_name ]  
  [ -l login_timeout ]  
  
```  
  
## <a name="command-line-options"></a>명령줄 옵션  
 **-XML**  
 **ssbdiagnose** 출력이 서식이 설정된 XML로 생성되도록 지정합니다. 이 출력은 파일이나 다른 응용 프로그램으로 리디렉션될 수 있습니다. **-XML** 을 지정하지 않을 경우 **ssbdiagnose** 출력 형식은 사람이 읽을 수 있는 텍스트로 지정됩니다.  
  
 **-LEVEL** { **ERROR** | **WARNING** | **INFO**}  
 보고할 메시지 수준을 지정합니다.  
  
 **ERROR**: 오류 메시지만 보고합니다.  
  
 **WARNING**: 경고 메시지와 오류 메시지를 보고합니다.  
  
 **INFO**: 오류, 경고 및 정보 메시지를 보고합니다.  
  
 기본 설정은 **WARNING**입니다.  
  
 **-IGNORE** *error_id*  
 지정된 *error_id* 의 오류 또는 메시지가 보고서에 포함되지 않도록 지정합니다. 여러 메시지 ID를 표시하지 않으려면 **-IGNORE** 를 여러 번 지정하면 됩니다.  
  
 **\<baseconnectionoptions >**  
 특정 절에 연결 옵션이 포함되어 있지 않은 경우 **ssbdiagnose** 에서 사용되는 기본 연결 정보를 지정합니다. 특정 절에 지정되는 연결 정보는 **baseconnectionoption** 정보보다 우선합니다. 이 작업은 각 매개 변수에 대해 별도로 수행됩니다. 예를 들어 **baseconnetionoptions** 에는 **-S** 와 **-d**가 둘 다 지정되고 **toconnetionoptions** 에는 **-d**만 지정된 경우 **ssbdiagnose** 는 **baseconnetionoptions** 의 -S와 **toconnetionoptions**의 -d를 사용합니다.  
  
 **CONFIGURATION**  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 서비스 쌍 간 구성 오류 또는 단일 서비스 구성 오류에 대한 보고서를 요청합니다.  
  
 **FROM SERVICE** *service_name*  
 대화를 시작하는 서비스를 지정합니다.  
  
 **\<fromconnectionoptions >**  
 시작자 서비스를 보유하는 데이터베이스에 연결하는 데 필요한 정보를 지정합니다. **fromconnectionoptions** 를 지정하지 않은 경우 **ssbdiagnose** 는 **baseconnectionoptions** 의 연결 정보를 사용하여 시작자 데이터베이스에 연결합니다. **fromconnectionoptions** 를 지정한 경우 시작자 서비스를 보유하는 데이터베이스를 포함해야 합니다. **fromconnectionoptions** 를 지정하지 않은 경우 **baseconnectionoptions** 에서 시작자 데이터베이스를 지정해야 합니다.  
  
 **TO SERVICE** *service_name*[, *broker_id* ]  
 대화의 대상이 되는 서비스를 지정합니다.  
  
 *service_name*: 대상 서비스의 이름을 지정합니다.  
  
 *broker_id*: 대상 데이터베이스를 식별하는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] ID를 지정합니다. *broker_id* 는 GUID입니다. 대상 데이터베이스에서 다음 쿼리를 실행하면 이 ID를 찾을 수 있습니다.  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID();  
```  
  
 **\<toconnectionoptions >**  
 대상 서비스를 보유하는 데이터베이스에 연결하는 데 필요한 정보를 지정합니다. **toconnectionoptions** 를 지정하지 않은 경우 **ssbdiagnose** 는 **baseconnectionoptions** 의 연결 정보를 사용하여 대상 데이터베이스에 연결합니다.  
  
 **MIRROR**  
 연결된 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 서비스가 미러된 데이터베이스에서 호스팅되도록 지정합니다. **ssbdiagnose** 는 서비스에 대한 경로가 CREATE ROUTE에 MIRROR_ADDRESS가 지정된 미러된 경로인지 확인합니다.  
  
 **\<mirrorconnectionoptions >**  
 미러 데이터베이스에 연결하는 데 필요한 정보를 지정합니다. **mirrorconnectionoptions** 를 지정하지 않은 경우 **ssbdiagnose** 는 **baseconnectionoptions** 의 연결 정보를 사용하여 미러 데이터베이스에 연결합니다.  
  
 **ON CONTRACT** *contract_name*  
 **ssbdiagnose** 가 지정된 계약을 사용하는 구성만 검사하도록 요청합니다. ON CONTRACT를 지정하지 않을 경우 **ssbdiagnose** 는 DEFAULT라는 계약에 대해 보고합니다.  
  
 **ENCRYPTION** { **ON** | **OFF** | **ANONYMOUS** }  
 대화가 지정된 수준의 암호화에 대해 올바로 구성되었는지 확인하도록 요청합니다.  
  
 **ON**: 기본 설정입니다. 전체 대화 보안이 구성됩니다. 인증서가 대화의 양측에 배포되었고, 원격 서비스 바인딩이 있으며, 대상 서비스에 대한 GRANT SEND 문이 시작 사용자를 지정했습니다.  
  
 **OFF**: 대화 보안이 구성되지 않습니다. 인증서가 배포되지 않았고, 원격 서비스 바인딩이 만들어지지 않았으며, 시작자 서비스에 대한 GRANT SEND가 **public** 역할을 지정했습니다.  
  
 **ANONYMOUS**: 익명 대화 보안이 구성됩니다. 인증서 한 개가 배포되었고, 원격 서비스 바인딩이 익명 절을 지정했으며, 대상 서비스에 대한 GRANT SEND가 **public** 역할을 지정했습니다.  
  
 **RUNTIME**  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화에 대해 런타임 오류를 일으키는 문제에 대한 보고서를 요청합니다. **-NEW** 와 **-ID** 를 둘 다 지정하지 않을 경우 **ssbdiagnose** 가 연결 옵션에 지정된 모든 데이터베이스에 있는 대화를 모두 모니터링합니다. **-NEW** 또는 **-ID** 를 지정할 경우 **ssbdiagnose** 는 매개 변수에 지정된 ID 목록을 작성합니다.  
  
 **ssbdiagnose** 는 실행되는 동안 런타임 오류를 나타내는 모든 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 이벤트를 기록합니다. 즉, 지정된 ID에 대해 발생하는 이벤트뿐 아니라 시스템 수준 이벤트도 기록합니다. 런타임 오류가 발생하면 **ssbdiagnose** 는 연결된 구성에 대한 구성 보고서를 실행합니다.  
  
 기본적으로 출력 보고서에는 런타임 오류가 포함되지 않고 구성 분석 결과만 포함됩니다. **-SHOWEVENTS** 를 사용하면 보고서에 런타임 오류를 포함할 수 있습니다.  
  
 **-SHOWEVENTS**  
 RUNTIME 보고 동안 **ssbdiagnose** 가 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 이벤트를 보고하도록 지정합니다. 오류 조건으로 간주되는 이벤트만 보고됩니다. 기본적으로 **ssbdiagnose** 는 오류 이벤트를 모니터링만 하고 출력에 보고하지 않습니다.  
  
 **-NEW**  
 **ssbdiagnose** 실행 후 시작되는 첫 번째 대화의 런타임 모니터링을 요청합니다.  
  
 **-ID**  
 지정된 대화 요소의 런타임 모니터링을 요청합니다. **-ID** 는 여러 번 지정할 수 있습니다.  
  
 대화 핸들을 지정할 경우 연결된 대화 끝점과 연결된 이벤트만 보고됩니다. 대화 ID를 지정할 경우 해당 대화와 그 시작자 및 대상 끝점에 대한 이벤트가 모두 보고됩니다. 대화 그룹 ID를 지정할 경우 대화 그룹에 있는 모든 대화와 끝점에 대한 이벤트가 모두 보고됩니다.  
  
 *conversation_handle*  
 응용 프로그램에 있는 대화 끝점을 식별하는 고유 식별자입니다. 대화 핸들은 대화의 각 끝점에 고유하기 때문에 시작자 끝점과 대상 끝점은 서로 다른 대화 핸들을 갖습니다.  
  
 대화 핸들은 *@dialog_handle* 문의 **@dialog_handle** 매개 변수와 **conversation_handle** 문의 결과 집합에 있는 **conversation_handle** 열에 의해 응용 프로그램에 반환됩니다.  
  
 대화 핸들은 **sys.transmission_queue** 및 **sys.conversation_endpoints** 카탈로그 뷰의 **conversation_handle** 열에서 보고됩니다.  
  
 *conversation_group_id*  
 대화 그룹을 식별하는 고유 식별자입니다.  
  
 대화 그룹 ID는 *@conversation_group_id* 문의 **@conversation_group_id** 매개 변수와 **conversation_group_id** 문의 결과 집합에 있는 **conversation_handle** 열에 의해 응용 프로그램에 반환됩니다.  
  
 대화 그룹 ID는 **sys.conversation_groups** 및 **sys.conversation_endpoints** 카탈로그 뷰의 **conversation_group_id** 열에서 보고됩니다.  
  
 *conversation_id*  
 대화를 식별하는 고유 식별자입니다. 대화의 시작자 끝점과 대상 끝점은 둘 다 동일한 대화 ID를 사용합니다.  
  
 대화 ID는 **sys.conversation_endpoints** 카탈로그 뷰의 **conversation_id** 열에서 보고됩니다.  
  
 **-TIMEOUT** *timeout_interval*  
 **RUNTIME** 보고서를 실행할 시간(초)을 지정합니다. **-TIMEOUT** 을 지정하지 않을 경우 런타임 보고서가 무기한 실행됩니다. **-TIMEOUT** 은 **RUNTIME** 보고서에서만 사용됩니다. **CONFIGURATION** 보고서에서는 사용되지 않습니다. Ctrl+C를 사용하면 **-TIMEOUT** 을 지정하지 않은 경우 **ssbdiagnose** 를 종료하거나 제한 시간 간격이**-**만료되기 전에 런타임 보고서를 종료할 수 있습니다. *timeout_interval* 은 1에서 2,147,483,647 사이의 숫자여야 합니다.  
  
 **\<runtimeconnectionoptions >**  
 모니터링 중인 대화 요소와 연결된 서비스를 포함하는 데이터베이스에 대한 연결 정보를 지정합니다. 모든 서비스가 동일한 데이터베이스에 있으면 **CONNECT TO** 절을 하나만 지정하면 됩니다. 서비스가 서로 다른 데이터베이스에 있으면 각 데이터베이스에 대해 **CONNECT TO** 절을 제공해야 합니다. **runtimeconnectionoptions** 를 지정하지 않은 경우 **ssbdiagnose** 는 **baseconnectionoptions**의 연결 정보를 사용합니다.  
  
 **–E**  
 현재 Windows 계정을 로그인 ID로 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 대해 Windows 인증 연결을 엽니다. 로그인은 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
 -E 옵션은 SQLCMDUSER 및 SQLCMDPASSWORD 환경 변수의 사용자와 암호 설정을 무시합니다.  
  
 **-E** 와 **-U** 를 둘 다 지정하지 않을 경우 **ssbdiagnose** 가 SQLCMDUSER 환경 변수의 값을 사용합니다. SQLCMDUSER도 설정하지 않을 경우 **ssbdiagnose** 는 Windows 인증을 사용합니다.  
  
 **-E** 옵션과 함께 **-U** 옵션 또는 **-P** 옵션을 사용하면 오류 메시지가 생성됩니다.  
  
 **-U** *login_id*  
 지정된 로그인 ID를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 연결을 엽니다. 로그인은 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
 **-E** 와 **-U** 를 둘 다 지정하지 않을 경우 **ssbdiagnose** 가 SQLCMDUSER 환경 변수의 값을 사용합니다. SQLCMDUSER도 설정하지 않을 경우 **ssbdiagnose** 는 **ssbdiagnose**를 실행하는 사용자의 Windows 계정을 기반으로 하는 Windows 인증 모드를 사용하여 연결을 시도합니다.  
  
 **-U** 옵션과 함께 **-E** 옵션을 사용하면 오류 메시지가 생성됩니다. **–U** 옵션 다음에 둘 이상의 인수를 지정하면 오류 메시지가 생성되고 프로그램이 종료됩니다.  
  
 **-P** *password*  
 **-U** 로그인 ID의 암호를 지정합니다. 암호는 대/소문자를 구분합니다. **-U** 옵션만 사용하고 **-P** 옵션을 사용하지 않을 경우 **ssbdiagnose** 는 SQLCMDPASSWORD 환경 변수의 값을 사용합니다. SQLCMDPASSWORD도 설정하지 않을 경우 **ssbdiagnose** 는 사용자에게 암호를 묻는 메시지를 표시합니다.  
  
> [!IMPORTANT]  
>  SET SQLCMDPASSWORD 명령을 입력하면 모니터에서 누구나 암호를 볼 수 있습니다.  
  
 **-P** 옵션을 암호 없이 지정할 경우 **ssbdiagnose** 는 기본 암호(NULL)를 사용합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]자세한 내용은 참조 [Strong Passwords](../../relational-databases/security/strong-passwords.md)합니다.  
  
 암호 프롬프트는 다음과 같이 콘솔에 출력되어 표시됩니다. `Password:`  
  
 사용자 입력은 숨겨지므로 아무 것도 표시되지 않고 커서가 해당 위치에 그대로 남아 있습니다.  
  
 **-P** 옵션과 함께 **-E** 옵션을 사용하면 오류 메시지가 생성됩니다.  
  
 **-P** 옵션 다음에 둘 이상의 인수를 지정하면 오류 메시지가 생성됩니다.  
  
 **baseconnetionoptions** *server_name*[\\*instance_name*]  
 분석할 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스를 보유하는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 인스턴스를 지정합니다.  
  
 해당 서버에 있는 기본 *인스턴스에 연결하려면* server_name [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 지정합니다. 해당 서버에 있는 명명된 *인스턴스에 연결하려면***\\***server_name* instance_name [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 지정합니다. **-S** 를 지정하지 않으면 **ssbdiagnose** 가 기본적으로 SQLCMDSERVER 환경 변수의 값을 사용합니다. SQLCMDSERVER도 설정하지 않을 경우 **ssbdiagnose** 는 로컬 컴퓨터에 있는 기본 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결합니다.  
  
 **-S** *database_name*  
 분석할 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 서비스를 보유하는 데이터베이스를 지정합니다. 데이터베이스가 없을 경우에는 오류가 생성됩니다. **-d** 를 지정하지 않을 경우 기본적으로 로그인의 기본 데이터베이스 속성에 지정된 데이터베이스가 사용됩니다.  
  
 **-l** *login_timeout*  
 서버 연결 시도 시간이 초과되기 전의 대기 시간을 초 단위로 지정합니다. **-l** 를 지정하지 않을 경우 **ssbdiagnose** 가 SQLCMDLOGINTIMEOUT 환경 변수의 값 집합을 사용합니다. SQLCMDLOGINTIMEOUT도 설정하지 않을 경우 기본 제한 시간은 30초입니다. 로그인 제한 시간은 0에서 65534 사이의 숫자여야 합니다. 입력한 값이 숫자가 아니거나 이 범위에 속하지 않을 경우 **ssbdiagnose** 는 오류 메시지를 생성합니다. 값을 0으로 설정하면 제한 시간이 없습니다.  
  
 **-?**  
 명령줄 도움말을 표시합니다.  
  
## <a name="remarks"></a>주의  
 **ssbdiagnose** 를 사용하여 다음을 수행할 수 있습니다.  
  
-   새로 구성된 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 응용 프로그램에 구성 오류가 없음을 확인합니다.  
  
-   기존 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 응용 프로그램의 구성을 변경한 후에 구성 오류가 없음을 확인합니다.  
  
-   [!INCLUDE[ssSB](../../includes/sssb-md.md)] 데이터베이스가 분리된 다음 새 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 다시 연결된 후에 구성 오류가 없음을 확인합니다.  
  
-   서비스 간에 메시지가 성공적으로 전송되지 않은 경우 구성 오류가 있는지 여부를 확인합니다.  
  
-   [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화 요소 집합에서 발생하는 모든 오류에 대한 보고서를 가져옵니다.  
  
## <a name="configuration-reporting"></a>구성 보고  
 대화에 사용되는 구성을 올바로 분석하려면 대화에 사용되는 것과 동일한 옵션을 사용하는 **ssbdiagnose** 구성 보고서를 실행합니다. 대화에 사용되는 것보다 낮은 수준의 옵션을 **ssbdiagnose** 에 지정할 경우 **ssbdiagnose** 가 대화에 필요한 조건을 보고하지 않을 수 있습니다. 대화에 사용되는 것보다 높은 수준의 옵션을 **ssbdiagnose**에 지정할 경우 대화에 필요하지 않은 항목을 보고할 수 있습니다. 예를 들어 동일한 데이터베이스에 있는 두 서비스 간의 대화가 ENCPRYPTION이 OFF인 상태에서 실행될 수 있습니다. **ssbdiagnose** 를 실행하여 두 서비스 간 구성의 유효성을 검사하는 경우 기본 ENCRYPTION ON 설정을 사용하면 **ssbdiagnose** 가 데이터베이스에 마스터 키가 없음을 보고합니다. 마스터 키는 대화에 필요하지 않습니다.  
  
 **ssbdiagnose** 구성 보고서는 실행될 때마다 하나 또는 한 쌍의 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 서비스만 분석합니다. 여러 쌍의 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 서비스를 보고하려면 **ssbdiagnose** 를 여러 번 호출하는 .cmd 명령 파일을 작성합니다.  
  
## <a name="runtime-reporting"></a>런타임 보고  
 -RUNTIME을 지정할 경우 **ssbdiagnose** 는 **runtimeconnectionoptions** 및 **baseconnectionoptions** 에 지정된 모든 데이터베이스를 검색하여 [!INCLUDE[ssSB](../../includes/sssb-md.md)] ID 목록을 작성합니다. 작성되는 전체 ID 목록은 다음과 같이 -NEW 및 -ID가 어떻게 지정되는지에 따라 달라집니다.  
  
-   **-NEW** 와 **-ID** 를 둘 다 지정하지 않을 경우 목록에 연결 옵션에 지정된 모든 데이터베이스에 있는 대화가 모두 포함됩니다.  
  
-   **-NEW** 를 지정할 경우 **ssbdiagnose** 는 **ssbdiagnose** 가 실행된 후 시작되는 첫 번째 대화의 요소를 포함합니다. 여기에는 대상 대화 끝점과 시작자 대화 끝점 둘 다에 대한 대화 ID와 대화 핸들이 포함됩니다.  
  
-   대화 핸들을 사용하여 **-ID** 가 지정된 경우에는 해당 핸들만 목록에 포함됩니다.  
  
-   대화 ID를 사용하여 **-ID** 가 지정된 경우에는 두 대화 끝점 모두에 대한 대화 ID와 핸들이 목록에 추가됩니다.  
  
-   대화 그룹 ID를 사용하여 **-ID** 가 지정된 경우에는 그룹에 있는 모든 대화 ID와 대화 핸들이 목록에 추가됩니다.  
  
 연결 옵션에 지정되지 않은 데이터베이스의 요소는 목록에 포함되지 않습니다. 예를 들어 **-ID** 를 사용하여 대화 ID를 지정할 때 시작자 데이터베이스에 대해서만 **runtimeconnectionoptions** 절을 제공하고 대상 데이터베이스에 대해서는 제공하지 않을 경우 **ssbdiagnose** 는 해당 ID 목록에 대화 ID와 시작자 대화 핸들만 포함하고 대상 대화 핸들을 포함하지 않습니다.  
  
 **ssbdiagnose** 모니터는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] runtimeconnectionoptions **및** baseconnectionoptions **에 지정된 데이터베이스에서**이벤트를 모니터링하며, 런타임 목록에 있는 하나 이상의 [!INCLUDE[ssSB](../../includes/sssb-md.md)] ID에서 오류가 발생했음을 나타내는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 이벤트를 검색합니다. 또한**ssbdiagnose** 는 특별히 대화 그룹과 연관이 없는 시스템 수준 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 오류 이벤트를 검색합니다.  
  
 **ssbdiagnose** 는 대화 오류를 찾을 경우 구성 보고서를 추가로 실행하여 해당 이벤트의 근본 원인을 보고하려고 합니다. **ssbdiagnose** 는 데이터베이스의 메타데이터를 사용하여 해당 대화에 사용된 인스턴스, [!INCLUDE[ssSB](../../includes/sssb-md.md)] ID, 데이터베이스, 서비스 및 계약을 파악한 다음 사용 가능한 모든 정보를 사용하여 구성 보고서를 실행합니다.  
  
 기본적으로 **ssbdiagnose** 는 오류 이벤트를 보고하지 않고 구성 검사 동안 발견된 기본 문제만 보고합니다. 따라서 보고되는 정보량이 최소화되고 기본 구성 문제에 집중하는 데 도움이 됩니다. **-SHOWEVENTS** 를 지정할 경우 **ssbdiagnose**에서 발생한 오류 이벤트를 볼 수 있습니다.  
  
## <a name="issues-reported-by-ssbdiagnose"></a>ssbdiagnose가 보고하는 문제  
 **ssbdiagnose** 는 세 가지 문제 클래스를 보고합니다. XML 출력 파일에서 각 문제 클래스는 서로 다른 유형의 Issue 요소로 보고됩니다. **ssbdiagnose** 가 보고하는 이러한 세 가지 유형의 문제는 다음과 같습니다.  
  
 **진단**  
 구성 문제를 보고합니다. 여기에는 **CONFIGURATION** 보고서가 실행되는 동안이나 **RUNTIME** 보고서의 구성 단계에서 발견된 문제가 포함됩니다. **ssbdiagnose** 는 한 번에 하나의 구성 문제를 보고합니다.  
  
 **이벤트**  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] RUNTIME **보고 동안 모니터링 중인 대화에서 문제가 발생했음을 나타내는** 이벤트를 보고합니다. **ssbdiagnose** 는 이벤트가 발생할 때마다 보고합니다. 따라서 여러 대화에서 문제가 발생할 경우 이벤트가 여러 번 보고될 수 있습니다.  
  
 **문제**  
 **ssbdiagnose** 가 구성 분석을 완료하거나 대화를 모니터링하지 못하게 하는 문제를 보고합니다.  
  
## <a name="sqlcmd-environment-variables"></a>sqlcmd 환경 변수  
 **ssbdiagnose** 유틸리티는 **sqlcmd** 유틸리티도 사용하는 SQLCMDSERVER, SQLCMDUSER, SQLCMDPASSWORD 및 SQLCMDLOGINTIMOUT 환경 변수를 지원합니다. 환경 변수는 명령 프롬프트 SET 명령을 사용하여 설정하거나 **sqlcmd** 를 사용하여 실행하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트에서 **setvar**명령을 사용하여 설정할 수 있습니다. **sqlcmd** 에서 **setvar**을 사용하는 방법은 [스크립팅 변수와 함께 sqlcmd 사용](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 각 **connectionoptions** 절에서 **-E** 또는 **-U** 를 사용하여 지정된 로그인은 **-S** 에 지정된 인스턴스에 있는 **sysadmin**고정 서버 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
 이 섹션에는 명령 프롬프트에서 **ssbdiagnose** 를 사용하는 예가 포함되어 있습니다.  
  
### <a name="a-checking-the-configuration-of-two-services-in-the-same-database"></a>1. 동일한 데이터베이스에 있는 두 서비스의 구성 검사  
 다음 예에서는 아래 조건에 해당하는 경우 구성 보고서를 요청하는 방법을 보여 줍니다.  
  
-   시작자 서비스와 대상 서비스가 동일한 데이터베이스에 있습니다.  
  
-   데이터베이스가 기본 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 있습니다.  
  
-   인스턴스가 **ssbdiagnose** 가 실행되는 동일한 컴퓨터에 있습니다.  
  
 **ssbdiagnose** 유틸리티는 ON CONTRACT가 지정되지 않았기 때문에 DEFAULT 계약을 사용하는 구성을 보고합니다.  
  
```  
ssbdiagnose -E -d MyDatabase CONFIGURATION FROM SERVICE /test/initiator TO SERVICE /test/target  
```  
  
### <a name="b-checking-the-configuration-of-two-services-on-separate-computers-that-use-one-login"></a>2. 별개의 컴퓨터에 있지만 동일한 로그인을 사용하는 두 서비스의 구성 검사  
 다음 예에서는 시작자 서비스와 대상 서비스가 서로 다른 컴퓨터에 있지만 동일한 Windows 인증 로그인을 사용하여 액세스할 수 있는 경우 구성 보고서를 요청하는 방법을 보여 줍니다.  
  
```  
ssbdiagnose -E CONFIGURATION FROM SERVICE /text/initiator -S InitiatorComputer -d InitiatorDatabase TO SERVICE /test/target -S TargetComputer -d TargetDatabase ON CONTRACT TestContract  
```  
  
### <a name="c-checking-the-configuration-of-two-services-on-separate-computers-that-use-separate-logins"></a>3. 별개의 컴퓨터에 있으며 서로 다른 로그인을 사용하는 두 서비스의 구성 검사  
 다음 예에서는 시작자 서비스와 대상 서비스가 서로 다른 컴퓨터에 있고 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 서로 다른 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인증 로그인이 필요한 경우 구성 보고서를 요청하는 방법을 보여 줍니다.  
  
```  
ssbdiagnose CONFIGURATION FROM SERVICE /text/initiator   
-S InitiatorComputer -U InitiatorLogin -p !wEx23Dvb   
-d InitiatorDatabase TO SERVICE /test/target -S TargetComputer   
-U TargetLogin -p ER!49jiy -d TargetDatabase ON CONTRACT TestContract  
```  
  
### <a name="d-checking-mirrored-service-configurations-on-separate-computers-with-anonymous-encryption"></a>4. 익명 암호화를 사용하는 서로 다른 컴퓨터에 있는 미러된 서비스 구성 검사  
 다음 예에서는 시작자 서비스와 대상 서비스가 서로 다른 컴퓨터에 있고 시작자가 명명된 인스턴스에 미러된 경우 보고서를 요청하는 방법을 보여 줍니다. 보고서는 서비스가 익명 암호화를 사용하도록 구성되어 있는지도 확인합니다.  
  
```  
ssbdiagnose -E CONFIGURATION FROM SERVICE /text/initiator   
-S InitiatorComputer -d InitiatorDatabase MIRROR   
-S MirrorComputer/MirrorInstance TO SERVICE /test/target   
-S TargetComputer -d TargetDatabase ON CONTRACT TestContract ENCRYPTION ANONYMOUS  
```  
  
### <a name="e-checking-the-configuration-of-two-contracts"></a>5. 두 계약의 구성 검사  
 다음 예에서는 아래 조건에 해당하는 경우 구성 보고서를 요청하는 명령 파일을 작성하는 방법을 보여 줍니다.  
  
-   시작자 서비스와 대상 서비스가 동일한 데이터베이스에 있습니다.  
  
-   데이터베이스가 기본 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 있습니다.  
  
-   인스턴스가 **ssbdiagnose** 가 실행되는 동일한 컴퓨터에 있습니다.  
  
 **ssbdiagnose** 유틸리티는 실행될 때마다 동일한 서비스 간에 서로 다른 계약을 사용하는 구성을 보고합니다.  
  
```  
ssbdiagnose -E -d MyDatabase CONFIGURATION FROM SERVICE   
/test/initiator TO SERVICE /test/target ON CONTRACT PayRaiseContract  
ssbdiagnose -E -d MyDatabase CONFIGURATION FROM SERVICE /test/initiator   
TO SERVICE /test/target ON CONTRACT PromotionContract  
```  
  
### <a name="f-monitor-the-status-of-a-specific-conversation-on-the-local-computer-with-a-time-out"></a>6. 제한 시간이 설정된 로컬 컴퓨터에 있는 특정 대화 상태 모니터링  
 다음 예에서는 시작자 서비스와 대상 서비스가 **ssbdiagnose**를 실행하고 있는 동일한 컴퓨터의 기본 인스턴스에 있는 동일한 데이터베이스에 있는 특정 대화를 모니터링하는 방법을 보여 줍니다. 제한 시간 간격은 20초로 설정됩니다.  
  
```  
ssbdiagnose -E -d TestDatabase RUNTIME -ID D68D77A9-B1CF-41BF-A5CE-279ABCAB140D -TIMEOUT 20  
```  
  
### <a name="g-monitor-the-status-of-a-conversation-that-spans-two-computers"></a>7. 두 컴퓨터를 연결하는 대화의 상태 모니터링  
 다음 예에서는 시작자 서비스와 대상 서비스가 서로 다른 컴퓨터에 있는 특정 대화를 모니터링하는 방법을 보여 줍니다.  
  
```  
ssbdiagnose RUNTIME -ID D68D77A9-B1CF-41BF-A5CE-279ABCAB140D   
-TIMEOUT 10 CONNECT TO -E -S InitiatorComputer/InitiatorInstance   
-d InitiatorDatabase CONNECT TO -E -S TargetComputer/TargetInstance   
-d TargetDatabase  
```  
  
### <a name="h-monitor-the-status-of-a-conversation-in-two-databases-in-the-same-instance"></a>8. 동일한 인스턴스의 두 데이터베이스에 있는 대화 상태 모니터링  
 다음 예에서는 시작자 서비스와 대상 서비스가 동일한 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스의 서로 다른 데이터베이스에 있는 특정 대화를 모니터링하는 방법을 보여 줍니다. 이 예에서는 **baseconnectionoptions** 를 사용하여 인스턴스 및 로그인 정보를 지정하고 두 개의 CONNECT TO 절을 사용하여 데이터베이스를 지정합니다. -SHOWEVENTS는 모든 런타임 이벤트가 보고서 출력에 포함되도록 하기 위해 지정됩니다.  
  
```  
ssbdiagnose -E -S TestComputer/DevTestInstance RUNTIME -SHOWEVENTS   
-ID 5094d4a7-e38c-4c37-da37-1d58b1cb8455 -TIMEOUT 10 CONNECT TO   
-d InitiatorDatabase CONNECT TO -d TargetDatabase  
```  
  
### <a name="i-monitor-the-status-of-two-conversations-between-two-databases"></a>9. 두 데이터베이스 간의 두 대화 상태 모니터링  
 다음 예에서는 시작자 서비스와 대상 서비스가 동일한 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스의 서로 다른 데이터베이스에 있는 두 대화를 모니터링하는 방법을 보여 줍니다. 이 예에서는 **baseconnectionoptions** 를 사용하여 인스턴스 및 로그인 정보를 지정하고 두 개의 CONNECT TO 절을 사용하여 데이터베이스를 지정합니다.  
  
```  
ssbdiagnose -E -S TestComputer/DevTestInstance RUNTIME   
-ID 5094d4a7-e38c-4c37-da37-1d58b1cb8455   
-ID 9b293be9-226b-4e22-e169-1d2c2c15be86 -TIMEOUT 10 CONNECT TO   
-d InitiatorDatabase CONNECT TO -d TargetDatabase  
```  
  
### <a name="j-monitor-the-status-of-all-conversations-between-two-databases"></a>10. 두 데이터베이스 간의 모든 대화 상태 모니터링  
 다음 예에서는 동일한 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 있는 두 데이터베이스 간의 모든 대화를 모니터링하는 방법을 보여 줍니다. 이 예에서는 **baseconnectionoptions** 를 사용하여 인스턴스 및 로그인 정보를 지정하고 두 개의 CONNECT TO 절을 사용하여 데이터베이스를 지정합니다.  
  
```  
ssbdiagnose -E -S TestComputer/DevTestInstance RUNTIME   
-TIMEOUT 10 CONNECT TO -d InitiatorDatabase CONNECT TO   
-d TargetDatabase  
```  
  
### <a name="k-ignore-specific-errors"></a>11. 특정 오류 무시  
 다음 예에서는 현재 테스트 시스템의 활성화 구성 방식에서 알려진 오류(303 및 304)를 무시하는 방법을 보여 줍니다.  
  
```  
ssbdiagnose -IGNORE 303 -IGNORE 304 -E -d TestDatabase   
CONFIGURATION FROM SERVICE /test/initiator TO SERVICE /test/target   
ON CONTRACT TextContract  
```  
  
### <a name="l-redirecting-ssbdiagnose-xml-output"></a>12. ssbdiagnose XML 출력 리디렉션  
 다음 예에서는 **ssbdiagnose** 가 해당 출력을 파일로 리디렉션되는 XML 파일로 생성하도록 요청하는 방법을 보여 줍니다. 이 예에서 생성하는 TestDiag.xml 파일은 나중에 **ssbdiagnose** XML 파일을 분석하거나 보고하는 응용 프로그램을 사용하여 열거나 XML 메모장과 같은 일반적인 XML 편집기를 사용하여 볼 수 있습니다.  
  
```  
ssbdiagnose -XML -E -d MyDatabase CONFIGURATION FROM SERVICE   
/test/initiator TO SERVICE /test/target > c:\MyDiagnostics\TestDiag.xml  
```  
  
### <a name="m-using-an-environment-variable"></a>13. 환경 변수 사용  
 다음 예제에서는 먼저 서버 이름을 보유하는 SQLCMDSERVER 환경 변수를 설정한 후 **-S** 를 지정하지 않고 **ssbdiagnose**를 실행합니다.  
  
```  
SET SQLCMDSERVER=MyComputer  
ssbdiagnose -XML -E -d MyDatabase CONFIGURATION FROM SERVICE   
/test/initiator TO SERVICE /test/target  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [BEGIN DIALOG conversation&#40; Transact SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [BROKER 우선 순위 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [계약 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-contract-transact-sql.md)   
 [CREATE ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [메시지 유형 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-message-type-transact-sql.md)   
 [CREATE QUEUE&#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [CREATE REMOTE SERVICE BINDING&#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [CREATE ROUTE&#40;Transact-SQL&#41;](../../t-sql/statements/create-route-transact-sql.md)   
 [CREATE SERVICE&#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [수신 &#40; Transact SQL &#41;](../../t-sql/statements/receive-transact-sql.md)   
 [sys.transmission_queue&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md)   
 [sys.conversation_endpoints&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)   
 [sys.conversation_groups&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-groups-transact-sql.md)  
  
  
