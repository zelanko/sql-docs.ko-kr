---
title: 포함된 데이터베이스 사용자 - 이식 가능한 데이터베이스 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- contained database, users
- user [SQL Server], about contained database users
ms.assetid: e57519bb-e7f4-459b-ba2f-fd42865ca91d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a10f892c8fd635892d76061e9f33649340e69593
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62655485"
---
# <a name="contained-database-users---making-your-database-portable"></a>포함된 데이터베이스 사용자 - 이식 가능한 데이터베이스 만들기
  포함된 데이터베이스 사용자를 사용하여 데이터베이스 수준에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 연결을 인증합니다. 포함된 데이터베이스는 다른 데이터베이스 및 해당 데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/[!INCLUDE[ssSDS](../../includes/sssds-md.md)] (및 master 데이터베이스) 인스턴스에서 격리된 데이터베이스입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 Windows 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 위해 포함된 데이터베이스 사용자를 지원합니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]을(를) 사용하는 경우, 포함된 데이터베이스 사용자와 데이터베이스 수준 방화벽 규칙을 조합합니다. 이 항목은 포함된 데이터베이스 모델을 사용할 때와 기존의 로그인/사용자 모델 및 Windows 또는 서버 수준 방화벽 규칙을 사용할 때를 비교하여 그 차이점과 장점을 검토합니다. 특정 시나리오의 경우, 관리 효율성 또는 애플리케이션 비즈니스 논리는 여전히 기존의 로그인/사용자 모델 및 서버 수준 방화벽 규칙을 사용해야 할 수도 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 이(가) [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서비스를 발전시키고 보다 높게 보장된 SLA로 이동함에 따라, 지정된 데이터베이스에 대해 가용성 SLA와 최대 로그인 속도를 더 높이기 위하여 포함된 데이터베이스 사용자 모델 및 데이터베이스 범위 방화벽 규칙으로 전환이 필요할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 은(는) 지금 이러한 변경 사항을 고려할 것을 권장합니다.  
  
## <a name="traditional-login-and-user-model"></a>기존의 로그인/사용자 모델  
 기존 연결 모델에서 Windows 사용자 또는 Windows 그룹의 구성원은 Windows에서 인증된 사용자 또는 그룹 자격 증명을 제공하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결합니다. 또는 연결에 이름과 암호를 모두 제공하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증( [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 연결 시 유일한 옵션)을 사용하여 연결합니다. 두 경우 모두 master 데이터베이스에 연결 자격 증명과 일치하는 로그인 정보가 반드시 있어야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 Windows 인증 자격 증명을 승인하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 자격 증명을 인증한 후에 연결은 일반적으로 사용자 데이터베이스에 연결을 시도합니다. 사용자 데이터베이스에 연결하려면 로그인은 사용자 데이터베이스에 포함된 데이터베이스 사용자와 매핑(즉, 연결)될 수 있어야 합니다. 연결 문자열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 선택 사항이지만 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서는 필수인 특정 데이터베이스에 연결을 지정할 수 있습니다.  
  
 중요한 원칙은 로그인(master 데이터베이스에 포함된)과 사용자(사용자 데이터베이스에 포함된)가 반드시 존재해야 하며 서로 관련되어 있어야 한다는 것입니다. 이는 사용자 데이터베이스에 대한 연결이 master 데이터베이스의 로그인에 종속성을 갖고 있으며 이것은 데이터베이스가 다른 호스팅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 서버로 이동될 수 있는 역량을 제한합니다. 어떤 이유로 든 장애 조치 (failover)가 진행 중인 경우와 같이 master 데이터베이스에 대 한 연결을 사용할 수 없는 경우 전체 연결 시간이 증가 하거나 연결 시간이 초과 될 수 있습니다. 따라서 연결 확장성이 줄어들 수 있습니다.  
  
## <a name="contained-database-user-model"></a>포함된 데이터베이스 사용자 모델  
 포함된 데이터베이스 사용자 모델에서 master 데이터베이스의 로그인은 존재하지 않습니다. 대신 인증 프로세스가 사용자 데이터베이스에서 일어나며 사용자 데이터베이스에 포함된 데이터베이스 사용자는 master 데이터베이스에 연관된 로그인을 갖지 않습니다. 포함된 데이터베이스 사용자 모델은 Windows 인증( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의) 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]의) 모두를 지원합니다. 포함된 데이터베이스 사용자로 연결하려면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 인증 프로세스를 관리할 책임이 있는 데이터베이스를 알 수 있도록 연결 문자열은 사용자 데이터베이스에 대한 매개 변수를 항상 포함해야 합니다. 포함된 데이터베이스 사용자의 활동은 데이터베이스 인증으로 제한되기 때문에 포함된 데이터베이스 사용자로 연결하는 경우 데이터베이스 사용자 계정은 반드시 사용자가 필요로 하는 각각의 데이터베이스에 독립적으로 생성되어야 합니다. 데이터베이스를 변경하려면 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 사용자가 새 연결을 만들어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 포함된 데이터베이스 사용자는 동일한 사용자가 다른 데이터베이스에 존재하면 데이터베이스를 변경할 수 있습니다.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]의 경우, 기존 모델에서 포함된 데이터베이스 사용자 모델로 전환 시 연결 문자열에 대한 변경이 필요치 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결은 데이터베이스 이름이 (이미 존재하지 않는 경우) 연결 문자열에 반드시 추가되어야 합니다.  
  
