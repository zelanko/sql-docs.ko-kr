---
title: SQL Server Data Tools에 필요한 권한 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: b27038c4-94ab-449c-90b7-29d87ce37a8b
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 1eb77a0990d8f0e19458dd66ea7f73b933de961c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65101848"
---
# <a name="required-permissions-for-sql-server-data-tools"></a>SQL Server Data Tools에 필요한 권한
Visual Studio에서 데이터베이스에 대한 작업을 수행하려면 먼저 해당 데이터베이스에 대한 특정 사용 권한이 있는 계정으로 로그인해야 합니다. 필요한 특정 사용 권한은 수행하려는 작업에 따라 달라집니다. 다음 섹션에서는 수행하려는 각 작업 및 해당 작업을 수행하는 데 필요한 특정 사용 권한에 대해 설명합니다.  
  
-   [데이터베이스를 만들거나 배포할 수 있는 권한](#DatabaseCreationAndDeploymentPermissions)  
  
-   [데이터베이스를 리팩터링할 수 있는 권한](#DatabaseRefactoringPermissions)  
  
-   [SQL Server 데이터베이스에 대한 단위 테스트를 수행할 수 있는 권한](#DatabaseUnitTestingPermissions)  
  
-   [데이터를 생성할 수 있는 권한](#DataGenerationPermissions)  
  
-   [스키마 및 데이터를 비교할 수 있는 권한](#SchemaAndDataComparePermissions)  
  
-   [Transact-SQL 편집기를 실행할 수 있는 권한](#Transact-SQLEditorPermissions)  
  
-   [SQL Server CLR(공용 언어 런타임) 프로젝트에 대한 사용 권한](#SQLCLRPermissions)  
  
## <a name="DatabaseCreationAndDeploymentPermissions"></a>데이터베이스를 만들거나 배포할 수 있는 권한  
데이터베이스를 만들거나 배포하려면 다음과 같은 사용 권한이 있어야 합니다.  
  
|||  
|-|-|  
|동작|필요한 권한|  
|데이터베이스 개체 및 설정 가져오기|원본 데이터베이스에 연결할 수 있어야 합니다.<br /><br />원본 데이터베이스가 SQL Server 2005를 기반으로 하는 경우 각 개체에 대한 **VIEW DEFINITION** 권한도 가지고 있어야 합니다.<br /><br />원본 데이터베이스가 SQL Server 2008 이상을 기반으로 하는 경우 각 개체에 대한 **VIEW DEFINITION** 권한도 가지고 있어야 합니다. 로그인하려면 데이터베이스 암호화 키에 대한 **VIEW SERVER STATE** 권한이 있어야 합니다.|  
|서버 개체 및 설정 가져오기|지정된 서버의 master 데이터베이스에 연결할 수 있어야 합니다.<br /><br />서버에서 SQL Server 2005가 실행 중인 경우 해당 서버에 대한 **VIEW ANY DEFINITION** 권한이 있어야 합니다.<br /><br />원본 데이터베이스가 SQL Server 2008 이상을 기반으로 하는 경우 해당 서버에 대한 **VIEW ANY DEFINITION** 권한이 있어야 합니다. 로그인하려면 데이터베이스 암호화 키에 대한 **VIEW SERVER STATE** 권한이 있어야 합니다.|  
|데이터베이스 프로젝트 만들기 또는 업데이트|데이터베이스 프로젝트를 만들거나 수정할 때는 데이터베이스 권한이 필요하지 않습니다.|  
|새 데이터베이스 배포 또는 **항상 데이터베이스 다시 만들기** 옵션이 설정된 상태에서 배포|대상 서버에 대한 **dbcreator** 역할의 멤버이거나 **CREATE DATABASE** 권한이 있어야 합니다.<br /><br />데이터베이스를 만들 때 Visual Studio는 모델 데이터베이스에 연결하여 데이터베이스 내용을 복사합니다. 대상 데이터베이스에 연결하기 위해 초기 로그인(예: *yourLogin*)하려면 **db_creator** 권한과 **CONNECT SQL** 권한이 있어야 합니다. 이 로그인에는 모델 데이터베이스에 대한 사용자 매핑이 있어야 합니다. **sysadmin** 권한이 있는 경우 다음 Transact\-SQL 문을 실행하여 매핑을 만들 수 있습니다.<br /><br />`USE [model] CREATE USER yourUser FROM LOGIN yourLogin`<br /><br />사용자(이 예에서는 yourUser)는 모델 데이터베이스에 대한 **CONNECT** 권한과 **VIEW DEFINITION** 권한이 있어야 합니다. **sysadmin** 권한이 있는 경우 다음 Transact\-SQL 문을 실행하여 이러한 권한을 부여할 수 있습니다.<br /><br />`USE [model] GRANT CONNECT to yourUser GRANT VIEW DEFINITION TO yourUser`<br /><br />명명되지 않은 제약 조건이 포함되어 있는 데이터베이스를 배포하는 경우 **CheckNewContraints** 옵션(기본적으로 설정되어 있음)이 설정되어 있으면 **db_owner** 권한이나 **sysadmin** 권한이 있어야 하며 그렇지 않은 경우 배포가 실패합니다. 이는 명명되지 않은 제약 조건에만 적용됩니다. **CheckNewConstraints** 옵션에 대한 자세한 내용은 [데이터베이스 프로젝트 설정](../ssdt/database-project-settings.md)을 참조하세요.|  
|기존 데이터베이스에 대한 업데이트 배포|유효한 데이터베이스 사용자여야 합니다. **db_ddladmin** 역할의 멤버이거나 스키마를 소유하거나 대상 데이터베이스에서 만들거나 수정할 개체를 소유해야 합니다. 배포 전 스크립트 또는 배포 후 스크립트에서 연결된 서버 또는 로그인과 같은 고급 개념에 대한 작업을 위해서는 추가 권한이 필요합니다.<br /><br />**참고:** master 데이터베이스를 배포하는 경우 배포할 서버에 대한 **VIEW ANY DEFINITION** 권한도 있어야 합니다.|  
|데이터베이스 프로젝트에서 EXTERNAL_ACCESS 옵션과 함께 어셈블리 사용|데이터베이스 프로젝트에 대한 TRUSTWORTHY 속성을 설정해야 합니다. SQL Server 로그인에 대한 EXTERNAL ACCESS ASSEMBLY 권한이 있어야 합니다.|  
|새 데이터베이스 또는 기본 데이터베이스에 어셈블리 배포|대상 배포 서버에 대한 sysadmin 역할의 멤버여야 합니다.|  
  
자세한 내용은 SQL Server 온라인 설명서를 참조하십시오.  
  
## <a name="DatabaseRefactoringPermissions"></a>데이터베이스를 리팩터링할 수 있는 권한  
*데이터베이스 리팩터링*은 데이터베이스 프로젝트 내에서만 발생합니다. 데이터베이스 프로젝트를 사용할 수 있는 권한이 있어야 합니다. 대상 데이터베이스에 대한 변경 내용을 배포하기 전까지는 대상 데이터베이스에 대한 사용 권한이 필요하지 않습니다.  
  
## <a name="DatabaseUnitTestingPermissions"></a>SQL Server 데이터베이스에 대한 단위 테스트를 수행할 수 있는 권한  
데이터베이스에 대한 단위 테스트를 수행하려면 다음과 같은 사용 권한이 있어야 합니다.  
  
|||  
|-|-|  
|동작|필요한 권한|  
|테스트 작업 실행|실행 컨텍스트 데이터베이스 연결을 사용해야 합니다. 자세한 내용은 [연결 문자열 및 사용 권한 개요](../ssdt/overview-of-connection-strings-and-permissions.md)를 참조하세요.|  
|테스트 전 및 테스트 후 작업 실행|권한 있는 컨텍스트 데이터베이스 연결을 사용해야 합니다. 이 데이터베이스 연결에는 실행 컨텍스트 연결보다 더 많은 사용 권한이 있습니다.|  
|TestInitialize 및 TestCleanup 스크립트 실행|권한 있는 컨텍스트 데이터베이스 연결을 사용해야 합니다.|  
|테스트를 실행하기 전에 데이터베이스 변경 내용 배포|권한 있는 컨텍스트 데이터베이스 연결을 사용해야 합니다. 자세한 내용은 [방법: SQL Server 단위 테스트 실행 구성](../ssdt/how-to-configure-sql-server-unit-test-execution.md)을 참조하세요.|  
|테스트를 실행하기 전에 데이터 생성|권한 있는 컨텍스트 데이터베이스 연결을 사용해야 합니다. 자세한 내용은 [방법: SQL Server 단위 테스트 실행 구성](../ssdt/how-to-configure-sql-server-unit-test-execution.md)을 참조하세요.|  
  
## <a name="DataGenerationPermissions"></a>데이터를 생성할 수 있는 권한  
데이터 생성기를 사용하여 테스트 데이터를 생성하려면 대상 데이터베이스의 개체에 대한 **INSERT** 및 **SELECT** 권한이 있어야 합니다. 데이터를 생성하기 전에 데이터를 제거하는 경우에는 대상 데이터베이스의 개체에 대한 **DELETE** 권한도 있어야 합니다. 테이블의 **IDENTITY** 열을 다시 설정하려면 테이블을 소유하고 있거나 db_owner 또는 db_ddladmin 역할의 멤버여야 합니다.  
  
## <a name="SchemaAndDataComparePermissions"></a>스키마 및 데이터를 비교할 수 있는 권한  
스키마 또는 데이터를 비교하려면 다음과 같은 사용 권한이 있어야 합니다.  
  
|||  
|-|-|  
|동작|필요한 권한|  
|두 데이터베이스의 스키마 비교|[데이터베이스를 만들거나 배포할 수 있는 권한](#DatabaseCreationAndDeploymentPermissions)에 설명된 대로 데이터베이스에서 개체 및 설정을 가져올 수 있는 권한이 있어야 합니다.|  
|데이터베이스 및 데이터베이스 프로젝트의 스키마 비교|[데이터베이스를 만들거나 배포할 수 있는 권한](#DatabaseCreationAndDeploymentPermissions)에 설명된 대로 데이터베이스에서 개체 및 설정을 가져올 수 있는 권한이 있어야 합니다. Visual Studio에서 열려 있는 데이터베이스 프로젝트가 있어야 합니다.|  
|대상 데이터베이스에 대한 업데이트 쓰기|[데이터베이스를 만들거나 배포할 수 있는 권한](#DatabaseCreationAndDeploymentPermissions)에 설명된 대로 대상 데이터베이스에 대한 업데이트를 배포할 수 있는 권한이 있어야 합니다.|  
|두 데이터베이스의 데이터 비교|두 데이터베이스의 스키마를 비교해야 하는 데 필요한 권한뿐 아니라 비교할 모든 테이블에 대한 **SELECT** 권한 및 **VIEW DATABASE STATE** 권한도 필요합니다.|  
  
자세한 내용은 SQL Server 온라인 설명서를 참조하십시오.  
  
## <a name="Transact-SQLEditorPermissions"></a>Transact\-SQL 편집기를 실행할 수 있는 권한  
Transact\-SQL 편집기 내에서 수행할 수 있는 작업은 대상 데이터베이스에 대한 실행 컨텍스트에 따라 결정됩니다.  
  
## <a name="SQLCLRPermissions"></a>SQL Server 공용 언어 런타임 프로젝트에 대한 사용 권한  
다음 표에서는 CLR 프로젝트를 배포하거나 디버깅할 때 필요한 권한을 보여 줍니다.  
  
|동작|필요한 권한|  
|-----------|------------------------|  
|Safe 권한 집합 어셈블리의 배포(초기 또는 증분)|db_DDLAdmin - 이 사용 권한은 배포하는 어셈블리 및 개체 유형에 대한 CREATE 및 ALTER 권한을 부여합니다.<br /><br />데이터베이스 수준 VIEW DEFINITION - 배포하는 데 필요합니다.<br /><br />데이터베이스 수준 CONNECT - 데이터베이스에 연결할 수 있도록 합니다.|  
|external_access 권한 집합 어셈블리 배포|db_DDLAdmin - 이 사용 권한은 배포하는 어셈블리 및 개체 유형에 대한 CREATE 및 ALTER 권한을 부여합니다.<br /><br />데이터베이스 수준 VIEW DEFINITION - 배포하는 데 필요합니다.<br /><br />데이터베이스 수준 CONNECT - 데이터베이스에 연결할 수 있도록 합니다.<br /><br />또한 다음 조건도 충족해야 합니다.<br /><br />TRUSTWORTHY 데이터베이스 옵션을 ON으로 설정해야 합니다.<br /><br />배포하는 데 사용하는 로그인에는 EXTERNAL ACCESS ASSEMBLY 서버 권한이 있어야 합니다.|  
|Unsafe 권한 집합 어셈블리 배포|db_DDLAdmin - 이 사용 권한은 배포하는 어셈블리 및 개체 유형에 대한 CREATE 및 ALTER 권한을 부여합니다.<br /><br />데이터베이스 수준 VIEW DEFINITION - 배포하는 데 필요합니다.<br /><br />데이터베이스 수준 CONNECT - 데이터베이스에 연결할 수 있도록 합니다.<br /><br />또한 다음 조건도 충족해야 합니다.<br /><br />TRUSTWORTHY 데이터베이스 옵션을 ON으로 설정해야 합니다.<br /><br />배포하는 데 사용하는 로그인에는 UNSAFE ASSEMBLY 서버 권한이 있어야 합니다.|  
|SQL CLR 어셈블리 원격 디버깅|sysadmin 고정 역할 권한이 있어야 합니다.|  
  
> [!IMPORTANT]  
> 모든 경우, 어셈블리 소유자는 어셈블리를 배포하는 데 사용할 사용자이거나 사용자가 멤버인 역할이어야 합니다. 이 요구 사항은 배포하는 어셈블리에서 참조하는 어셈블리에도 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server Data Tools](../ssdt/sql-server-data-tools.md)  
  
