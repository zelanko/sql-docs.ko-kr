---
title: "R 패키지 관리를 사용하거나 사용하지 않도록 설정하는 방법 | Microsoft Docs"
ms.custom: ""
ms.date: "12/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: 7
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# R 패키지 관리를 사용하거나 사용하지 않도록 설정하는 방법

기본적으로 패키지 관리는 R Services가 설치되어 있는 경우에도 SQL Server 인스턴스에서 사용되지 않습니다. 이 기능을 사용하도록 설정하려면 데이터베이스 관리자가 다음 2단계 프로세스를 수행해야 합니다. 

1. SQL Server 인스턴스에서 패키지 관리를 사용하도록 설정(SQL Server 인스턴스당 한 번) 
2. SQL 데이터베이스에서 패키지 관리를 사용하도록 설정(SQL Server 데이터베이스당 한 번) 


패키지 관리 기능을 사용하지 않도록 설정하려면 프로세스를 반대로 수행하여 데이터베이스 수준 패키지 및 권한을 제거한 다음 서버에서 역할을 제거합니다.
 
1. 각 데이터베이스에서 패키지 관리를 사용하지 않도록 설정(데이터베이스당 한 번) 
2. SQL Server 인스턴스에서 패키지 관리를 사용하지 않도록 설정(인스턴스당 한 번) 

> [!IMPORTANT]
> 이 기능은 개발 중입니다. 이후 릴리스에서는 구문이나 기능이 변경될 수 있습니다. 

### <a name="to-enable-package-management"></a>패키지 관리를 사용하도록 설정하려면

패키지 관리를 사용하거나 사용하지 않도록 설정하려면 명령줄 유틸리티 **RegisterRExt.exe**가 필요하며, 이 유틸리티는 SQL Server R Services와 함께 설치되는 **RevoScaleR** 패키지에 포함되어 있습니다. 기본 위치는 다음과 같습니다.

`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe` 
    
1. 관리자 권한 명령 프롬프트를 열고 다음 명령을 사용합니다.

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 패키지 관리에 필요한 SQL Server 컴퓨터에 인스턴스 수준 아티팩트를 만듭니다. 

2. 데이터베이스 수준에서 패키지 관리를 추가하려면 패키지를 설치해야 하는 각 데이터베이스에 대해 관리자 권한 명령 프롬프트에서 다음 명령을 실행합니다. 

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]` 

    이 명령은 사용자 권한을 제어하는 데 필요한 **rpkgs-users**, **rpkgs-private** 및 **rpkgs-shared** 같은 데이터베이스 역할을 포함하여 몇 가지 데이터베이스 아티팩트를 만듭니다. 

### <a name="to-disable-package-management"></a>패키지 관리를 사용하지 않도록 설정하려면 

1. 데이터베이스 수준에서 패키지 관리를 사용하지 않도록 설정하려면 관리자 권한 명령 프롬프트에서 다음 명령을 실행합니다.

   `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]` 

    이 명령은 지정된 데이터베이스에서 패키지 관리와 관련된 데이터베이스 아티팩트를 제거합니다.  또한 이 명령은 SQL Server 컴퓨터의 보안된 파일 시스템 위치에서 데이터베이스별로 설치된 모든 패키지를 제거합니다.
    
    이 명령은 패키지 관리가 사용된 각 데이터베이스에 대해 한 번 실행해야 합니다.
 
2. (선택 사항) 인스턴스에서 패키지 관리 기능을 완전히 제거하려면 이전 단계를 사용하여 모든 데이터베이스에서 패키지를 지운 후 관리자 권한 명령 프롬프트에서 다음 명령을 실행합니다.

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    이 명령은 패키지 관리에 사용되는 인스턴스 수준 아티팩트를 SQL Server 인스턴스에서 제거합니다. 


## <a name="see-also"></a>관련 항목:
[SQL Server R Services에 대한 R 패키지 관리](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)