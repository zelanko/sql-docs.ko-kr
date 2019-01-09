---
title: 보안 개요(Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- Integration Services, security
- security [Integration Services], about security
- passwords [Integration Services]
- packages [Integration Services], security
- SQL Server Integration Services, security
- SSIS, security
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 01aa0b88-d477-4581-9a3b-2efc3de2b133
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 35376c36361bd7453ed925c8b0be5721aa120037
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52761205"
---
# <a name="security-overview-integration-services"></a>보안 개요(Integration Services)
   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 보안은 풍부하고 유연한 보안 환경을 제공하는 여러 계층으로 구성되어 있습니다. 이러한 보안 계층에서는 디지털 서명, 패키지 속성, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 역할 및 운영 체제 권한을 사용합니다. 이러한 보안 기능은 대부분 ID 및 액세스 제어라는 범주에 해당합니다.  
  
## <a name="identity-features"></a>ID 기능  
 패키지에서 ID 기능을 구현하면 다음과 같은 목표를 달성할 수 있습니다.  
  
 **출처를 신뢰할 수 있는 패키지만 열고 실행할 수 있습니다**.  
  
 출처를 신뢰할 수 있는 패키지만 열고 실행하려면 우선 패키지의 원래 출처를 식별해야 합니다. 패키지를 인증서로 서명하면 원래 출처를 식별할 수 있습니다. 그런 다음 패키지를 열거나 실행할 때 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 디지털 서명의 존재 여부와 유효성을 확인할 수 있습니다. 자세한 내용은 [디지털 서명을 사용하여 패키지 원본 확인](identify-the-source-of-packages-with-digital-signatures.md)을 참조하세요.  
  
## <a name="access-control-features"></a>액세스 제어 기능  
 패키지에서 ID 기능을 구현하면 다음과 같은 목표를 달성할 수 있습니다.  
  
 **권한 있는 사용자만 패키지를 열고 실행할 수 있습니다**.  
  
 권한 있는 사용자만 패키지를 열고 실행할 수 있게 하려면 다음과 같은 정보에 대한 액세스를 제어해야 합니다.  
  
-   기밀 데이터를 비롯한 패키지의 콘텐츠  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장된 패키지 및 패키지 구성  
  
-   패키지 및 관련 파일(파일 시스템에 저장된 구성, 로그 및 검사점 파일)  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 및 이 서비스에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 표시하는 패키지 관련 정보  
  
### <a name="controlling-access-to-the-contents-of-packages"></a>패키지 콘텐츠에 대한 액세스 제어  
 패키지의 ProtectionLevel 속성을 설정하여 패키지를 암호화하면 패키지 콘텐츠에 대한 액세스를 제한하는 데 도움이 됩니다. 이 속성을 패키지에 필요한 보호 수준으로 설정할 수 있습니다. 예를 들어 팀 개발 환경에서는 패키지에 대한 작업을 수행하는 팀 멤버에게만 알려진 암호를 사용하여 패키지를 암호화할 수 있습니다.  
  
 패키지의 ProtectionLevel 속성을 설정하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 자동으로 중요한 속성을 감지하고 지정된 패키지 보호 수준에 따라 이러한 속성을 처리합니다. 예를 들어 암호를 사용하여 중요한 정보를 암호화하는 수준으로 패키지의 ProtectionLevel 속성을 설정하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 자동으로 모든 중요 속성의 값을 암호화하고, 정확한 암호를 입력하지 않으면 해당 데이터가 표시되지 않습니다.  
  
 일반적으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 암호나 연결 문자열 등의 정보가 들어 있거나 변수 또는 태스크 생성 XML 노드에 해당하는 속성을 중요한 속성으로 식별합니다. 특정 속성이 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 중요한 속성으로 간주되는지 여부는 연결 관리자나 태스크와 같은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소의 개발자가 속성을 중요한 것으로 지정했는지 여부에 따라 달라집니다. 사용자는 중요한 것으로 간주되는 속성 목록에서 속성을 추가하거나 제거할 수 없습니다. 사용자 지정 태스크, 연결 관리자 또는 데이터 흐름 구성 요소를 작성하는 경우에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 중요한 것으로 취급할 속성을 지정할 수 있습니다.  
  
 자세한 내용은 [Access Control for Sensitive Data in Packages](access-control-for-sensitive-data-in-packages.md)을 참조하세요.  
  
### <a name="controlling-access-to-packages"></a>패키지에 대한 액세스 제어  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 msdb 데이터베이스에 저장할 수도 있고, 파일 이름 확장명이 .dtsx인 XML 파일로 파일 시스템에 저장할 수도 있습니다. 자세한 내용은 [패키지 저장](../save-packages.md)을 참조하세요.  
  
#### <a name="saving-packages-to-the-msdb-database"></a>패키지를 msdb 데이터베이스에 저장  
 패키지를 msdb 데이터베이스에 저장하면 서버, 데이터베이스 및 테이블 수준에서 보안이 제공됩니다. msdb 데이터베이스에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지는 sysssispackages 테이블에 저장됩니다. 패키지는 msdb 데이터베이스의 sysssispackages 및 sysdtspackages 테이블에 저장되므로 msdb 데이터베이스를 백업하면 패키지가 자동으로 백업됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 데이터베이스에 저장된 패키지는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터베이스 수준 역할을 적용하여 보호될 수도 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 패키지에 대한 액세스를 제어하기 위한 3가지 고정 데이터베이스 수준 역할인 db_ssisadmin, db_ssisltduser 및 db_ssisoperator가 있습니다. 읽기 및 쓰기 역할을 각 패키지와 연결할 수 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 사용할 데이터베이스 수준 사용자 지정 역할을 정의할 수도 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 msdb 데이터베이스에 저장된 패키지에만 역할을 구현할 수 있습니다. 자세한 내용은 [Integration Services 경로&#40;SSIS Service&#41;](integration-services-roles-ssis-service.md)를 참조하세요.  
  
#### <a name="saving-packages-to-the-file-system"></a>파일 시스템에 패키지 저장  
 패키지를 msdb 데이터베이스 대신 파일 시스템에 저장하는 경우 패키지 파일 및 패키지 파일이 들어 있는 폴더에 대한 보안을 설정해야 합니다.  
  
### <a name="controlling-access-to-files-used-by-packages"></a>패키지에서 사용되는 파일에 대한 액세스 제어  
 구성, 검사점 및 로깅을 사용하도록 구성된 패키지는 패키지 외부에 저장되는 정보를 생성합니다. 이 정보는 중요할 수 있으므로 보호되어야 합니다. 검사점 파일은 파일 시스템에만 저장할 수 있지만 구성과 로그는 파일 시스템 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 테이블에 저장할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 저장된 구성 및 로그에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안이 적용되지만 파일 시스템에 기록된 정보에는 추가 보안이 필요합니다.  
  
 자세한 내용은 [패키지에서 사용되는 파일 액세스](../access-to-files-used-by-packages.md)를 참조하세요.  
  
#### <a name="storing-package-configurations-securely"></a>안전한 패키지 구성 저장  
 패키지 구성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 테이블이나 파일 시스템에 저장할 수 있습니다.  
  
 msdb 데이터베이스뿐 아니라 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 구성을 저장할 수 있습니다. 따라서 패키지 구성의 리포지토리로 사용할 데이터베이스를 지정할 수 있습니다. 또한 구성을 포함할 테이블의 이름을 지정하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 올바른 구조를 갖춘 테이블을 자동으로 만듭니다. 구성을 테이블에 저장하면 서버, 데이터베이스 및 테이블 수준에서 보안을 제공할 수 있습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 저장된 구성은 해당 데이터베이스를 백업할 때 자동으로 백업됩니다.  
  
 구성을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]대신 파일 시스템에 저장하는 경우 패키지 구성 파일이 들어 있는 폴더에 대한 보안을 설정해야 합니다.  
  
 구성에 대한 자세한 내용은 [Package Configurations](../package-configurations.md)을 참조하십시오.  
  
### <a name="controlling-access-to-the-integration-services-service"></a>Integration Services 서비스에 대한 액세스 제어  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 사용하여 저장된 패키지를 나열합니다. 로컬 및 원격 컴퓨터에 저장된 패키지에 대한 정보를 무단으로 열람하여 개인 정보를 습득할 수 없게 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 실행하는 컴퓨터에 대한 액세스를 제한해야 합니다.  
  
 자세한 내용은 [Integration Services 서비스 액세스](../access-to-the-integration-services-service.md)를 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 다음 목록에는 보안과 관련된 특정 태스크를 수행하는 방법을 보여 주는 항목에 대한 링크가 나와 있습니다.  
  
-   [사용자 정의 역할 만들기](../create-a-user-defined-role.md)  
  
-   [패키지에 읽기 및 쓰기 역할 할당](../assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [레지스트리 값을 설정하여 서명 정책 구현](../implement-a-signing-policy-by-setting-a-registry-value.md)  
  
-   [디지털 인증서를 사용하여 패키지 서명](../sign-a-package-by-using-a-digital-certificate.md)  
  
-   [패키지 보호 수준 설정 또는 변경](../set-or-change-the-protection-level-of-packages.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
