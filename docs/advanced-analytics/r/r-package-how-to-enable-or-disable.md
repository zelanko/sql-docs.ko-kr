---
title: SQL Server Machine Learning에 대 한 원격 R 패키지 관리를 사용 하지 않도록 설정 하거나 사용 | Microsoft Docs
description: SQL Server 2016 R Services 또는 SQL Server 2017 Machine Learning Services (In-database)에서 원격 R 패키지 관리
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a38bd844e56dca4c5096156bde3b544a44038d49
ms.sourcegitcommit: fafb9b5512695b8e3fc2891f9c5e3abd7571d550
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50753514"
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>SQL Server에 대 한 원격 패키지 관리를 사용할지 설정 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 다양 한 Machine Learning Server 또는 클라이언트 워크스테이션에서 R 패키지의 원격 관리를 사용 하도록 설정 하는 방법을 설명 합니다. SQL Server에서 패키지 관리 기능을 설정한 후에 SQL Server에서 패키지를 설치 하려면 클라이언트에서 RevoScaleR 명령을 사용할 수 있습니다.

> [!NOTE]
> 현재 R 라이브러리 관리 지원 됩니다. Python은 로드맵에 대 한 지원.

기본적으로 SQL Server에 대 한 외부 패키지 관리 기능을 해제 합니다. 다음 섹션에 설명 된 대로 기능을 사용 하려면 별도 스크립트를 실행 해야 합니다.

## <a name="overview-of-process-and-tools"></a>프로세스 및 도구 개요

를 사용 하거나 SQL Server에서 패키지 관리를 사용 하지 않도록 설정 하려면 명령줄 유틸리티를 사용 하 여 **RegisterRExt.exe**에 포함 되어 있는 합니다 **RevoScaleR** 패키지 있습니다.

[사용 하도록 설정 하면](#bkmk_enable) 이 기능은 데이터베이스 관리자가 요구 하는 2 단계 프로세스를: (인스턴스당 한 번 SQL Server), SQL Server 인스턴스에서 패키지 관리를 사용 하도록 설정 하 고 다음 패키지 관리 (SQL Server 당 한 번 SQL database 사용 하도록 설정 데이터베이스)입니다.

[사용 하지 않도록 설정](#bkmk_disable) 패키지 관리 기능에는 multipel 단계가 필요 하기도: 데이터베이스 수준 패키지 및 사용 권한 (데이터베이스당 한 번)를 제거 하 고 다음 (인스턴스당 한 번) 서버에서 역할을 제거 합니다.

## <a name="bkmk_enable"></a> 패키지 관리를 사용 하도록 설정

1. SQL Server에서 관리자 권한 명령 프롬프트를 열고 유틸리티가 RegisterRExt.exe가 있는 폴더로 이동 합니다. 기본 위치는 `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`합니다.

2. 사용자 환경에 대 한 적절 한 인수를 제공 하 고 다음 명령을 실행 합니다.

    `RegisterRExt.exe /install pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 패키지 관리에 필요한 SQL Server 컴퓨터의 인스턴스 수준 개체를 만듭니다. 인스턴스에 대 한 실행 패드에도 다시 시작 됩니다.

    인스턴스를 지정 하지 않으면 기본 인스턴스가 사용 됩니다. 사용자를 지정 하지 않으면 현재 보안 컨텍스트가 사용 됩니다. 예를 들어, 다음 명령을 통해 RegisterRExt.exe 명령 프롬프트를 연 사용자의 자격 증명을 사용 하 여 경로에 인스턴스에서 패키지 관리:

    `REgisterRExt.exe /install pkgmgmt`

3. 패키지 관리에 특정 데이터베이스를 추가 하려면 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.

    `RegisterRExt.exe /install pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    이 명령은 사용자 권한을 제어에 사용 되는 다음 데이터베이스 역할을 포함 하 여 몇 가지 데이터베이스 아티팩트를 만듭니다: `rpkgs-users`, `rpkgs-private`, 및 `rpkgs-shared`합니다.

    예를 들어, 다음 명령에는 RegisterRExt 실행 되는 인스턴스에서 데이터베이스에 패키지 관리할을 수 있습니다. 사용자를 지정 하지 않으면 현재 보안 컨텍스트가 사용 됩니다.

    `RegisterRExt.exe /install pkgmgmt /database:TestDB`

4. 패키지를 설치 해야 하는 각 데이터베이스에 대해 명령을 반복 합니다.

5. 를 새 역할 성공적으로 만들어졌는지 확인 하려면 SQL Server Management Studio에서 데이터베이스를 클릭, 확장 **보안**를 확장 하 고 **데이터베이스 역할**입니다.

    또한 다음과 같은 sys.database_principals에 쿼리를 실행할 수 있습니다.

    ```SQL
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

이 기능을 사용 하도록 설정한 후에 설치 또는 원격 R 클라이언트에서 패키지를 제거 하려면 RevoScaleR 함수를 사용할 수 있습니다.

## <a name="bkmk_disable"></a> 패키지 관리를 사용 하지 않도록 설정

1. 관리자 권한 명령 프롬프트에서 RegisterRExt 유틸리티를 다시 실행 하 고 데이터베이스 수준에서 패키지 관리를 사용 하지 않도록 설정 합니다.

    `RegisterRExt.exe /uninstall pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 지정된 된 데이터베이스에서 패키지 관리와 관련 된 데이터베이스 개체를 제거 합니다. 또한 SQL Server 컴퓨터의 보안된 파일 시스템 위치에서 설치 된 모든 패키지를 제거 합니다.

2. 패키지 관리를 사용 하는 각 데이터베이스에서이 명령을 반복 합니다.

3.  (선택 사항) 이전 단계를 사용 하 여 패키지의 모든 데이터베이스를 해결 한 후 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.

    `RegisterRExt.exe /uninstall pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 인스턴스에서 패키지 관리 기능을 제거합니다. 수동으로 변경 내용을 확인 하려면 한 번 더 실행 패드 서비스를 다시 시작 해야 합니다.

## <a name="next-steps"></a>다음 단계

+ [RevoScaleR을 사용 하 여 새로운 R 패키지 설치](use-revoscaler-to-manage-r-packages.md)
+ [R 패키지를 설치 하기 위한 팁](packages-installed-in-user-libraries.md)
+ [기본 패키지](installing-and-managing-r-packages.md)
