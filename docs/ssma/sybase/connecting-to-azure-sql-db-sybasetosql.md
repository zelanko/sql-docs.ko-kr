---
title: "Azure SQL DB (SybaseToSQL)에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 217492904d3d21818fed28222dcc6acaf193c92b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="connecting-to-azure-sql-db-sybasetosql"></a>Azure SQL DB (SybaseToSQL)에 연결
Azure SQL DB에 Sybase 데이터베이스를 마이그레이션하려면 Azure SQL DB의 대상 인스턴스에 연결 해야 합니다. 에 연결할 때 SSMA는 Azure SQL DB 인스턴스의 모든 데이터베이스에 대 한 메타 데이터를 가져오고 Azure SQL DB 메타 데이터 탐색기에서 데이터베이스 메타 데이터를 표시 합니다. SSMA는 Azure SQL DB에 연결 되어 있지만 암호를 저장 하지 않는 인스턴스 정보를 저장 합니다.  
  
Azure SQL DB에 대 한 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 다시 열 때 다시 연결 해야 Azure SQL DB에는 서버에 연결 되어 하려는 경우. Azure SQL DB에 데이터베이스 개체를 로드 하 고 데이터를 마이그레이션할 때까지 오프 라인으로 작업 합니다.  
  
Azure SQL DB의 인스턴스에 대 한 메타 데이터를 자동으로 동기화 되지 않습니다. 대신, Azure SQL DB 메타 데이터 탐색기에서 메타 데이터를 업데이트 하려면 Azure SQL DB 메타 데이터 수동으로 업데이트 해야 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 "동기화 중 Azure SQL DB 메타 데이터" 섹션을 참조 합니다.  
  
## <a name="required-azure-sql-db-permissions"></a>필요한 Azure SQL DB 권한  
Azure SQL DB에 연결 하는 데 사용 되는 계정에는 계정 수행 하는 작업에 따라 다른 권한이 필요 합니다.  
  
1.  Sybase 개체를 변환 하려면 [!INCLUDE[tsql](../../includes/tsql_md.md)] 를 Azure SQL DB에서 메타 데이터를 업데이트 하거나 저장 하는 변환 된 구문을 구문, 스크립트, 계정에는 Azure SQL DB 인스턴스에 로그온 할 수 있는 권한이 있어야 합니다.  
  
2.  Azure SQL DB에 데이터베이스 개체를 로드 하려면의 최소 권한 요구 사항은의 멤버 자격이 **db_owner** 대상 데이터베이스의 데이터베이스 역할입니다.  
  
## <a name="establishing-a-azure-sql-db-connection"></a>Azure SQL DB 연결을 설정  
Sybase 데이터베이스 개체를 Azure SQL DB 구문으로 변환 하기 전에 Azure SQL DB Sybase 데이터베이스 또는 데이터베이스를 마이그레이션할 하려는 인스턴스에 대 한 연결을 설정 해야 합니다.  
  
연결 속성을 정의할 때도 데이터베이스 개체와 데이터 마이그레이션할 수를 지정 합니다. Azure SQL DB에 연결한 다음 Sybase 스키마 수준에서이 매핑을 사용자 지정할 수 있습니다. 자세한 내용은 참조 [SQL Server 스키마 &#40; Sybase ASE 스키마 매핑 SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> Azure SQL DB에 연결 하려고 하기 전에 Azure SQL DB의 인스턴스가 실행 되 고 연결을 허용할 수 있는지 확인 합니다.  
  
**Azure SQL DB에 연결 하려면**  
  
1.  에 **파일** 메뉴 선택 **Azure SQL DB에 연결**(이 옵션은 프로젝트를 만든 후).  
  
    Azure SQL DB에 이전에 연결한 경우 명령 이름 됩니다 **Azure SQL DB에 다시 연결**  
  
2.  연결 대화 상자에서 입력 하거나 Azure SQL DB의 서버 이름을 선택 합니다.  
  
3.  선택, 입력 또는 **찾아보기** 데이터베이스 이름입니다.  
  
4.  입력 하거나 선택 **UserName**합니다.  
  
5.  입력은 **암호**합니다.  
  
6.  SSMA는 Azure SQL DB에 암호화 된 연결을 권장합니다.  
  
7.  **연결**을 클릭합니다.  
  
> [!IMPORTANT]  
> SSMA for Sybase 연결을 지원 하지 않습니다 **마스터** Azure SQL DB에는 데이터베이스입니다.  
  
## <a name="synchronizing-azure-sql-db-metadata"></a>Azure SQL DB 메타 데이터를 동기화합니다.  
Azure SQL DB 데이터베이스에 대 한 메타 데이터를 자동으로 업데이트 되지 않습니다. Azure SQL DB 메타 데이터 탐색기에 있는 메타 데이터는 Azure SQL DB 또는 마지막으로 메타 데이터를 수동으로 업데이트 하는에 처음 연결 하는 경우 메타 데이터의 한 스냅숏입니다. 모든 데이터베이스에 대해 또는 모든 단일 데이터베이스 또는 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 동기화 하려면**  
  
1.  Azure SQL DB에 연결 되어 있는지 확인 합니다.  
  
2.  Azure SQL DB 메타 데이터 탐색기에서 데이터베이스 또는 데이터베이스 스키마를 업데이트 하려면 옆에 있는 확인란을 선택 합니다.  
  
    예를 들어 모든 데이터베이스에 대 한 메타 데이터를 업데이트 하려면 데이터베이스 옆의 상자를 선택 합니다.  
  
3.  데이터베이스 또는 개별 데이터베이스 또는 데이터베이스 스키마를 마우스 오른쪽 단추로 클릭 한 다음 선택 **데이터베이스와 동기화**합니다.  
  
## <a name="next-step"></a>다음 단계  
다음 단계는 마이그레이션에서 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   Sybase 스키마 및 Azure SQL DB 데이터베이스 및 스키마 간의 매핑을 사용자 지정, 하려면 참조 [SQL Server 스키마 &#40; Sybase ASE 스키마 매핑 SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   참조 프로젝트에 대 한 구성 옵션을 사용자 지정 하려면 [프로젝트 옵션 설정 &#40; SybaseToSQL &#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   원본 및 대상 데이터 형식 매핑, 사용자 지정 하려면 참조 [매핑 Sybase ASE 및 SQL Server 데이터 형식 &#40; SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   이러한 작업을 수행 해야 하는 경우 Azure SQL DB 개체 정의를 Sybase 데이터베이스 개체 정의 변환할 수 있습니다. 자세한 내용은 참조 [Sybase ASE 데이터베이스 개체 변환 &#40; SybaseToSQL &#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>참고 항목  
[Azure SQL DB &#40; SQL Server-Sybase ASE 데이터베이스 마이그레이션 SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

