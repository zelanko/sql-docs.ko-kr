---
title: "Integration Services 역할(SSIS 서비스) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "보안 [Integration Services], 역할"
  - "db_ssisoperator 역할"
  - "db_ssisadmin 역할"
  - "고정 데이터베이스 역할 [Integration Services]"
  - "패키지 [Integration Services], 보안"
  - "역할 [Integration Services]"
  - "db_ssisltduser 역할"
ms.assetid: 9702e90c-fada-4978-a473-1b1423017d80
caps.latest.revision: 50
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# Integration Services 역할(SSIS 서비스)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장된 패키지에 대한 액세스를 보호하는 데 사용할 수 있는 특정 고정 데이터베이스 수준 역할을 제공합니다. 사용 가능한 역할은 패키지를 SSIS 카탈로그 데이터베이스(SSISDB)에 저장하는지 아니면 msdb 데이터베이스에 저장하는지에 따라 달라집니다.  
  
## SSIS 카탈로그 데이터베이스(SSISDB)의 역할  
 SSIS 카탈로그 데이터베이스(SSISDB)는 패키지에 대한 액세스 및 패키지 관련 정보를 보호하는 데 사용할 수 있는 다음과 같은 고정 데이터베이스 수준 역할을 제공합니다.  
  
-   **ssis_admin**. 이 역할은 SSIS 카탈로그 데이터베이스에 대한 모든 관리 권한을 제공합니다.  
  
-   **ssis_logreader** 이 역할은 SSISDB 작업 로그와 관련된 모든 보기에 액세스할 수 있는 권한을 제공합니다.  
  
     보기 목록에는 [catalog].[projects], [catalog].[packages], [catalog].[operations], [catalog].[extended_operation_info], [catalog].[operation_messages], [catalog].[event_messages], [catalog].[execution_data_statistics], [catalog].[execution_component_phases], [catalog].[execution_data_taps], [catalog].[event_message_context], [catalog].[executions], [catalog].[executables], [catalog].[executable_statistics], [catalog].[validations], [catalog].[execution_parameter_values] 및 [catalog].[execution_property_override_values]가 포함됩니다.  
  
## msdb 데이터베이스의 역할  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 **msdb** 데이터베이스에 저장되는 패키지에 대한 액세스를 제어하기 위한 3가지 고정 데이터베이스 수준 역할인 **db_ssisadmin**, **db_ssisltduser** 및 **db_ssisoperator**가 포함되어 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 패키지에 역할을 할당하십시오. 역할 할당은 **msdb** 데이터베이스에 저장됩니다.  
  
### 읽기 및 쓰기 작업  
 다음 표에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 내에서 Windows 및 고정 데이터베이스 수준 역할의 읽기/쓰기 동작에 대해 설명합니다.  
  
|역할|읽기 동작|쓰기 동작|  
|----------|-----------------|------------------|  
|**db_ssisadmin**<br /><br /> 또는<br /><br /> **sysadmin**|자체 패키지를 열거합니다.<br /><br /> 모든 패키지를 열거합니다.<br /><br /> 자체 패키지를 봅니다.<br /><br /> 모든 패키지를 봅니다.<br /><br /> 자체 패키지를 실행합니다.<br /><br /> 모든 패키지를 실행합니다.<br /><br /> 자체 패키지를 내보냅니다.<br /><br /> 모든 패키지를 내보냅니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 모든 패키지를 실행합니다.|패키지를 가져옵니다.<br /><br /> 자체 패키지를 삭제합니다.<br /><br /> 모든 패키지를 삭제합니다.<br /><br /> 자체 패키지 역할을 변경합니다.<br /><br /> 모든 패키지 역할을 변경합니다.<br /><br /> <br /><br /> **\*\* 경고 \*\***db_ssisadmin 및 dc_admin 역할의 멤버는 해당 권한을 sysadmin으로 승격할 수 있습니다. 이러한 권한 승격이 발생할 수 있는 것은 이러한 역할이 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 수정할 수 있고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 sysadmin 보안 컨텍스트를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 패키지를 실행할 수 있기 때문입니다. 유지 관리 계획, 데이터 컬렉션 집합 및 기타 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 실행할 때 이러한 권한 상승이 발생하지 않도록 하려면 패키지를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업이 제한된 권한을 갖는 프록시 계정을 사용하도록 구성하거나 db_ssisadmin 및 dc_admin 역할에 sysadmin 멤버만 추가합니다.|  
|**db_ssisltduser**|자체 패키지를 열거합니다.<br /><br /> 모든 패키지를 열거합니다.<br /><br /> 자체 패키지를 봅니다.<br /><br /> 자체 패키지를 실행합니다.<br /><br /> 자체 패키지를 내보냅니다.|패키지를 가져옵니다.<br /><br /> 자체 패키지를 삭제합니다.<br /><br /> 자체 패키지 역할을 변경합니다.|  
|**db_ssisoperator**|모든 패키지를 열거합니다.<br /><br /> 모든 패키지를 봅니다.<br /><br /> 모든 패키지를 실행합니다.<br /><br /> 모든 패키지를 내보냅니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 모든 패키지를 실행합니다.|InclusionThresholdSetting|  
|**Windows 관리자**|실행 중인 모든 패키지의 실행 세부 사항을 봅니다.|실행 중인 모든 패키지를 중지합니다.|  
  
