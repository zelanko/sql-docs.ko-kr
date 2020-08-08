---
title: Azure SQL Database에 연결 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 12e090ef0b2c97fe57d27a61842dd7fe2cb99866
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87932105"
---
# <a name="connecting-to-azure-sql-database-sybasetosql"></a>Azure SQL Database에 연결 (SybaseToSQL)
Sybase 데이터베이스를 Azure SQL Database로 마이그레이션하려면 Azure SQL Database의 대상 인스턴스에 연결 해야 합니다. 연결할 때 SSMA는 Azure SQL Database 인스턴스의 모든 데이터베이스에 대 한 메타 데이터를 가져오고 Azure SQL Database 메타 데이터 탐색기에 데이터베이스 메타 데이터를 표시 합니다. SSMA는 연결 된 Azure SQL Database의 인스턴스에 대 한 정보를 저장 하지만 암호를 저장 하지는 않습니다.  
  
Azure SQL Database에 대 한 연결은 프로젝트를 닫을 때까지 활성 상태로 유지 됩니다. 프로젝트를 다시 열 때 서버에 대 한 활성 연결을 원하는 경우 Azure SQL Database에 다시 연결 해야 합니다. 데이터베이스 개체를 Azure SQL Database로 로드 하 고 데이터를 마이그레이션할 때까지 오프 라인으로 작업할 수 있습니다.  
  
Azure SQL Database 인스턴스에 대 한 메타 데이터는 자동으로 동기화 되지 않습니다. 대신 메타 데이터 탐색기 Azure SQL Database에서 메타 데이터를 업데이트 하려면 Azure SQL Database 메타 데이터를 수동으로 업데이트 해야 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 "Azure SQL Database 메타 데이터 동기화" 섹션을 참조 하십시오.  
  
## <a name="required-azure-sql-database-permissions"></a>필요한 Azure SQL Database 권한  
Azure SQL Database에 연결 하는 데 사용 되는 계정에는 해당 계정에서 수행 하는 작업에 따라 다른 사용 권한이 필요 합니다.  
  
1.  Sybase 개체를 구문으로 변환 [!INCLUDE[tsql](../../includes/tsql-md.md)] 하거나, Azure SQL Database에서 메타 데이터를 업데이트 하거나, 변환 된 구문을 스크립트로 저장 하려면 계정에 Azure SQL Database 인스턴스에 로그온 할 수 있는 권한이 있어야 합니다.  
  
2.  데이터베이스 개체를 Azure SQL Database 로드 하려면 최소 권한 요구 사항이 대상 데이터베이스에서 **db_owner** 데이터베이스 역할의 멤버 자격 이어야 합니다.  
  
## <a name="establishing-an-azure-sql-database-connection"></a>Azure SQL Database 연결 설정  
Sybase 데이터베이스 개체를 Azure SQL Database 구문으로 변환 하기 전에 Sybase 데이터베이스를 마이그레이션하려는 Azure SQL Database 인스턴스에 대 한 연결을 설정 해야 합니다.  
  
연결 속성을 정의 하는 경우 개체 및 데이터가 마이그레이션되는 데이터베이스도 지정 합니다. Azure SQL Database에 연결한 후 Sybase 스키마 수준에서이 매핑을 사용자 지정할 수 있습니다. 자세한 내용은 [SQL Server 스키마에 SYBASE ASE 스키마 매핑 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md) 을 참조 하세요.  
  
> [!WARNING]  
> Azure SQL Database에 연결 하기 전에 Azure SQL Database 인스턴스가 실행 되 고 있는지 확인 하 고 연결을 허용할 수 있는지 확인 하십시오.  
  
**Azure SQL Database에 연결 하려면**  
  
1.  **파일** 메뉴에서 **Azure SQL Database에 연결**을 선택 합니다 .이 옵션은 프로젝트를 만든 후에 사용할 수 있습니다.  
  
    이전에 Azure SQL Database에 연결한 경우 명령 이름이 **Azure SQL Database에 다시 연결** 됩니다.  
  
2.  연결 대화 상자에서 Azure SQL Database 서버 이름을 입력 하거나 선택 합니다.  
  
3.  데이터베이스 이름을 입력 하 고 선택 하거나 **탐색** 합니다.  
  
4.  **사용자 이름**을 입력 하거나 선택 합니다.  
  
5.  **암호**를 입력 합니다.  
  
6.  SSMA는 Azure SQL Database에 대 한 암호화 된 연결을 권장 합니다.  
  
7.  **연결**을 클릭합니다.  
  
> [!IMPORTANT]  
> Sybase 용 SSMA는 Azure SQL Database의 **master** 데이터베이스에 대 한 연결을 지원 하지 않습니다.  
  
## <a name="synchronizing-azure-sql-database-metadata"></a>Azure SQL Database 메타 데이터 동기화  
Azure SQL Database 데이터베이스에 대 한 메타 데이터는 자동으로 업데이트 되지 않습니다. Azure SQL Database 메타 데이터 탐색기의 메타 데이터는 Azure SQL Database에 처음 연결 하거나 마지막으로 메타 데이터를 마지막으로 업데이트 한 경우 메타 데이터의 스냅숏입니다. 모든 데이터베이스 또는 단일 데이터베이스 또는 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 동기화 하려면**  
  
1.  Azure SQL Database에 연결 되어 있는지 확인 합니다.  
  
2.  메타 데이터 탐색기 Azure SQL Database 업데이트 하려는 데이터베이스 또는 데이터베이스 스키마 옆의 확인란을 선택 합니다.  
  
    예를 들어 모든 데이터베이스에 대 한 메타 데이터를 업데이트 하려면 데이터베이스 옆의 상자를 선택 합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭 하거나 개별 데이터베이스 또는 데이터베이스 스키마를 클릭 한 다음 **데이터베이스와 동기화**를 선택 합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션의 다음 단계는 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   Sybase 스키마와 Azure SQL Database 데이터베이스 및 스키마 간의 매핑을 사용자 지정 하려면 [SYBASE ASE 스키마를 SQL Server 스키마에 매핑 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md) 를 참조 하세요.  
  
-   프로젝트에 대 한 구성 옵션을 사용자 지정 하려면 [프로젝트 옵션 설정 &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   원본 및 대상 데이터 형식의 매핑을 사용자 지정 하려면 [SYBASE ASE 매핑 및 SQL Server 데이터 형식 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md) 를 참조 하세요.  
  
-   이러한 작업을 수행할 필요가 없는 경우 Sybase 데이터베이스 개체 정의를 Azure SQL Database 개체 정의로 변환할 수 있습니다. 자세한 내용은 [SYBASE ASE 데이터베이스 개체 변환 &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md) 을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
[Sybase ASE 데이터베이스를 SQL Server-Azure SQL Database &#40;SybaseToSQL&#41;로 마이그레이션](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
