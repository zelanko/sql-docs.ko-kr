---
title: 원격 R 패키지 관리를 사용 하거나 사용 하지 않도록 설정
description: SQL Server 2016 R Services 또는 SQL Server 2017 Machine Learning Services (데이터베이스 내)에서 원격 R 패키지 관리를 사용 하도록 설정
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 9cc08b1227751559ea509838fe8fc3a446296770
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470029"
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>SQL Server에 대 한 원격 패키지 관리를 사용 하거나 사용 하지 않도록 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 클라이언트 워크스테이션 또는 다른 Machine Learning Server에서 R 패키지의 원격 관리를 사용 하도록 설정 하는 방법을 설명 합니다. SQL Server에서 패키지 관리 기능을 사용 하도록 설정한 후에는 클라이언트에서 RevoScaleR 명령을 사용 하 여 SQL Server에 패키지를 설치할 수 있습니다.

> [!NOTE]
> 현재 R 라이브러리 관리가 지원 됩니다. Python에 대 한 지원은 로드맵에 있습니다.

기본적으로 SQL Server의 외부 패키지 관리 기능은 사용할 수 없습니다. 다음 섹션에 설명 된 대로 기능을 사용 하도록 설정 하려면 별도의 스크립트를 실행 해야 합니다.

## <a name="overview-of-process-and-tools"></a>프로세스 및 도구 개요

SQL Server에서 패키지 관리를 사용 하거나 사용 하지 않도록 설정 하려면 **RevoScaleR** 패키지에 포함 된 명령줄 유틸리티 **registerrext .exe**를 사용 합니다.

이 기능을 [사용 하도록 설정](#bkmk_enable) 하는 과정은 두 단계로 구성 됩니다. 데이터베이스 관리자가 필요 합니다. (SQL Server 인스턴스당 한 번씩) SQL Server 인스턴스에서 패키지 관리를 사용 하도록 설정한 다음 SQL 데이터베이스에서 패키지 관리를 사용 하도록 설정 합니다 (SQL Server 데이터베이스당 한 번). ).

패키지 관리 기능을 [사용 하지 않도록 설정](#bkmk_disable) 하려면 multipel 단계가 필요 합니다. 데이터베이스 수준 패키지 및 사용 권한을 제거한 다음 (데이터베이스당 한 번) 서버에서 역할을 제거 합니다 (인스턴스당 한 번).

## <a name="bkmk_enable"></a>패키지 관리 사용

1. SQL Server에서 관리자 권한 명령 프롬프트를 열고 RegisterRExt .exe 유틸리티가 포함 된 폴더로 이동 합니다. 기본 위치 `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`는입니다.

2. 사용자 환경에 적절 한 인수를 제공 하 여 다음 명령을 실행 합니다.

    `RegisterRExt.exe /install pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 SQL Server 컴퓨터에서 패키지를 관리 하는 데 필요한 인스턴스 수준 개체를 만듭니다. 또한 인스턴스에 대 한 실행 패드를 다시 시작 합니다.

    인스턴스를 지정 하지 않으면 기본 인스턴스가 사용 됩니다. 사용자를 지정 하지 않으면 현재 보안 컨텍스트가 사용 됩니다. 예를 들어 다음 명령은 명령 프롬프트를 연 사용자의 자격 증명을 사용 하 여 RegisterRExt의 경로에서 인스턴스에 대 한 패키지 관리를 사용 하도록 설정 합니다.

    `REgisterRExt.exe /install pkgmgmt`

3. 특정 데이터베이스에 패키지 관리를 추가 하려면 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.

    `RegisterRExt.exe /install pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    이 명령은 사용자 권한을 `rpkgs-users` `rpkgs-private`제어 하는 데 사용 되는 데이터베이스 역할, 및 `rpkgs-shared`를 비롯 한 일부 데이터베이스 아티팩트를 만듭니다.

    예를 들어 다음 명령은 RegisterRExt가 실행 되는 인스턴스에서 데이터베이스에 대 한 패키지 관리를 사용 하도록 설정 합니다. 사용자를 지정 하지 않으면 현재 보안 컨텍스트가 사용 됩니다.

    `RegisterRExt.exe /install pkgmgmt /database:TestDB`

4. 패키지를 설치 해야 하는 각 데이터베이스에 대해이 명령을 반복 합니다.

5. 새 역할이 성공적으로 만들어졌는지 확인 하려면 SQL Server Management Studio에서 데이터베이스를 클릭 하 고 **보안**을 확장 한 다음 **데이터베이스 역할**을 확장 합니다.

    Database_principals에서 다음과 같은 쿼리를 실행할 수도 있습니다.

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

이 기능을 사용 하도록 설정한 후에는 RevoScaleR 함수를 사용 하 여 원격 R 클라이언트에서 패키지를 설치 하거나 제거할 수 있습니다.

## <a name="bkmk_disable"></a>패키지 관리 사용 안 함

1. 관리자 권한 명령 프롬프트에서 RegisterRExt 유틸리티를 다시 실행 하 고 데이터베이스 수준에서 패키지 관리를 사용 하지 않도록 설정 합니다.

    `RegisterRExt.exe /uninstall pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 지정 된 데이터베이스에서 패키지 관리와 관련 된 데이터베이스 개체를 제거 합니다. 또한 SQL Server 컴퓨터의 보안 파일 시스템 위치에서 설치 된 모든 패키지를 제거 합니다.

2. 패키지 관리가 사용 된 각 데이터베이스에 대해이 명령을 반복 합니다.

3.  필드 이전 단계를 사용 하 여 모든 데이터베이스의 패키지를 지운 후 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.

    `RegisterRExt.exe /uninstall pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 인스턴스에서 패키지 관리 기능을 제거 합니다. 변경 내용을 확인 하려면 실행 패드 서비스를 추가 하 여 수동으로 다시 시작 해야 할 수도 있습니다.

## <a name="next-steps"></a>다음 단계

+ [RevoScaleR를 사용 하 여 새 R 패키지 설치](use-revoscaler-to-manage-r-packages.md)
+ [R 패키지를 설치 하기 위한 팁](packages-installed-in-user-libraries.md)
+ [기본 패키지](../package-management/default-packages.md)
