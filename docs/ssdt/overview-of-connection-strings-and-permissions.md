---
title: 연결 문자열 및 사용 권한 개요 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: ceff114e-a738-46ad-9785-b6647a2247f9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 413d6ad71b70cc4ddca8205589d25e224bbcad76
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65102028"
---
# <a name="overview-of-connection-strings-and-permissions"></a>연결 문자열 및 사용 권한 개요
SQL Server 단위 테스트를 실행하려면 한 개 또는 두 개의 특정 연결 문자열을 사용하여 데이터베이스 서버에 연결해야 합니다. 각 연결 문자열은 테스트의 일환으로 특정 스크립트의 태스크나 태스크 집합을 수행하기 위해 필요한 특정 사용 권한이 있는 계정을 나타냅니다. **SQL Server 테스트 구성** 대화 상자에서 또는 테스트 프로젝트의 app.config 파일을 수동으로 편집하여 이러한 문자열을 지정할 수 있습니다.  
  
## <a name="connection-strings"></a>연결 문자열  
**SQL Server 테스트 구성** 대화 상자에서 다음 각 계정에 대한 연결 문자열을 지정할 수 있습니다.  
  
> [!NOTE]  
> 실행 컨텍스트와 권한 있는 컨텍스트는 SQL Server 인증을 사용하는 경우에만 다릅니다. Windows 인증을 사용하는 경우에는 두 연결 문자열 모두에 동일한 자격 증명이 사용됩니다.  
  
-   실행 컨텍스트(필수) - 테스트 스크립트를 실행하기 위한 사용자 계정입니다. 이 연결 문자열에는 사용자에게 필요한 자격 증명과 동일한 자격 증명이 있어야 합니다. 이 연결 문자열은 이를 통해 적절한 사용 권한이 데이터베이스에 적용되었음이 확인되므로 중요합니다. 자세한 내용은 [방법: SQL Server 단위 테스트 실행 구성](../ssdt/how-to-configure-sql-server-unit-test-execution.md)을 참조하세요.  
  
    테스트 프로젝트의 app.config 파일에서는 `ExecutionContext` 요소가 이 문자열에 해당합니다.  
  
-   권한 있는 컨텍스트(옵션) - 테스트 전 작업, 테스트 후 작업, TestInitialize 및 TestCleanup 스크립트를 실행하기 위한 높은 권한이 있는 동일한 데이터베이스의 계정입니다. 이러한 스크립트는 데이터베이스 상태를 설정하며 테스트 후 작업의 경우 이러한 스크립트를 사용하여 데이터베이스의 개체에 대한 유효성을 검사할 수 있습니다. 이 연결 문자열은 데이터베이스 변경 내용을 배포하고 데이터를 생성하는 데도 사용됩니다.  
  
    테스트 프로젝트의 app.config 파일에서는 `PrivilegedContext` 요소가 이 문자열에 해당합니다. SQL Server 단위 테스트가 테스트 스크립트만 실행하는 경우에는 권한 있는 컨텍스트를 지정할 필요가 없습니다.  
  
프로젝트 구성 대화 상자에서 지정하는 문자열은 테스트 프로젝트의 app.config 파일에 저장됩니다. 또한 해당 파일을 직접 편집한 후 프로젝트를 다시 빌드할 수도 있으며 그러면 대화 상자에 새 값이 나타납니다.  
  
## <a name="windows-authentication-versus-sql-server-authentication"></a>Windows 인증 및 SQL Server 인증 비교  
연결 문자열을 지정하는 경우 SQL 인증을 사용할지 Windows 인증을 사용할지 선택해야 합니다. Windows 인증을 선택하는 이유 중 하나는 팀에서의 테스트 사용에 대한 지원이 SQL Server 인증의 경우보다 낫기 때문입니다. SQL Server 인증을 선택하면 연결 문자열은 사용자 자격 증명을 기반으로 DPAPI(데이터 보호 API)를 사용하여 암호화됩니다. 즉, 이 테스트 프로젝트의 테스트는 사용자가 테스트를 체크 인한 후 소스 제어 시스템을 통해 테스트를 가져오는 팀 멤버를 위해서가 아니라 해당 사용자를 위해서만 실행됩니다. 이 테스트 프로젝트의 테스트를 실행하려면 팀의 다른 멤버가 자신의 자격 증명을 사용하여 테스트 프로젝트를 다시 구성해야 합니다. 이렇게 하려면 app.config 파일의 복사본을 편집하거나 프로젝트 구성 대화 상자를 사용합니다.  
  
## <a name="permissions"></a>사용 권한  
테스트 스크립트는 실행 컨텍스트 권한 수준에서 실행되며, 이 수준은 일반적인 사용 시 데이터베이스에서 실행되는 사용자 명령에 유효한 사용 권한 수준과 동일한 수준입니다. 테스트 전 작업, 테스트 작업, TestInitialize 및 TestCleanup 스크립트는 권한 있는 컨텍스트 권한 수준에서 실행됩니다.  
  
테스트 후 작업 스크립트에 사용되는 높은 권한 연결로 인해 해당 스크립트 내에서 유효성 검사를 수행할 수 있습니다. 이 스크립트에서는 사용 권한을 테스트하는 스크립트 명령을 실행할 수도 있습니다. 사용 권한에 대한 자세한 내용은 [SQL Server Data Tools에 필요한 권한](../ssdt/required-permissions-for-sql-server-data-tools.md)의 SQL Server 단위 테스트 섹션을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server 단위 테스트의 스크립트](../ssdt/scripts-in-sql-server-unit-tests.md)  
[SQL Server 단위 테스트 파일](../ssdt/sql-server-unit-test-files.md)  
  
