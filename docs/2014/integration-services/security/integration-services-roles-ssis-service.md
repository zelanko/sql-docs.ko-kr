---
title: Integration Services 역할(SSIS 서비스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- security [Integration Services], roles
- db_ssisoperator role
- db_ssisadmin role
- fixed database roles [Integration Services]
- packages [Integration Services], security
- roles [Integration Services]
- db_ssisltduser role
ms.assetid: 9702e90c-fada-4978-a473-1b1423017d80
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9c6f7ef38c779b07b9cbeffc2b9300360620e350
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52792878"
---
# <a name="integration-services-roles-ssis-service"></a>Integration Services 역할(SSIS 서비스)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 세 가지 고정된 데이터베이스 수준 역할을 포함 `db_ssisadmin`, **db_ssisltduser**, 및 **db_ssisoperator**, 패키지에 대 한 액세스를 제어 합니다. 에 저장 된 패키지에만 역할을 구현할 수 있습니다 합니다 `msdb` 데이터베이스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]입니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 패키지에 역할을 할당하십시오. 역할 할당에 저장 되는 `msdb` 데이터베이스입니다.  
  
## <a name="read-and-write-actions"></a>읽기 및 쓰기 작업  
 다음 표에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]내에서 Windows 및 고정 데이터베이스 수준 역할의 읽기/쓰기 동작에 대해 설명합니다.  
  
|역할|읽기 동작|쓰기 동작|  
|----------|-----------------|------------------|  
|`db_ssisadmin`<br /><br /> 로 구분하거나 여러<br /><br /> `sysadmin`|자체 패키지를 열거합니다.<br /><br /> 모든 패키지를 열거합니다.<br /><br /> 자체 패키지를 봅니다.<br /><br /> 모든 패키지를 봅니다.<br /><br /> 자체 패키지를 실행합니다.<br /><br /> 모든 패키지를 실행합니다.<br /><br /> 자체 패키지를 내보냅니다.<br /><br /> 모든 패키지를 내보냅니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 모든 패키지를 실행합니다.|패키지를 가져옵니다.<br /><br /> 자체 패키지를 삭제합니다.<br /><br /> 모든 패키지를 삭제합니다.<br /><br /> 자체 패키지 역할을 변경합니다.<br /><br /> 모든 패키지 역할을 변경합니다.<br /><br /> <br /><br /> **\*\* 중요 \* \***  db_ssisadmin 및 dc_admin 역할의 멤버는 해당 권한을 sysadmin으로 승격할 수 있습니다. 이러한 권한 승격이 발생할 수 있는 것은 이러한 역할이 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 수정할 수 있고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 sysadmin 보안 컨텍스트를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 패키지를 실행할 수 있기 때문입니다. 유지 관리 계획, 데이터 컬렉션 집합 및 기타 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 실행할 때 이러한 권한 상승이 발생하지 않도록 하려면 패키지를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업이 제한된 권한을 갖는 프록시 계정을 사용하도록 구성하거나 db_ssisadmin 및 dc_admin 역할에 sysadmin 멤버만 추가합니다.|  
|**db_ssisadmin**|자체 패키지를 열거합니다.<br /><br /> 모든 패키지를 열거합니다.<br /><br /> 자체 패키지를 봅니다.<br /><br /> 자체 패키지를 실행합니다.<br /><br /> 자체 패키지를 내보냅니다.|패키지를 가져옵니다.<br /><br /> 자체 패키지를 삭제합니다.<br /><br /> 자체 패키지 역할을 변경합니다.|  
|**db_ssisltduser**|모든 패키지를 열거합니다.<br /><br /> 모든 패키지를 봅니다.<br /><br /> 모든 패키지를 실행합니다.<br /><br /> 모든 패키지를 내보냅니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 모든 패키지를 실행합니다.|없음|  
|**Windows 관리자**|실행 중인 모든 패키지의 실행 세부 사항을 봅니다.|실행 중인 모든 패키지를 중지합니다.|  
  
## <a name="sysssispackages-table"></a>Sysssispackages 테이블  
 합니다 **sysssispackages** 테이블의 `msdb` 에 저장 된 패키지가 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 [sysssispackages&#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysssispackages-transact-sql)를 참조하세요.  
  
 **sysssispackages** 테이블에는 패키지로 할당되는 역할에 대한 정보가 들어 있는 열이 포함됩니다.  
  
-   **readerrole** 열은 패키지에 읽기 액세스를 가진 역할을 지정합니다.  
  
-   **writerrole** 열은 패키지에 쓰기 액세스를 가진 역할을 지정합니다.  
  
-   **ownersid** 열은 패키지를 만든 사용자의 고유 보안 식별자를 포함하며 패키지의 소유자를 정의합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 권한 합니다 `db_ssisadmin` 하 고 **db_ssisoperator** 고정된 데이터베이스 수준 역할 및 패키지를 만든 사용자의 고유 보안 식별자의 사용 권한과 패키지를 실행 하는 것에 대 한 읽기 권한자 역할에 적용 `db_ssisadmin` 기록기 역할에 역할 및 패키지를 만든 사용자의 고유 보안 식별자를 적용 합니다. 사용자의 멤버 여야 합니다.는 `db_ssisadmin`, **db_ssisltduser**, 또는 **db_ssisoperator** 역할 패키지에 읽기 권한이 있어야 합니다. 사용자의 멤버 여야 합니다.는 `db_ssisadmin` 쓰기 액세스는 역할입니다.  
  
## <a name="access-to-packages"></a>패키지에 대한 액세스  
 고정 데이터 수준 역할은 사용자 정의 역할과 함께 작동합니다. 사용자 정의 역할은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 만들며 패키지에 권한을 할당하는 데 사용되는 역할입니다. 패키지에 액세스하려면 해당 사용자가 사용자 정의 역할 및 적절한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 고정 데이터베이스 수준 역할의 멤버여야 합니다. 예를 들어, 사용자의 구성원 인 경우는 **AuditUsers** 패키지에 할당 된 사용자 정의 역할에도 야 멤버인 `db_ssisadmin`를 **db_ssisltduser**, 또는 **db_ ssisoperator** 역할 패키지에 읽기 권한이 있어야 합니다.  
  
 패키지에 사용자 정의 역할을 할당하지 않은 경우 패키지에 대한 액세스는 고정 데이터베이스 수준 역할에 의해 결정됩니다.  
  
 에 추가 해야 사용자 정의 역할을 사용 하려는 경우는 `msdb` 패키지에 할당 하기 전에 데이터베이스입니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 새 데이터베이스 역할을 만들 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터베이스 수준 역할은 msdb 데이터베이스의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 시스템 테이블에 대한 권한을 부여합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진 및 액세스에 연결할 수 있습니다 (MSSQLSERVER 서비스) 시작 해야 합니다 `msdb` 데이터베이스입니다.  
  
 패키지에 역할을 할당하려면 다음 태스크를 완료해야 합니다.  
  
-   **개체 탐색기를 열어 Integration Services에 연결**  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 패키지에 역할을 할당하기 전에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 개체 탐색기를 열고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 연결해야 합니다.  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 연결하기 전에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]서비스를 시작해야 합니다.  
  
-   **패키지에 읽기 및 쓰기 역할 할당**  
  
     각 패키지에 읽기 및 쓰기 역할을 할당할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [패키지에 읽기 및 쓰기 역할 할당](../assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [사용자 정의 역할 만들기](../create-a-user-defined-role.md)  
  
-   [Integration Services에 연결](../connect-to-integration-services.md)  
  
  
