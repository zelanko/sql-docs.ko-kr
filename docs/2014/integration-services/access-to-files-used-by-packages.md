---
title: 패키지에서 사용 하는 파일에 대 한 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- packages [Integration Services], security
- configuration files [Integration Services]
- checkpoint files
- Integration Services packages, security
- logs [Integration Services], security
- files [Integration Services], security
- SQL Server Integration Services packages, security
ms.assetid: 2e3ddea9-5289-4289-a70e-11c018f34977
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c0dbc5c5c72b6c69a6d2d390ac6c2c8920a19332
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66062184"
---
# <a name="access-to-files-used-by-packages"></a>패키지에서 사용되는 파일 액세스
  패키지 보호 수준은 패키지 외부에 저장된 파일을 보호하지 않습니다. 이러한 파일은 다음과 같습니다.  
  
-   구성 파일  
  
-   검사점 파일  
  
-   로그 파일  
  
 이러한 파일은 특히 중요한 정보를 포함하고 있을 경우 별도로 보호해야 합니다.  
  
## <a name="configuration-files"></a>구성 파일  
 구성에 로그인 및 암호 정보와 같은 중요한 정보가 포함된 경우 구성을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 저장하거나 ACL(액세스 제어 목록)을 사용하여 파일이 저장된 위치나 폴더에 대한 액세스를 제한하고 특정 계정에만 액세스할 수 있도록 해야 합니다. 일반적으로 패키지를 실행하도록 허용할 계정이나 구성, 검사점 및 로그 파일의 내용에 대한 검토를 비롯하여 패키지를 관리하고 문제를 해결하는 계정에 대해 액세스 권한을 부여합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 서버 및 데이터베이스 수준에서 보호하므로 보다 안전한 스토리지를 제공합니다. 구성을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 저장하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 유형을 사용하고 파일 시스템을 저장하려면 XML 구성 유형을 사용합니다.  
  
 자세한 내용은 [패키지 구성](../../2014/integration-services/package-configurations.md), [패키지 구성 만들기](../../2014/integration-services/create-package-configurations.md)및 [SQL Server 설치에 대한 보안 고려 사항](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)을 참조하세요.  
  
## <a name="checkpoint-files"></a>검사점 파일  
 이와 비슷하게 패키지에서 사용되는 검사점 파일에 중요한 정보가 들어 있는 경우 ACL(액세스 제어 목록)을 사용하여 파일 저장 위치 또는 폴더를 보호해야 합니다. 검사점 파일은 패키지 진행 중에 현재 상태 정보와 현재 변수 값을 저장합니다. 예를 들어 패키지에는 전화 번호가 포함된 사용자 지정 변수가 포함될 수 있습니다. 자세한 내용은 [검사점을 사용하여 패키지 다시 시작](packages/restart-packages-by-using-checkpoints.md)을 참조하세요.  
  
## <a name="log-files"></a>로그 파일  
 파일 시스템에 기록된 로그 항목도 ACL(액세스 제어 목록)을 사용하여 보호되어야 합니다. 로그 항목을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 테이블에 저장하고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 보안으로 보호할 수도 있습니다. 로그 항목에는 중요한 정보가 포함될 수 있습니다. 예를 들어 패키지에 전화 번호를 참조하는 SQL 문을 구성하는 SQL 실행 태스크가 포함되는 경우 SQL 문에 대한 로그 항목에는 전화 번호가 포함됩니다. SQL 문은 또한 데이터베이스에 있는 테이블 및 열 이름에 대한 개인 정보를 제공합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](performance/integration-services-ssis-logging.md)을 참조하세요.  
  
  
