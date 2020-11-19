---
title: 원격 Disable R 패키지 관리 사용 또는 사용 안 함
description: SQL Server 2016 R Services 또는 SQL Server Machine Learning Services(In-Database)에서 원격 R 패키지 관리를 사용하도록 설정
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/13/2019
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 1b3c857d5ba86fa1cb10097cf91ee5d591b67f94
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869931"
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>SQL Server용 원격 패키지 관리 사용 또는 사용 안 함
[!INCLUDE [SQL Server 2016 and 2017 only](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

이 문서에서는 클라이언트 워크스테이션 또는 다른 Machine Learning Server에서 R 패키지의 원격 관리를 사용하도록 설정하는 방법을 설명합니다. SQL Server에서 패키지 관리 기능을 사용하도록 설정한 후에는 클라이언트에서 RevoScaleR 명령을 사용하여 SQL Server에 패키지를 설치할 수 있습니다.

기본적으로 SQL Server용 외부 패키지 관리 기능은 사용하지 않도록 설정되어 있습니다. 다음 섹션에 설명된 대로 별도의 스크립트를 실행하여 이 기능을 사용하도록 설정해야 합니다.

## <a name="overview-of-process-and-tools"></a>프로세스 및 도구 개요

SQL Server에서 패키지 관리를 사용하거나 사용하지 않도록 설정하려면 **RevoScaleR** 패키지에 포함되어 있는 명령줄 유틸리티 **RegisterRExt.exe** 를 사용합니다.

이 기능을 [사용하도록 설정](#bkmk_enable)하는 프로세스는 두 단계이며 데이터베이스 관리자가 필요합니다. 즉, SQL Server 인스턴스에서 패키지 관리를 사용하도록 설정하고(SQL Server 인스턴스당 한 번) SQL 데이터베이스에서 패키지 관리를 사용하도록 설정합니다(SQL Server 데이터베이스당 한 번).

패키지 관리 기능을 [사용하지 않도록 설정](#bkmk_disable)하는 프로세스도 여러 단계가 필요합니다. 데이터베이스 수준 패키지 및 권한을 제거하고(데이터베이스당 한 번) 서버에서 역할을 제거합니다(인스턴스당 한 번).

## <a name="enable-package-management"></a><a name="bkmk_enable"></a> 패키지 관리를 사용하도록 설정

1. SQL Server에서 관리자 권한 명령 프롬프트를 열고 RegisterRExt.exe 유틸리티가 포함된 폴더로 이동합니다. 기본 위치는 `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`입니다.

2. 사용자 환경에 적절한 인수를 제공하여 다음 명령을 실행합니다.

    `RegisterRExt.exe /install pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 SQL Server 컴퓨터에서 패키지 관리에 필요한 인스턴스 수준 아티팩트를 만듭니다. 또한 인스턴스에 대한 실행 패드를 다시 시작합니다.

    인스턴스를 지정하지 않으면 기본 인스턴스가 사용됩니다. 사용자를 지정하지 않으면 현재 보안 컨텍스트가 사용됩니다. 예를 들어 다음 명령은 명령 프롬프트를 연 사용자의 자격 증명을 사용하여 기본 인스턴스에서 패키지 관리를 사용하도록 설정합니다.

    `REgisterRExt.exe /install pkgmgmt`

3. 특정 데이터베이스에 패키지 관리를 추가하려면 관리자 권한 명령 프롬프트에서 다음 명령을 실행합니다.

    `RegisterRExt.exe /install pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    이 명령은 사용자 권한을 제어하는 데 사용되는 다음과 같은 데이터베이스 역할을 비롯하여 몇 가지 데이터베이스 아티팩트를 만듭니다. `rpkgs-users`, `rpkgs-private` 및 `rpkgs-shared`.

    예를 들어 다음 명령은 기본 인스턴스에서 데이터베이스에 대한 패키지 관리를 사용하도록 설정합니다. 사용자를 지정하지 않으면 현재 보안 컨텍스트가 사용됩니다.

    `RegisterRExt.exe /install pkgmgmt /database:TestDB`

4. 패키지를 설치해야 하는 각 데이터베이스에 대해이 명령을 반복합니다.

5. 새 역할이 성공적으로 만들어졌는지 확인하려면 SQL Server Management Studio에서 데이터베이스를 클릭하고 **보안** 을 확장한 다음 **데이터베이스 역할** 을 확장합니다.

    다음과 같이 sys.database_principals에 대한 쿼리를 실행할 수도 있습니다.

    ```sql
    SELECT pr.principal_id, pr.name, pr.type_desc,   
        pr.authentication_type_desc, pe.state_desc,   
        pe.permission_name, s.name + '.' + o.name AS ObjectName  
    FROM sys.database_principals AS pr  
    JOIN sys.database_permissions AS pe  
        ON pe.grantee_principal_id = pr.principal_id  
    JOIN sys.objects AS o  
        ON pe.major_id = o.object_id  
    JOIN sys.schemas AS s  
        ON o.schema_id = s.schema_id;
    ```

이 기능을 사용하도록 설정한 후에는 RevoScaleR 함수를 사용하여 원격 R 클라이언트에서 패키지를 설치하거나 제거할 수 있습니다.

## <a name="disable-package-management"></a><a name="bkmk_disable"></a> 패키지 관리를 사용하지 않도록 설정

1. 관리자 권한 명령 프롬프트에서 RegisterRExt 유틸리티를 다시 실행하고 데이터베이스 수준에서 패키지 관리를 사용하지 않도록 설정합니다.

    `RegisterRExt.exe /uninstall pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 지정된 데이터베이스에서 패키지 관리와 관련된 데이터베이스 개체를 제거합니다. 또한 SQL Server 컴퓨터의 보안된 파일 시스템 위치에서 설치된 모든 패키지를 제거합니다.

2. 패키지 관리가 사용된 각 데이터베이스에서 이 명령을 반복합니다.

3.  (선택 사항) 이전 단계를 사용하여 모든 데이터베이스에서 패키지를 제거한 후 관리자 권한 명령 프롬프트에서 다음 명령을 실행합니다.

    `RegisterRExt.exe /uninstall pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 인스턴스에서 패키지 관리 기능을 제거합니다. 변경 내용을 확인하려면 실행 패드 서비스를 수동으로 한 번 더 다시 시작해야 할 수 있습니다.

## <a name="next-steps"></a>다음 단계

+ [RevoScaleR을 사용하여 R 패키지 설치](install-r-packages-with-revoscaler.md)
+ [R 패키지 정보 가져오기](r-package-information.md)
+ [R 패키지 사용 팁](tips-for-using-r-packages.md)
