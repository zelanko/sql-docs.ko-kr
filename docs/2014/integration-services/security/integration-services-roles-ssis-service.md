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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 43c1c932565ae3df666be10a1b89794ecd720135
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62766675"
---
# <a name="integration-services-roles-ssis-service"></a>Integration Services 역할(SSIS 서비스)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 패키지에 대 한 액세스를 제어 `db_ssisadmin`하기 위한 세 가지 고정 데이터베이스 수준 역할인, **db_ssisltduser**및 **db_ssisoperator**포함 되어 있습니다. 에서 `msdb` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터베이스에 저장 된 패키지에만 역할을 구현할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 패키지에 역할을 할당하십시오. 역할 할당은 `msdb` 데이터베이스에 저장 됩니다.  
  
## <a name="read-and-write-actions"></a>읽기 및 쓰기 작업  
 다음 표에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]내에서 Windows 및 고정 데이터베이스 수준 역할의 읽기/쓰기 동작에 대해 설명합니다.  
  
|역할|읽기 동작|쓰기 동작|  
|----------|-----------------|------------------|  
|`db_ssisadmin`<br /><br /> 를 실행하거나<br /><br /> `sysadmin`|자체 패키지를 열거합니다.<br /><br /> 모든 패키지를 열거합니다.<br /><br /> 자체 패키지를 봅니다.<br /><br /> 모든 패키지를 봅니다.<br /><br /> 자체 패키지를 실행합니다.<br /><br /> 모든 패키지를 실행합니다.<br /><br /> 자체 패키지를 내보냅니다.<br /><br /> 모든 패키지를 내보냅니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 모든 패키지를 실행합니다.|패키지를 가져옵니다.<br /><br /> 자체 패키지를 삭제합니다.<br /><br /> 모든 패키지를 삭제합니다.<br /><br /> 자체 패키지 역할을 변경합니다.<br /><br /> 모든 패키지 역할을 변경합니다.<br /><br /> <br /><br /> ** \* 중요 \* \* ** Db_ssisadmin 역할 및 dc_admin 역할의 멤버는 해당 권한을 sysadmin으로 승격할 수 있습니다. 이러한 권한 승격이 발생할 수 있는 것은 이러한 역할이 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 수정할 수 있고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 sysadmin 보안 컨텍스트를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 패키지를 실행할 수 있기 때문입니다. 유지 관리 계획, 데이터 컬렉션 집합 및 기타 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 실행할 때 이러한 권한 상승이 발생하지 않도록 하려면 패키지를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업이 제한된 권한을 갖는 프록시 계정을 사용하도록 구성하거나 db_ssisadmin 및 dc_admin 역할에 sysadmin 멤버만 추가합니다.|  
|**db_ssisltduser**|자체 패키지를 열거합니다.<br /><br /> 모든 패키지를 열거합니다.<br /><br /> 자체 패키지를 봅니다.<br /><br /> 자체 패키지를 실행합니다.<br /><br /> 자체 패키지를 내보냅니다.|패키지를 가져옵니다.<br /><br /> 자체 패키지를 삭제합니다.<br /><br /> 자체 패키지 역할을 변경합니다.|  
|**db_ssisoperator**|모든 패키지를 열거합니다.<br /><br /> 모든 패키지를 봅니다.<br /><br /> 모든 패키지를 실행합니다.<br /><br /> 모든 패키지를 내보냅니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 모든 패키지를 실행합니다.|없음|  
|**Windows 관리자**|실행 중인 모든 패키지의 실행 세부 사항을 봅니다.|실행 중인 모든 패키지를 중지합니다.|  
  
## <a name="sysssispackages-table"></a>Sysssispackages 테이블  
 `msdb` 의 **sysssispackages** 테이블에는에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]저장 된 패키지가 포함 됩니다. 자세한 내용은 [sysssispackages&#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysssispackages-transact-sql)를 참조하세요.  
  
 **sysssispackages** 테이블에는 패키지로 할당되는 역할에 대한 정보가 들어 있는 열이 포함됩니다.  
  
-   **readerrole** 열은 패키지에 읽기 액세스를 가진 역할을 지정합니다.  
  
-   **writerrole** 열은 패키지에 쓰기 액세스를 가진 역할을 지정합니다.  
  
-   **ownersid** 열은 패키지를 만든 사용자의 고유 보안 식별자를 포함하며 패키지의 소유자를 정의합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 `db_ssisadmin` 및 **db_ssisoperator** 고정 데이터베이스 수준 역할의 사용 권한과 패키지를 만든 사용자의 고유 보안 식별자는 패키지에 대 한 읽기 권한자 역할 및 해당 `db_ssisadmin` 역할의 사용 권한과 패키지를 만든 사용자의 고유 보안 식별자가 기록기 역할에 적용 됩니다. 사용자는 패키지에 대 한 읽기 액세스 `db_ssisadmin`권한을 보유 하려면, **db_ssisltduser**또는 **db_ssisoperator** 역할의 멤버 여야 합니다. 사용자는 쓰기 권한을 갖도록 `db_ssisadmin` 역할의 멤버 여야 합니다.  
  
## <a name="access-to-packages"></a>패키지에 대한 액세스  
 고정 데이터 수준 역할은 사용자 정의 역할과 함께 작동합니다. 사용자 정의 역할은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 만들며 패키지에 권한을 할당하는 데 사용되는 역할입니다. 패키지에 액세스하려면 해당 사용자가 사용자 정의 역할 및 적절한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 고정 데이터베이스 수준 역할의 멤버여야 합니다. 예를 들어 사용자가 패키지에 할당 된 **auditusers** 사용자 정의 역할의 멤버인 경우에는 패키지에 대 한 읽기 액세스 권한이 있는, `db_ssisadmin` **db_ssisltduser**또는 **db_ssisoperator** 역할의 멤버 이기도 해야 합니다.  
  
 패키지에 사용자 정의 역할을 할당하지 않은 경우 패키지에 대한 액세스는 고정 데이터베이스 수준 역할에 의해 결정됩니다.  
  
 사용자 정의 역할을 사용 하려면 패키지에 할당 하기 전에 `msdb` 데이터베이스에 해당 역할을 추가 해야 합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 새 데이터베이스 역할을 만들 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터베이스 수준 역할은 msdb 데이터베이스의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 시스템 테이블에 대한 권한을 부여합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터베이스 엔진에 연결 하 여 데이터베이스에 `msdb` 액세스 하려면 먼저 (MSSQLSERVER 서비스)를 시작 해야 합니다.  
  
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
  
  
