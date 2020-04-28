---
title: 프로젝트 옵션 설정 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Project Options Setting
ms.assetid: 97b70fc8-1f68-4f15-8e22-db5b784ea4ec
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2c8d074db2fc1e8a9d29ecf5fdc0405524e9bb1a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68020925"
---
# <a name="setting-project-options-sybasetosql"></a>프로젝트 옵션 설정(SybaseToSQL)
각 SSMA 프로젝트에 대해 프로젝트 수준 옵션을 설정할 수 있습니다. 이러한 옵션은 개체 변환, 개체 로드, SQL azure, 사용자 인터페이스 및 데이터 마이그레이션 설정을 지정 합니다. 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 변환 하거나 SQL Azure 하거나 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure로 마이그레이션하려면 먼저 구성 옵션이 프로젝트에 적합 한지 확인 합니다.  
  
SSMA를 사용 하면 모든 프로젝트에 대 한 기본 옵션을 구성할 수 있습니다. 이러한 옵션은 사용자가 만드는 모든 새 프로젝트에 적용 됩니다. 그런 다음 각 프로젝트에 대 한 옵션을 사용자 지정할 수 있습니다.  
  
## <a name="configuration-options-and-modes"></a>구성 옵션 및 모드  
SSMA에는 5 개의 프로젝트 설정 집합이 있습니다.  
  
1.  프로젝트 정보  
  
2.  일반 (변환, 마이그레이션 및 데이터 수집)  
  
3.  동기화  
  
4.  GUI  
  
5.  형식 매핑  
  
또한 이러한 설정을 구성 하는 네 가지 모드가 있습니다.  
  
1.  기본값  
  
2.  Optimistic  
  
3.  전체  
  
4.  사용자 지정  
  
대부분의 사용자에 게 기본 모드를 권장 합니다. 낙관적 모드에서는 현재 Sybase ASE (적응 서버 엔터프라이즈) 구문이 더 많이 유지 되며 읽기가 더 쉽습니다. 그러나 현재 구문을 유지 하는 것은 정확 하지 않을 수 있습니다. ASE 구문을 동등한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구문이 나 SQL Azure 구문으로 변환 해야 하는 경우 전체 모드에서 전체 변환을 수행 하지만 결과 코드를 읽기가 더 어려울 수 있습니다. 사용자 지정 모드에서 옵션을 설정 합니다.  
  
설정은이 설명서의 사용자 인터페이스 참조 섹션에 설명 되어 있습니다. 설정 및 설정 설정에 대 한 자세한 내용은 다음 항목을 참조 하십시오.  
  
-   [프로젝트 설정 &#40;변환&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
-   [프로젝트 설정 &#40;마이그레이션&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)  
  
-   [프로젝트 설정 &#40;동기화&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)  
  
-   [프로젝트 설정 &#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)  
  
-   [프로젝트 설정 &#40;형식 매핑&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)  
  
-   [프로젝트 설정 &#40;Azure SQL DB &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)  
  
## <a name="setting-project-options"></a>프로젝트 옵션 설정  
SSMA에서 모든 프로젝트에 대 한 기본 설정을 구성할 수 있습니다. 이러한 설정은 SSMA 구성 파일에 저장 되 고 사용자가 만드는 모든 새 프로젝트에 적용 됩니다.  
  
**기본 프로젝트 옵션을 설정 하려면**  
  
1.  **도구** 메뉴에서 **기본 프로젝트 설정**을 선택 합니다.  
  
2.  **기본 프로젝트 설정** 대화 상자에서 다음 절차 중 하나를 사용 합니다.  
  
    -   마이그레이션 **대상 버전** 드롭다운에서 설정을 보거나 변경 해야 하는 마이그레이션 프로젝트 형식을 선택 합니다. 왼쪽 창의 맨 아래에서 일반을 클릭 한 다음 변환 또는 마이그레이션 또는 SQL Azure을 선택 합니다.  
  
    -   미리 정의 된 모드를 선택 하려면 **모드** 드롭다운 상자에서 **기본값**, **낙관적**또는 **전체**를 선택 합니다.  
  
    -   사용자 지정 설정을 지정 하려면 새 설정 또는 값을 선택 하거나 입력 하면 됩니다.  
  
3.  **확인**을 클릭하여 설정을 저장합니다.  
  
현재 프로젝트에 대 한 설정을 사용자 지정할 수도 있습니다. 이러한 설정은 현재 프로젝트 파일에 저장 됩니다.  
  
**현재 프로젝트에 대 한 설정을 사용자 지정 하려면**  
  
1.  **도구** 메뉴에서 **프로젝트 설정**을 선택 합니다.  
  
2.  **프로젝트 설정** 대화 상자에서 다음 절차 중 하나를 사용 합니다.  
  
    -   미리 정의 된 모드를 선택 하려면 **모드** 드롭다운 상자에서 **기본값**, **낙관적**또는 **전체**를 선택 합니다.  
  
    -   사용자 지정 모드를 지정 하려면 **모드** 드롭다운 상자에서 **사용자 지정**을 선택 하 고 왼쪽 창에서 옵션을 선택한 다음 오른쪽 창에서 설정 또는 값을 클릭 하 고 새 설정 또는 값을 선택 하거나 입력 합니다.  
  
3.  **확인**을 클릭하여 설정을 저장합니다.  
  
## <a name="next-steps"></a>다음 단계  
마이그레이션의 다음 단계는 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   원본 및 대상 데이터 형식의 매핑을 사용자 지정 하려면 [SYBASE ASE 및 SQL Server 데이터 형식 매핑 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)을 참조 하세요.  
  
-   그렇지 않으면 Sybase 데이터베이스 개체 정의를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체 정의로 변환할 수 있습니다. 자세한 내용은 [SYBASE ASE 데이터베이스 개체 변환 &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
[Sybase ASE 데이터베이스를 SQL Server로 마이그레이션-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