### Sysssispackages 테이블  
 **msdb** 의 **sysssispackages** 테이블에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 저장되는 패키지가 포함됩니다. 자세한 내용은 [sysssispackages&#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysssispackages-transact-sql.md)를 참조하세요.  
  
 **sysssispackages** 테이블에는 패키지로 할당되는 역할에 대한 정보가 들어 있는 열이 포함됩니다.  
  
-   **readerrole** 열은 패키지에 읽기 액세스를 가진 역할을 지정합니다.  
  
-   **writerrole** 열은 패키지에 쓰기 액세스를 가진 역할을 지정합니다.  
  
-   **ownersid** 열은 패키지를 만든 사용자의 고유 보안 식별자를 포함하며 패키지의 소유자를 정의합니다.  
  
### Permissions  
 기본적으로 패키지의 읽기 역할에는 **db_ssisadmin** 및 **db_ssisoperator** 고정 데이터베이스 수준 역할의 사용 권한과 패키지를 만든 사용자의 고유 보안 식별자가 적용되고 쓰기 역할에는 **db_ssisadmin** 역할의 사용 권한과 패키지를 만든 사용자의 고유 보안 식별자가 적용됩니다. 패키지에 대한 읽기 액세스 권한을 가지려면 **db_ssisadmin**, **db_ssisltduser** 또는 **db_ssisoperator** 역할의 멤버여야 하고 쓰기 권한을 가지려면 **db_ssisadmin** 역할의 멤버여야 합니다.  
  
### 패키지에 대한 액세스  
 고정 데이터 수준 역할은 사용자 정의 역할과 함께 작동합니다. 사용자 정의 역할은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 만들며 패키지에 권한을 할당하는 데 사용되는 역할입니다. 패키지에 액세스하려면 해당 사용자가 사용자 정의 역할 및 적절한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 고정 데이터베이스 수준 역할의 멤버여야 합니다. 예를 들어 사용자가 패키지에 할당된 **AuditUsers** 사용자 정의 역할의 멤버인 경우 패키지에 대한 읽기 권한을 가지려면 **db_ssisadmin**, **db_ssisltduser** 또는 **db_ssisoperator** 역할의 멤버여야 합니다.  
  
 패키지에 사용자 정의 역할을 할당하지 않은 경우 패키지에 대한 액세스는 고정 데이터베이스 수준 역할에 의해 결정됩니다.  
  
 사용자 정의 역할을 사용하려면 패키지에 할당하기 전에 **msdb** 데이터베이스에 역할을 추가해야 합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 새 데이터베이스 역할을 만들 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터베이스 수준 역할은 msdb 데이터베이스의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 시스템 테이블에 대한 권한을 부여합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER 서비스)를 데이터베이스 엔진에 연결하고 **msdb** 데이터베이스에 액세스하기 전에 시작해야 합니다.  
  
 패키지에 역할을 할당하려면 다음 태스크를 완료해야 합니다.  
  
-   **개체 탐색기를 열어 Integration Services에 연결**  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 패키지에 역할을 할당하기 전에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 개체 탐색기를 열고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 연결해야 합니다.  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 연결하기 전에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]서비스를 시작해야 합니다.  
  
-   **패키지에 읽기 및 쓰기 역할 할당**  
  
     각 패키지에 읽기 및 쓰기 역할을 할당할 수 있습니다.  
  
## 관련 작업  
  
-   [패키지에 읽기 및 쓰기 역할 할당](../../integration-services/service/assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [사용자 정의 역할 만들기](../../integration-services/service/create-a-user-defined-role.md)  
  
-   [Integration Services에 연결](../../integration-services/service/connect-to-integration-services.md)  
  
  