---
title: "SQL Server에 대 한 R 패키지 관리를 사용할지 | Microsoft Docs"
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 35bcae1e29e9b640d2e04b9adc788e382b18b6e8
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="enable-or-disable-r-package-management-for-sql-server"></a>SQL Server에 대 한 R 패키지 관리를 사용할지 설정 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 데이터베이스 관리자가 오른쪽 것이 아니라 T-SQL을 사용 하 여 인스턴스에서 패키지 설치를 제어할 수 있도록 설계 되었습니다. SQL Server 2017 년의 새로운 패키지 관리 기능 설명

에서는 패키지 관리 frature 사용 하도록 설정, 데이터베이스 제거 원격 클라이언트에 패키지를 설치 하려면 R 명령을도 사용할 수 있습니다.

> [!NOTE]
> 기본적으로 SQL Server에 대 한 외부 패키지 관리 기능 불가능, 컴퓨터 학습 기능이 설치 된 경우에 합니다. 

## <a name="enable-package-management"></a>패키지 관리를 사용 하도록 설정

[사용](#bkmk_enable) 이 기능은 데이터베이스 관리자는 2 단계 프로세스:

1.  SQL Server 인스턴스에서 패키지 관리를 사용하도록 설정(SQL Server 인스턴스당 한 번)

2.  SQL 데이터베이스에서 패키지 관리를 사용하도록 설정(SQL Server 데이터베이스당 한 번)

[사용 하지 않도록 설정](#bkmk_disable) 패키지 관리 기능을 데이터베이스 수준 패키지 및 사용 권한을 제거 하는 프로세스를 반대로 한 다음 서버에서 역할을 제거 합니다.

1.  각 데이터베이스에서 패키지 관리를 사용하지 않도록 설정(데이터베이스당 한 번)

2.  SQL Server 인스턴스에서 패키지 관리를 사용하지 않도록 설정(인스턴스당 한 번)

## <a name="bkmk_enable"></a>패키지 관리를 사용 하도록 설정

를 사용 하거나 패키지 관리를 사용 하지 않도록 설정 하려면 명령줄 유틸리티를 사용 하 여 **RegisterRExt.exe**에 포함 되어 있는 **RevoScaleR** 패키지 합니다.

1. 관리자 권한 명령 프롬프트를 열고 RegisterRExt.exe 유틸리티 포함 된 폴더로 이동 합니다. 기본 위치는 `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`합니다.

2. 사용자 환경에 적절 한 인수를 제공 하 고 다음 명령을 실행 합니다.

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 패키지 관리에 필요한 SQL Server 컴퓨터에서 인스턴스 수준 개체를 만듭니다. 또한 실행 패드 인스턴스에 대 한 다시 시작합니다.

    인스턴스를 지정 하지 않으면 기본 인스턴스가 사용 됩니다. 사용자 지정 하지 않으면 현재 보안 컨텍스트가 사용 됩니다. 예를 들어 다음 명령은 RegisterRExt.exe 명령 프롬프트를 연 사용자의 자격 증명을 사용 하 여 경로 있는 인스턴스의 패키지 관리를 사용 하면:

    `REgisterRExt.exe /installpkgmgmt`

2.  패키지 관리에 특정 데이터베이스를 추가 하려면 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    이 명령은 사용자 사용 권한을 제어에 사용 되는 다음 데이터베이스 역할을 포함 하 여 일부 데이터베이스 아티팩트를 만듭니다: `rpkgs-users`, `rpkgs-private`, 및 `rpkgs-shared`합니다.

    예를 들어 다음 명령은 RegisterRExt 실행 되는 위치 인스턴스에서 데이터베이스에 패키지 관리를 활성화 합니다. 사용자 지정 하지 않으면 현재 보안 컨텍스트가 사용 됩니다. 

    `RegisterRExt.exe /installpkgmgmt /database:TestDB`

3. 패키지를 설치 해야 하는 각 데이터베이스에 대 한 명령을 반복 합니다.

4.  를 새 역할 성공적으로 만들어졌는지 확인 하려면 SQL Server Management Studio에서 데이터베이스를 클릭를 확장 하 고 **보안**, 확장 및 **데이터베이스 역할**합니다.

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

4.  해당 기능을 사용 하는 후 서버에 연결 하 고 설치 또는 패키지 R 명령을 사용 하 여 원격으로 동기화 합니다. 이 과정의 예제를 보려면 [추가 패키지를 SQL Server에 설치](install-additional-r-packages-on-sql-server.md)합니다.

## <a name="bkmk_disable"></a>패키지 관리를 사용 하지 않도록 설정

1.  상승된 된 명령 프롬프트에서 RegisterRExt 유틸리티를 다시 실행 하 고 데이터베이스 수준에서 패키지 관리를 사용 하지 않도록 설정 합니다.

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 지정된 된 데이터베이스에서 패키지 관리와 관련 된 데이터베이스 개체를 제거 합니다. 또한 SQL Server 컴퓨터에서 보안된 파일 시스템 위치에서 설치 된 모든 패키지를 제거 합니다.

2. 패키지 관리를 사용 하는 각 데이터베이스에 대해 한 번만이 명령을 실행 합니다. 

3.  (선택 사항) 이전 단계를 사용 하 여 패키지의 모든 데이터베이스를 해결 한 후 상승된 된 명령 프롬프트에서 다음 명령을 실행 합니다.

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 인스턴스에서 패키지 관리 기능을 제거 합니다. 변경 내용을 확인할 수는 한 번 더 실행 패드 서비스를 수동으로 다시 시작 해야 합니다.

## <a name="see-also"></a>참고 항목

[SQL Server에 대한 R 패키지 관리](r-package-management-for-sql-server-r-services.md)
