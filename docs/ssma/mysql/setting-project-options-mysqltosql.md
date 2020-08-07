---
title: 프로젝트 옵션 설정 (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: d5c85c551ba70d28b4af7eb87126c51ef5a4ff75
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87863524"
---
# <a name="setting-project-options-mysqltosql"></a>프로젝트 옵션 설정(MySQLToSQL)
각 SSMA 프로젝트에 대해 프로젝트 수준 옵션을 설정할 수 있습니다. 이러한 옵션은 개체가 변환 되는 방법, 데이터를 마이그레이션하는 방법 및 원본 데이터 형식을 대상 데이터 형식에 매핑하는 방법을 지정 합니다.  개체를 SQL Server 또는 SQL Azure 데이터를 SQL Server 또는 SQL Azure로 변환 하기 전에 구성 옵션이 프로젝트에 적합 한지 확인 합니다.  
  
SSMA를 사용 하면 모든 프로젝트에 대 한 기본 옵션을 구성할 수 있습니다. 이러한 옵션은 사용자가 만드는 모든 새 프로젝트에 적용 됩니다. 그런 다음 각 프로젝트에 대 한 옵션을 사용자 지정할 수 있습니다.  
  
## <a name="configuration-options-and-modes"></a>구성 옵션 및 모드  
SSMA에는 5 개의 프로젝트 설정 집합이 있습니다.  
  
-   프로젝트 정보  
  
-   일반 (변환, 마이그레이션 및 SQL Azure)  
  
-   동기화  
  
-   GUI  
  
-   형식 매핑  
  
프로젝트 설정은 다음 네 가지 방법으로 구성할 수 있습니다.  
  
-   기본값  
  
-   Optimistic  
  
-   전체  
  
-   사용자 지정  
  
대부분의 사용자에 게 기본 모드를 권장 합니다. 낙관적 모드는 현재 MySQL 구문을 더 많이 유지 하 고 더 쉽게 읽을 수 있습니다. 그러나 현재 구문을 유지 하는 것은 정확 하지 않을 수 있습니다. MySQL 구문을 동등한 SQL Server 또는 SQL Azure 구문으로 변환 해야 하는 경우 전체 모드에서 가장 완전 한 변환을 수행 합니다. 그러나 결과 코드를 읽기가 더 어려울 수 있습니다. 사용자 지정 모드에서 옵션을 설정할 수 있습니다.  
  
설정 및 설정 설정에 대 한 자세한 내용은 다음 항목을 참조 하십시오.  
  
-   [프로젝트 설정 &#40;MySQLToSQL&#41;&#41; &#40;변환](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [프로젝트 설정 &#40;마이그레이션&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [프로젝트 설정 (GUI) (SSMA Common)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [프로젝트 설정 &#40;형식 매핑&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [프로젝트 설정 &#40;동기화&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [프로젝트 설정 &#40;Azure SQL Database&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>프로젝트 옵션 설정  
SSMA에서 모든 프로젝트에 대 한 기본 설정을 구성할 수 있습니다. 이러한 설정은 SSMA 구성 파일에 저장 되 고 사용자가 만드는 모든 새 프로젝트에 적용 됩니다.  
  
**기본 프로젝트 옵션을 설정 하려면**  
  
1.  **도구** 메뉴에서 **기본 프로젝트 설정**을 클릭 합니다.  
  
2.  **기본 프로젝트 설정** 대화 상자에서 다음 절차 중 하나를 사용 합니다.  
  
    1.  마이그레이션 **대상 버전** 드롭다운에서 설정 하거나 변경 해야 하는 설정에 대 한 마이그레이션 프로젝트 유형을 선택 하 고 왼쪽 창의 맨 아래에서 **일반** 을 클릭 한 다음 **변환 또는 마이그레이션 또는 SQL Azure** 옵션을 선택 합니다.  
  
    2.  미리 정의 된 모드를 선택 하려면 **모드** 드롭다운 상자에서 **기본**, **낙관적**또는 **전체** 를 선택 합니다.  
  
    3.  사용자 지정 설정을 지정 하려면 새 설정 또는 값을 선택 하거나 입력 합니다.  
  
3.  **확인**을 클릭하여 설정을 저장합니다.  
  
현재 프로젝트에 대 한 설정을 사용자 지정할 수도 있습니다. 설정은 현재 프로젝트 파일에 저장 됩니다.  
  
**현재 프로젝트에 대 한 설정을 사용자 지정 하려면**  
  
1.  **도구** 메뉴에서 **projectsettings**를 클릭 합니다.  
  
2.  **Projectsettings** 대화 상자에서 다음 절차 중 하나를 사용 합니다.  
  
    1.  미리 정의 된 모드를 선택 하려면 **모드** 드롭다운 상자에서 **기본**, **낙관적**또는 **전체** 를 선택 합니다.  
  
    2.  사용자 지정 모드를 지정 하려면 **모드** 드롭다운 상자에서 **사용자 지정** 을 선택 합니다. 그런 다음 적절 한 프로젝트 설정을 선택 합니다.  
  
3.  **확인**을 클릭하여 설정을 저장합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션의 다음 단계는 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   원본 및 대상 데이터 형식의 매핑을 사용자 지정 하려면 [MySQL 및 SQL Server 데이터 형식 &#40;MySQLToSQL에 매핑](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md) 을 참조 하세요&#41;  
  
-   그렇지 않으면 MySQL 데이터베이스 개체 정의를 SQL Server 또는 SQL Azure 개체 정의로 변환할 수 있습니다. 자세한 내용은 [&#40;MySQLToSQL&#41;MySQL 데이터베이스 변환](../../ssma/mysql/converting-mysql-databases-mysqltosql.md) (영문)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
[MySQL 및 SQL Server 데이터 형식 &#40;MySQLToSQL&#41;매핑](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