> [!IMPORTANT]  
>  기존 모델을 사용하는 경우, 서버 수준 역할 및 서버 수준 권한은 모든 데이터베이스에 대한 액세스를 제한할 수 있습니다. 포함된 데이터베이스 모델을 사용하는 경우, 데이터베이스 소유자와 ALTER ANY USER 권한이 있는 데이터베이스 사용자는 데이터베이스에 대한 액세스를 부여할 수 있습니다. 이것은 고급 권한 서버 로그인의 액세스 제어를 줄이고 고급 권한 데이터베이스 사용자에 대한 액세스 제어를 확장합니다.  
  
## <a name="firewalls"></a>방화벽  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Windows 방화벽 규칙은 모든 연결에 적용되며 로그인(기존 모델 연결) 및 포함된 데이터베이스 사용자에 동일한 효력을 갖습니다. Windows 방화벽에 대한 자세한 내용은 [데이터베이스 엔진 액세스에 대한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)을(를) 참조하세요.  
  
### <a name="sssds-firewalls"></a>[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 방화벽  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]는 여러 수준 연결(로그인) 및 데이터베이스 수준 연결(포함된 데이터베이스 사용자)에 대해 별도의 방화벽 규칙을 허용합니다. 사용자 데이터베이스에 연결할 때 첫 번째 데이터베이스 방화벽 규칙이 확인됩니다. 데이터베이스에 액세스를 허용하는 규칙이 없는 경우, 서버 수준 방화벽 규칙이 확인되고 논리 서버 master 데이터베이스에 대한 액세스가 필요합니다. 포함된 데이터베이스 사용자와 결합된 데이터베이스 수준 방화벽 규칙은 연결 시 서버의 master 데이터베이스에 액세스할 필요가 없고 향상된 연결 확장성을 제공합니다.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 방화벽 규칙에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [Azure SQL 데이터베이스 방화벽](https://msdn.microsoft.com/library/azure/ee621782.aspx)  
  
-   [방법: 방화벽 설정 구성(Azure SQL Database)](https://msdn.microsoft.com/library/azure/jj553530.aspx)  
  
-   [sp_set_firewall_rule&#40;Azure SQL 데이터베이스&#41;](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
-   [sp_set_database_firewall_rule&#40;Azure SQL 데이터베이스&#41;](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
## <a name="syntax-differences"></a>구문 차이  
  
|기존 모델|포함된 데이터베이스 사용자 모델|  
|-----------------------|-----------------------------------|  
|master 데이터베이스에 연결하는 경우:<br /><br /> `CREATE LOGIN login_name  WITH PASSWORD = 'strong_password';`<br /><br /> 사용자 데이터베이스에 연결하는 경우:<br /><br /> `CREATE USER 'user_name' FOR LOGIN 'login_name';`|사용자 데이터베이스에 연결하는 경우:<br /><br /> `CREATE USER user_name  WITH PASSWORD = 'strong_password';`|  
  
|기존 모델|포함된 데이터베이스 사용자 모델|  
|-----------------------|-----------------------------------|  
|master DB의 컨텍스트에서 암호를 변경하려면:<br /><br /> `ALTER LOGIN login_name  WITH PASSWORD = 'strong_password';`|사용자 DB의 컨텍스트에서 암호를 변경하려면:<br /><br /> `ALTER USER user_name  WITH PASSWORD = 'strong_password';`|  
  
## <a name="remarks"></a>설명  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 포함된 데이터베이스 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대해 설정되어야 합니다. 자세한 내용은 [contained database authentication Server Configuration Option](../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md)을 참조하세요.  
  
-   겹치지 않는 이름을 가진 포함된 데이터베이스 사용자와 로그인은 애플리케이션에서 공존할 수 있습니다.  
  
-   **name1** 이라는 이름으로 마스터 데이터베이스에 로그인하고 **name1**이라는 이름으로 포함된 데이터베이스 사용자를 만들면, 데이터베이스 이름이 연결 문자열에 제공되는 경우, 데이터베이스에 연결할 때 데이터베이스 사용자의 컨텍스트는 로그인 컨텍스트보다 우선하여 선택됩니다. 즉, 포함된 데이터베이스 사용자가 동일한 이름의 로그인보다 우선합니다.  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에서 포함된 데이터베이스 사용자의 이름은 서버 관리자 계정의 이름과 같을 수 없습니다.  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버 관리자 계정은 포함된 데이터베이스 사용자일 수 없습니다. 서버 관리자에는 포함된 데이터베이스 사용자를 만들고 관리하는 데 충분한 권한이 있습니다. 서버 관리자는 사용자 데이터베이스의 포함된 데이터베이스 사용자에게 권한을 부여할 수 있습니다.  
  
-   포함된 데이터베이스 사용자가 데이터베이스 수준의 주체이기 때문에, 사용하려는 모든 데이터베이스에 포함된 데이터베이스 사용자를 만들어야 합니다. ID는 데이터베이스에만 한정되며 동일한 서버에 있는 다른 데이터베이스의 동일한 이름과 동일한 암호를 가진 사용자와는 모든 면에서 관련이 없습니다.  
  
-   일반적으로 사용하는 것과 동일한 강도의 암호를 사용하여 로그인합니다.  
  
## <a name="see-also"></a>참고 항목  
 [포함 된 데이터베이스](../databases/contained-databases.md)   
 [포함 된 데이터베이스의 보안 모범 사례](../databases/security-best-practices-with-contained-databases.md)   
 [CREATE USER&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)  
  
  
