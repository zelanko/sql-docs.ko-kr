---
title: 프로젝트 옵션 (MySQLToSQL) 설정 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
caps.latest.revision: 12
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0a39cb38cc8439ccb5eac559445b7836982b41ff
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="setting-project-options-mysqltosql"></a>프로젝트 옵션 설정 (MySQLToSQL)
각 SSMA 프로젝트에 대해 프로젝트 수준의 옵션을 설정할 수 있습니다. 이러한 옵션에는 개체를 변환 하는 방법을, 데이터가 마이그레이션되는 방식 및 원본 데이터 형식이 대상 데이터 형식으로 매핑되는 방법을 지정 합니다.  SQL Server 또는 SQL Azure에 개체를 변환 하거나 SQL Server 또는 SQL Azure로 데이터를 마이그레이션하려면 하기 전에 구성 옵션은 프로젝트에 적절 한지 확인 합니다.  
  
SSMA를 사용 하면 모든 프로젝트에 대 한 기본 옵션을 구성할 수 있습니다. 이러한 옵션은 만들어지는 모든 새 프로젝트에 적용 됩니다. 그런 다음 각 프로젝트에 대 한 옵션을 사용자 지정할 수 있습니다.  
  
## <a name="configuration-options-and-modes"></a>구성 옵션 및 모드  
SSMA는 프로젝트 설정의 5 개 세트:  
  
-   프로젝트 정보  
  
-   일반 (변환, 마이그레이션 및 SQL Azure)  
  
-   Synchronization  
  
-   GUI  
  
-   형식 매핑  
  
프로젝트 설정 네 가지 방법으로 구성할 수 있습니다.  
  
-   기본값  
  
-   Optimistic  
  
-   전체  
  
-   사용자 지정  
  
대부분의 사용자에 대 한 기본 모드를 사용 하는 것이 좋습니다. 최적 모드 중 현재 MySQL 구문을 유지 되며 더 쉽게 읽을 수 있습니다. 그러나 현재 구문을 유지 하지 정확할 수도 있습니다. MySQL 구문 해당 SQL Server 또는 SQL Azure 구문으로 변환 해야, 하는 경우 전체 모드에서 가장 완벽 변환을 수행 합니다. 그러나 결과 코드를 수 있습니다 읽기가 더 어려워집니다. 사용자 지정 모드 옵션을 설정할 수 있습니다.  
  
설정과 각 모드에서 설정이 적용 되는 방식을 대 한 자세한 내용은 다음 항목을 참조 합니다.  
  
-   [프로젝트 설정 &#40;변환&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [프로젝트 설정 &#40;마이그레이션&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [프로젝트 설정 (GUI) (SSMA 공통)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [프로젝트 설정 &#40;형식 매핑&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [프로젝트 설정 &#40;동기화&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [프로젝트 설정 &#40;Azure SQL DB&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>프로젝트 옵션 설정  
SSMA를 모든 프로젝트에 대 한 기본 설정을 구성할 수 있습니다. 이러한 설정은 SSMA 구성 파일에 저장 되며 만드는 모든 새 프로젝트에 적용 됩니다.  
  
**기본 프로젝트 옵션을 설정 하려면**  
  
1.  에 **도구** 메뉴를 클릭 하 여 **기본 프로젝트 설정**합니다.  
  
2.  에 **기본 프로젝트 설정** 대화 상자에서 다음 절차 중 하나를 사용 합니다.  
  
    1.  설정을 볼 /에서 변경 하는 데 필요한는 마이그레이션 프로젝트 형식을 선택 **마이그레이션 대상 버전** 드롭다운을 클릭 **일반** 선택 고 왼쪽된 창 맨 아래에 **변환 하거나 마이그레이션 또는 SQL Azure** 옵션입니다.  
  
    2.  미리 정의 된 모드를 선택 하려면 선택 **기본**, **Optimistic**, 또는 **전체** 에서 **모드** 드롭다운 상자입니다.  
  
    3.  사용자 지정 설정을 지정 하려면에서 선택 하거나 새 설정이 나 값을 입력 합니다.  
  
3.  클릭 **확인** 설정을 저장할 수 있습니다.  
  
또한 현재 프로젝트에 대 한 설정을 사용자 지정할 수 있습니다. 설정은 현재 프로젝트 파일에 저장 됩니다.  
  
**현재 프로젝트에 대 한 설정을 사용자 지정 하려면**  
  
1.  에 **도구** 메뉴를 클릭 하 여 **ProjectSettings**합니다.  
  
2.  에 **ProjectSettings** 대화 상자에서 다음 절차 중 하나를 사용 합니다.  
  
    1.  미리 정의 된 모드를 선택 하려면 선택 **기본**, **Optimistic**, 또는 **전체** 에서 **모드** 드롭다운 상자입니다.  
  
    2.  사용자 지정 모드를 지정 하려면 **사용자 지정** 에서 **모드** 드롭다운 상자입니다. 선택한 후 적절 한 프로젝트 설정 합니다.  
  
3.  클릭 **확인** 설정을 저장할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
다음 단계는 마이그레이션에서 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   원본 및 대상 데이터 형식 매핑, 사용자 지정 하려면 참조 [매핑 MySQL 및 SQL Server 데이터 형식 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   그렇지 않으면 SQL Server 또는 SQL Azure 개체 정의에 MySQL 데이터베이스 개체 정의 변환할 수 있습니다. 자세한 내용은 참조 [MySQL 데이터베이스 변환 &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>관련 항목:  
[MySQL 및 SQL Server 데이터 형식 매핑 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
