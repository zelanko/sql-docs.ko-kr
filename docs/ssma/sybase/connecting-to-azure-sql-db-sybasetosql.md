---
title: Azure SQL DB에 연결 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 10be1dc3652c944b9de08a01b0f4cdff5ae5849a
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176232"
---
# <a name="connecting-to-azure-sql-db-sybasetosql"></a>Azure SQL DB에 연결(SybaseToSQL)
Sybase 데이터베이스를 Azure SQL DB로 마이그레이션하려면 Azure SQL DB의 대상 인스턴스에 연결 해야 합니다. 연결할 때 SSMA는 Azure SQL DB의 인스턴스에 있는 모든 데이터베이스에 대 한 메타 데이터를 가져오고 Azure SQL DB 메타 데이터 탐색기에서 데이터베이스 메타 데이터를 표시 합니다. SSMA는 연결 된 Azure SQL DB의 인스턴스에 대 한 정보를 저장 하지만 암호를 저장 하지는 않습니다.  
  
Azure SQL DB에 대 한 연결은 프로젝트를 닫을 때까지 활성 상태로 유지 됩니다. 프로젝트를 다시 열 때 서버에 대 한 활성 연결을 원하는 경우 Azure SQL DB에 다시 연결 해야 합니다. Azure SQL DB에 데이터베이스 개체를 로드 하 고 데이터를 마이그레이션할 때까지 오프 라인으로 작업할 수 있습니다.  
  
Azure SQL DB 인스턴스에 대 한 메타 데이터는 자동으로 동기화 되지 않습니다. 대신 azure SQL DB 메타 데이터 탐색기에서 메타 데이터를 업데이트 하려면 Azure SQL DB 메타 데이터를 수동으로 업데이트 해야 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 "Azure SQL DB 메타 데이터 동기화" 섹션을 참조 하세요.  
  
## <a name="required-azure-sql-db-permissions"></a>필요한 Azure SQL DB 권한  
Azure SQL DB에 연결 하는 데 사용 되는 계정에는 계정에서 수행 하는 작업에 따라 다른 사용 권한이 필요 합니다.  
  
1.  Sybase 개체를 구문으로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 변환 하거나, Azure sql db에서 메타 데이터를 업데이트 하거나, 변환 된 구문을 스크립트에 저장 하려면 계정에 azure sql db 인스턴스에 로그온 할 수 있는 권한이 있어야 합니다.  
  
2.  Azure SQL DB에 데이터베이스 개체를 로드 하기 위해 최소 권한 요구 사항은 대상 데이터베이스에서 **db_owner** 데이터베이스 역할의 멤버 자격입니다.  
  
## <a name="establishing-an-azure-sql-db-connection"></a>Azure SQL DB 연결 설정  
Sybase 데이터베이스 개체를 Azure SQL DB 구문으로 변환 하기 전에 Sybase 데이터베이스를 마이그레이션하려는 Azure SQL DB 인스턴스에 대 한 연결을 설정 해야 합니다.  
  
연결 속성을 정의 하는 경우 개체 및 데이터가 마이그레이션되는 데이터베이스도 지정 합니다. Azure SQL DB에 연결한 후 Sybase 스키마 수준에서이 매핑을 사용자 지정할 수 있습니다. 자세한 내용은 [SQL Server &#40;스키마에 Sybase ASE 스키마 매핑 sybasetosql&#41; 을](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md) 참조 하세요.  
  
> [!WARNING]  
> Azure SQL DB에 연결 하기 전에 Azure SQL DB 인스턴스가 실행 되 고 있는지 확인 하 고 연결을 허용할 수 있는지 확인 하세요.  
  
**Azure SQL DB에 연결 하려면**  
  
1.  **파일** 메뉴에서 **Azure SQL DB에 연결**(이 옵션은 프로젝트를 만든 후에 사용 됨)을 선택 합니다.  
  
    이전에 Azure SQL DB에 연결한 경우 명령 이름이 **AZURE SQL db에 다시 연결** 됩니다.  
  
2.  연결 대화 상자에서 Azure SQL DB의 서버 이름을 입력 하거나 선택 합니다.  
  
3.  데이터베이스 이름을 입력 하 고 선택 하거나 **탐색** 합니다.  
  
4.  **사용자 이름**을 입력 하거나 선택 합니다.  
  
5.  **암호**를 입력 합니다.  
  
6.  SSMA는 Azure SQL DB에 대 한 암호화 된 연결을 권장 합니다.  
  
7.  **연결**을 클릭합니다.  
  
> [!IMPORTANT]  
> Sybase 용 SSMA는 Azure SQL DB의 **master** 데이터베이스에 대 한 연결을 지원 하지 않습니다.  
  
## <a name="synchronizing-azure-sql-db-metadata"></a>Azure SQL DB 메타 데이터 동기화  
Azure SQL DB 데이터베이스에 대 한 메타 데이터는 자동으로 업데이트 되지 않습니다. Azure SQL DB 메타 데이터 탐색기의 메타 데이터는 처음으로 Azure SQL DB에 연결 하거나 메타 데이터를 마지막으로 업데이트할 때의 메타 데이터에 대 한 스냅숏입니다. 모든 데이터베이스 또는 단일 데이터베이스 또는 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 동기화 하려면**  
  
1.  Azure SQL DB에 연결 되어 있는지 확인 합니다.  
  
2.  Azure SQL DB 메타 데이터 탐색기에서 업데이트 하려는 데이터베이스 또는 데이터베이스 스키마 옆의 확인란을 선택 합니다.  
  
    예를 들어 모든 데이터베이스에 대 한 메타 데이터를 업데이트 하려면 데이터베이스 옆의 상자를 선택 합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭 하거나 개별 데이터베이스 또는 데이터베이스 스키마를 클릭 한 다음 **데이터베이스와 동기화**를 선택 합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션의 다음 단계는 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   Sybase 스키마와 Azure SQL DB 데이터베이스 및 스키마 간의 매핑을 사용자 지정 하려면 [SQL Server &#40;스키마에 Sybase ASE 스키마 매핑 sybasetosql&#41; ](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md) 을 참조 하세요.  
  
-   프로젝트에 대 한 구성 옵션을 사용자 지정 하려면 [프로젝트 옵션 &#40;설정 sybasetosql&#41; ](../../ssma/sybase/setting-project-options-sybasetosql.md) 을 참조 하세요.  
  
-   원본 및 대상 데이터 형식의 매핑을 사용자 지정 하려면 [SYBASE ASE 및 SQL Server 데이터 형식 &#40;매핑 sybasetosql&#41; ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md) 을 참조 하세요.  
  
-   이러한 작업을 수행할 필요가 없는 경우 Sybase 데이터베이스 개체 정의를 Azure SQL DB 개체 정의로 변환할 수 있습니다. 자세한 내용은 [SYBASE ASE 데이터베이스 개체 &#40;변환 sybasetosql&#41; ](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md) 을 참조 하세요.  
  
## <a name="see-also"></a>관련 항목  
[Sybase ASE 데이터베이스를 SQL Server로 마이그레이션-Azure SQL &#40;DB sybasetosql&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
