---
title: 데이터베이스 만들기 마법사
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.createdbwiz.f1
ms.assetid: 45fe7a23-a46c-4d40-8bca-3431fbfc5c9d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a5ed33054cc497761775a83eba8d023fe215fcd9
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729430"
---
# <a name="create-database-wizard-master-data-services-configuration-manager"></a>데이터베이스 만들기 마법사(Master Data Services 구성 관리자)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  **데이터베이스 만들기** 마법사를 사용하여 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스를 만들 수 있습니다.  
  
## <a name="database-server"></a>데이터베이스 서버  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 데이터베이스를 호스팅하는 로컬 또는 원격 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 인스턴스에 연결할 정보를 지정합니다. 원격 인스턴스에 연결하려면 원격 연결을 설정해야 합니다.  
  
|컨트롤 이름|설명|  
|------------------|-----------------|  
|**SQL Server 인스턴스**|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 데이터베이스를 호스팅할 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 인스턴스의 이름을 지정합니다. 로컬 컴퓨터나 원격 컴퓨터의 기본 또는 명명된 인스턴스를 사용할 수 있습니다. 다음을 입력하여 정보를 지정하십시오.<br /><br /> 마침표(.) - 로컬 컴퓨터의 기본 인스턴스에 연결하려는 경우<br /><br /> 서버 이름 또는 IP 주소 - 지정된 로컬 또는 원격 컴퓨터의 기본 인스턴스에 연결하려는 경우<br /><br /> 서버 이름 또는 IP 주소 및 인스턴스 이름 - 지정된 로컬 또는 원격 컴퓨터의 명명된 인스턴스에 연결하려는 경우. 이 정보는 *server_name*\\*instance_name*형식으로 지정합니다.|  
|**인증 유형**|지정된 SQL Server 인스턴스에 연결할 때 사용할 인증 유형을 선택합니다. 지정된 **인스턴스에 대한** sysadmin [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서버 역할의 일부인 자격 증명을 사용하여 연결해야 합니다. sysadmin 역할에 대한 자세한 내용은 [서버 수준 역할](../relational-databases/security/authentication-access/server-level-roles.md)을 참조하세요.<br /><br /> 인증 유형은 다음과 같습니다.<br /><br /> **현재 사용자 – 통합 보안**: Windows 통합 인증을 사용하여 현재 Windows 사용자 계정의 자격 증명으로 연결합니다. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 에서는 컴퓨터에 로그온하여 애플리케이션을 연 사용자의 Windows 자격 증명을 사용합니다. 애플리케이션에서 다른 Windows 자격 증명은 지정할 수 없습니다. 다른 Windows 자격 증명으로 연결하려면 해당 사용자로 컴퓨터에 로그온한 다음 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]를 열어야 합니다.<br /><br /> **SQL Server 계정**: SQL Server 계정을 사용하여 연결합니다. 이 옵션을 선택하면 **사용자 이름** 및 **암호** 필드가 활성화됩니다. 이 필드에 지정된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 계정에 대한 자격 증명을 지정해야 합니다.|  
|**사용자 이름**|지정된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용되는 사용자 계정의 이름을 지정합니다. 계정은 지정된 **인스턴스에 대한** sysadmin [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 역할의 일부여야 합니다.<br /><br /> **인증 유형**이 **현재 사용자 – 통합 보안**인 경우 **사용자 이름** 상자는 읽기 전용이며 컴퓨터에 로그온된 Windows 사용자 계정의 이름이 표시됩니다.<br /><br /> **인증 유형** 이 **SQL Server 계정**인 경우 **사용자 이름** 상자가 활성화되며, 지정된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 계정에 대한 자격 증명을 지정해야 합니다.|  
|**암호**|사용자 계정에 연결된 암호를 지정합니다.<br /><br /> **인증 유형**이 **현재 사용자 – 통합 보안**인 경우 **암호** 상자는 읽기 전용이며 지정된 Windows 사용자 계정의 자격 증명을 사용하여 연결합니다.<br /><br /> **인증 유형** 이 **SQL Server 계정**인 경우 **암호** 상자가 활성화되며, 지정된 사용자 계정에 연결된 암호를 지정해야 합니다.|  
|**연결 테스트**|지정된 사용자 계정에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있는지, 그리고 해당 인스턴스에 대해 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스를 만들 수 있는 권한이 있는지 확인합니다. **연결 테스트**를 클릭하지 않은 경우 **다음**을 클릭하면 연결이 테스트됩니다.|  
  
## <a name="database"></a>데이터베이스  
 새 데이터베이스에 대한 데이터베이스 이름 및 데이터 정렬 옵션을 지정합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 데이터 정렬은 데이터에 대한 정렬 규칙과 대/소문자 및 악센트 구분 속성을 제공합니다. char 및 varchar과 같은 문자 데이터 형식과 함께 사용되는 데이터 정렬은 해당 데이터 형식을 나타내는 데 사용할 수 있는 코드 페이지와 해당 문자를 지정합니다. 데이터베이스 데이터 정렬에 대한 자세한 내용은 [데이터 정렬 및 유니코드 지원](../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
|컨트롤 이름|설명|  
|------------------|-----------------|  
|**데이터베이스 이름**|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스 이름을 지정합니다.|  
|**SQL Server 기본 데이터 정렬**|새 데이터베이스에 지정된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스의 현재 데이터베이스 데이터 정렬 설정을 사용하려면 선택합니다.|  
|**Windows 데이터 정렬**|새 데이터베이스에 사용할 Windows 데이터 정렬 설정을 지정합니다. Windows 데이터 정렬은 관련 Windows 로캘을 기반으로 문자 데이터 저장 규칙을 정의합니다. Windows 데이터 정렬 및 관련 옵션에 대한 자세한 내용은 [Windows 데이터 정렬 이름&#40;Transact-SQL&#41;](../t-sql/statements/windows-collation-name-transact-sql.md)을 참조하세요.<br /><br /> 참고: **Windows 데이터 정렬** 목록 및 관련 옵션은 **SQL Server 기본 데이터 정렬** 상자의 선택을 취소한 경우에만 활성화됩니다.|  
  
## <a name="administrator-account"></a>관리자 계정  
  
|컨트롤 이름|설명|  
|------------------|-----------------|  
|**사용자 이름**|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에 대한 기본 슈퍼 사용자를 지정합니다. 슈퍼 사용자는 모든 기능 영역에 액세스할 수 있으며 모든 모델을 추가, 삭제 및 업데이트할 수 있습니다. [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]의 슈퍼 사용자 권한 및 다른 유형의 관리자에 대한 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.|  
  
## <a name="summary"></a>요약  
 선택한 옵션에 대한 요약 정보를 표시합니다. 선택 항목을 검토한 후 **다음** 을 클릭하면 지정된 설정으로 데이터베이스 만들기가 시작됩니다.  
  
## <a name="progress-and-finish"></a>진행 후 마침  
 만들기 프로세스의 진행률을 표시합니다. 데이터베이스가 만들어진 후 **마침** 을 클릭하면 데이터베이스 마법사가 닫히고 **데이터베이스** 페이지로 돌아갑니다. 이 페이지에는 새 데이터베이스가 선택되어 있으며 해당 시스템 설정을 보고 수정할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 구성 페이지&#40;Master Data Services 구성 관리자&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
[Master Data Services 설치 및 구성](../master-data-services/master-data-services-installation-and-configuration.md) [데이터베이스 요구 사항&#40;Master Data Services&#41;](../master-data-services/install-windows/database-requirements-master-data-services.md)  
  
  
