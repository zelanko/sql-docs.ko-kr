---
title: SQL Server에 대 한 원격 패키지 관리를 사용할지 | Microsoft Docs
ms.custom: ''
ms.date: 02/20/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 5b0039736102af09fe12e296c85cd57a83509a6b
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>SQL Server에 대 한 원격 패키지 관리를 사용할지 설정 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 관리 서버를 학습 하는 컴퓨터의 원격 인스턴스에서 R 패키지를 설정 하는 방법을 설명 합니다. 패키지 관리 기능에 설정한 후 원격 클라이언트에서 데이터베이스에 패키지를 설치 하려면 RevoScaleR 명령을 사용할 수 있습니다.

> [!NOTE]
> 현재에 R 라이브러리의 관리가 지원 됩니다. Python은 로드맵을 지원 합니다.

기본적으로 SQL Server에 대 한 외부 패키지 관리 기능 불가능, 컴퓨터 학습 기능이 설치 된 경우에 합니다. 다음 섹션에 설명 된 대로 기능을 사용 하려면 별도 스크립트를 실행 해야 합니다.

## <a name="overview-of-process-and-tools"></a>프로세스 및 도구 개요

를 사용 하거나 패키지 관리를 사용 하지 않도록 설정 하려면 명령줄 유틸리티를 사용 하 여 **RegisterRExt.exe**에 포함 되어 있는 **RevoScaleR** 패키지 합니다.

[사용 하도록 설정](#bkmk_enable) 이 기능은 데이터베이스 관리자는 한 단계로: SQL Server 인스턴스 (SQL Server 인스턴스) 당 한 번에 패키지 관리를 사용 하도록 설정 하 고 다음 SQL 데이터베이스 (SQL Server 당 한 번에 패키지 관리를 사용 하도록 설정 데이터베이스)입니다.

[사용 하지 않도록 설정](#bkmk_disable) 에서도 패키지 관리 기능에 필요 multipel 단계: 데이터베이스 수준 패키지 및 사용 권한 (데이터베이스) 당 한 번 제거 하 고 다음 (인스턴스마다 한 번씩) 서버에서 역할을 제거 합니다.

## <a name="bkmk_enable"></a> 패키지 관리를 사용 하도록 설정

1. 관리자 권한 명령 프롬프트를 열고 RegisterRExt.exe 유틸리티 포함 된 폴더로 이동 합니다. 기본 위치는 `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`합니다.

2. 사용자 환경에 적절 한 인수를 제공 하 고 다음 명령을 실행 합니다.

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 패키지 관리에 필요한 SQL Server 컴퓨터에서 인스턴스 수준 개체를 만듭니다. 또한 실행 패드 인스턴스에 대 한 다시 시작합니다.

    인스턴스를 지정 하지 않으면 기본 인스턴스가 사용 됩니다. 사용자 지정 하지 않으면 현재 보안 컨텍스트가 사용 됩니다. 예를 들어 다음 명령은 RegisterRExt.exe 명령 프롬프트를 연 사용자의 자격 증명을 사용 하 여 경로 있는 인스턴스의 패키지 관리를 사용 하면:

    `REgisterRExt.exe /installpkgmgmt`

3. 패키지 관리에 특정 데이터베이스를 추가 하려면 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    이 명령은 사용자 사용 권한을 제어에 사용 되는 다음 데이터베이스 역할을 포함 하 여 일부 데이터베이스 아티팩트를 만듭니다: `rpkgs-users`, `rpkgs-private`, 및 `rpkgs-shared`합니다.

    예를 들어 다음 명령은 RegisterRExt 실행 되는 위치 인스턴스에서 데이터베이스에 패키지 관리를 활성화 합니다. 사용자 지정 하지 않으면 현재 보안 컨텍스트가 사용 됩니다.

    `RegisterRExt.exe /installpkgmgmt /database:TestDB`

4. 패키지를 설치 해야 하는 각 데이터베이스에 대 한 명령을 반복 합니다.

5. 를 새 역할 성공적으로 만들어졌는지 확인 하려면 SQL Server Management Studio에서 데이터베이스를 클릭를 확장 하 고 **보안**, 확장 및 **데이터베이스 역할**합니다.

    다음과 같은 sys.database_principals에서 쿼리를 실행할 수도 있습니다.

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

이 기능을 사용 하도록 설정한 후 설치 하거나 원격 R 클라이언트에서 패키지를 제거 하려면 RevoScaleR 함수를 사용할 수 있습니다.

## <a name="bkmk_disable"></a> 패키지 관리를 사용 하지 않도록 설정

1. 상승된 된 명령 프롬프트에서 RegisterRExt 유틸리티를 다시 실행 하 고 데이터베이스 수준에서 패키지 관리를 사용 하지 않도록 설정 합니다.

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 지정된 된 데이터베이스에서 패키지 관리와 관련 된 데이터베이스 개체를 제거 합니다. 또한 SQL Server 컴퓨터에서 보안된 파일 시스템 위치에서 설치 된 모든 패키지를 제거 합니다.

2. 패키지 관리를 사용 하는 각 데이터베이스에서이 명령을 반복 합니다.

3.  (선택 사항) 이전 단계를 사용 하 여 패키지의 모든 데이터베이스를 해결 한 후 상승된 된 명령 프롬프트에서 다음 명령을 실행 합니다.

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 인스턴스에서 패키지 관리 기능을 제거 합니다. 변경 내용을 확인할 수는 한 번 더 실행 패드 서비스를 수동으로 다시 시작 해야 합니다.

