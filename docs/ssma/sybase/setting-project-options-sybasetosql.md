---
title: 프로젝트 옵션 (SybaseToSQL) 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Project Options Setting
ms.assetid: 97b70fc8-1f68-4f15-8e22-db5b784ea4ec
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7c7053d6a7acad85fe2094cca1bf8568a1a2f94a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="setting-project-options-sybasetosql"></a>프로젝트 옵션 설정 (SybaseToSQL)
각 SSMA 프로젝트에 대 한 프로젝트 수준 옵션을 설정할 수 있습니다. 이러한 옵션에는 변환 개체, 개체 로드, SQL azure, 사용자 인터페이스 및 데이터 마이그레이션 설정을 지정합니다. 개체를 변환 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure에 데이터를 마이그레이션하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure, 구성 옵션은 프로젝트에 대 한 적절 한지 확인 하십시오.  
  
SSMA를 사용 하면 모든 프로젝트에 대 한 기본 옵션을 구성할 수 있습니다. 이러한 옵션은 만들 새 프로젝트에 적용 됩니다. 그런 다음 각 프로젝트에 대 한 옵션을 사용자 지정할 수 있습니다.  
  
## <a name="configuration-options-and-modes"></a>구성 옵션 및 모드  
SSMA는 프로젝트 설정의 5 개 세트:  
  
1.  프로젝트 정보  
  
2.  일반 (변환, 마이그레이션 및 데이터 수집)  
  
3.  Synchronization  
  
4.  GUI  
  
5.  형식 매핑  
  
구성이 설정에 대 한 네 가지 모드에 있습니다.  
  
1.  기본값  
  
2.  Optimistic  
  
3.  전체  
  
4.  사용자 지정  
  
대부분의 사용자에 대 한 기본 모드를 사용 하는 것이 좋습니다. 최적 모드 중 현재 Sybase 적응형 Server Enterprise (ASE) 구문을 유지 되며 더 쉽게 읽을 수 있습니다. 그러나 현재 구문을 유지 하지 정확할 수도 있습니다. ASE 구문으로 변환 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 구문, 전체 모드 전체 변환을 수행 하지만 결과 코드를 읽기가 어려울 수 있습니다. 사용자 지정 모드에서 옵션을 설정 합니다.  
  
설정은이 설명서의 사용자 인터페이스 참조 섹션에 설명 되어 있습니다. 설정과 각 모드에서 설정이 적용 되는 방식을 대 한 자세한 내용은 다음 항목을 참조 합니다.  
  
-   [프로젝트 설정 &#40;변환&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
-   [프로젝트 설정 &#40;마이그레이션&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)  
  
-   [프로젝트 설정 &#40;동기화&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)  
  
-   [프로젝트 설정 &#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)  
  
-   [프로젝트 설정 &#40;형식 매핑&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)  
  
-   [프로젝트 설정 &#40;Azure SQL DB &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)  
  
## <a name="setting-project-options"></a>프로젝트 옵션 설정  
SSMA를 모든 프로젝트에 대 한 기본 설정을 구성할 수 있습니다. 이러한 설정은 SSMA 구성 파일에 저장 되며 만드는 모든 새 프로젝트에 적용 됩니다.  
  
**기본 프로젝트 옵션을 설정 하려면**  
  
1.  에 **도구** 메뉴 선택 **기본 프로젝트 설정**합니다.  
  
2.  에 **기본 프로젝트 설정** 대화 상자에서 다음 절차 중 하나를 사용 합니다.  
  
    -   설정을 보거나에서 변경 하는 데 필요한는 마이그레이션 프로젝트 형식을 선택 **마이그레이션 대상 버전** drop 아래로 왼쪽 창의 맨 아래에 일반을 클릭 한 다음 변환 하거나 마이그레이션 또는 SQL Azure를 선택 합니다.  
  
    -   미리 정의 된 모드를 선택 하 고 **모드** 드롭다운 상자 **기본**, **Optimistic**, 또는 **전체**합니다.  
  
    -   사용자 지정 설정을 지정 하려면에서 단순히 선택 하거나 새 설정이 나 값을 입력 합니다.  
  
3.  클릭 **확인** 설정을 저장할 수 있습니다.  
  
현재 프로젝트에 대 한 설정을 사용자 지정할 수도 있습니다. 이러한 설정은 현재 프로젝트 파일에 저장 됩니다.  
  
**현재 프로젝트에 대 한 설정을 사용자 지정 하려면**  
  
1.  에 **도구** 메뉴 선택 **프로젝트 설정**합니다.  
  
2.  에 **프로젝트 설정** 대화 상자에서 다음 절차 중 하나를 사용 합니다.  
  
    -   미리 정의 된 모드를 선택 하 고 **모드** 드롭다운 상자 **기본**, **Optimistic**, 또는 **전체**합니다.  
  
    -   사용자 지정 모드를 지정 하는 **모드** 드롭다운 선택 상자 **사용자 지정**에서 왼쪽된 창에서 옵션을 선택, 설정 또는 오른쪽 창에서 값을 클릭 한 다음 선택 하거나 새 설정 또는 값을 입력 합니다.  
  
3.  클릭 **확인** 설정을 저장할 수 있습니다.  
  
## <a name="next-steps"></a>다음 단계  
다음 단계는 마이그레이션에서 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   사용자 지정으로 소스 및 대상 데이터 형식 매핑, 참조 [매핑 Sybase ASE 및 SQL Server 데이터 형식 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)합니다.  
  
-   그렇지 않으면 Sybase 데이터베이스 개체 정의로 변환할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 개체를 정의 합니다. 자세한 내용은 참조 [Sybase ASE 데이터베이스 개체 변환 &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server-Azure SQL DB Sybase ASE 데이터베이스 마이그레이션 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
