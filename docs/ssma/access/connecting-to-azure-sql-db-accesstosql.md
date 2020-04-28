---
title: Azure SQL DB에 연결 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- instance of SQL Azure
- metadata, refreshing
- refreshing metadata
- SQL Azure
- SQL Azure, connecting
- SQL Azure, connecting to
- SQL Azure, reconnecting
- SQL Azure, synchronizing metadata
ms.assetid: 1ba0d113-dc05-4431-8689-e14a8821bafd
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 6c35168f1c77f0574b202b77da515dab497a3ec7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68006658"
---
# <a name="connecting-to-azure-sql-db-accesstosql"></a>Azure SQL DB에 연결 (AccessToSQL)
Access 데이터베이스를 SQL Azure로 마이그레이션하려면 SQL Azure의 대상 인스턴스에 연결 해야 합니다. 연결할 때 SSMA는 SQL Azure 인스턴스의 모든 데이터베이스에 대 한 메타 데이터를 가져오고 SQL Azure 메타 데이터 탐색기에 데이터베이스 메타 데이터를 표시 합니다. SSMA는 연결 된 SQL Azure의 인스턴스에 대 한 정보를 저장 하지만 암호를 저장 하지는 않습니다.  
  
SQL Azure에 대 한 연결은 프로젝트를 닫을 때까지 활성 상태로 유지 됩니다. 프로젝트를 다시 열 때 서버에 대 한 활성 연결을 원하는 경우 SQL Azure에 다시 연결 해야 합니다. 데이터베이스 개체를 SQL Azure로 로드 하 고 데이터를 마이그레이션할 때까지 오프 라인으로 작업할 수 있습니다.  
  
SQL Azure 인스턴스에 대 한 메타 데이터는 자동으로 동기화 되지 않습니다. 대신 메타 데이터 탐색기 SQL Azure에서 메타 데이터를 업데이트 하려면 SQL Azure 메타 데이터를 수동으로 업데이트 해야 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 "SQL Azure 메타 데이터 동기화" 섹션을 참조 하십시오.  
  
## <a name="required-sql-azure-permissions"></a>필요한 SQL Azure 권한  
SQL Azure에 연결 하는 데 사용 되는 계정에는 해당 계정에서 수행 하는 작업에 따라 다른 사용 권한이 필요 합니다.  
  
-   Access 개체를 구문으로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 변환 하거나, SQL Azure에서 메타 데이터를 업데이트 하거나, 변환 된 구문을 스크립트로 저장 하려면 계정에 SQL Azure 인스턴스에 로그온 할 수 있는 권한이 있어야 합니다.  
  
-   데이터베이스 개체를 SQL Azure 로드 하려면 최소 권한 요구 사항이 대상 데이터베이스에서 **db_owner** 데이터베이스 역할의 멤버 자격 이어야 합니다.  
  
## <a name="establishing-a-sql-azure-connection"></a>SQL Azure 연결 설정  
Access 데이터베이스 개체를 SQL Azure 구문으로 변환 하기 전에 Access 데이터베이스를 마이그레이션하려는 SQL Azure의 인스턴스에 대 한 연결을 설정 해야 합니다.  
  
연결 속성을 정의 하는 경우 개체 및 데이터가 마이그레이션되는 데이터베이스도 지정 합니다. SQL Azure에 연결한 후에 액세스 스키마 수준에서이 매핑을 사용자 지정할 수 있습니다. 자세한 내용은 [Access 데이터베이스를 SQL Server 스키마에 매핑](mapping-source-and-target-databases-accesstosql.md) 을 참조 하세요.  
  
> [!IMPORTANT]  
> SQL Azure에 연결 하기 전에 SQL Azure 인스턴스가 실행 되 고 있는지 확인 하 고 연결을 허용할 수 있는지 확인 하십시오.  
  
**SQL Azure에 연결 하려면**  
  
1.  **파일** 메뉴에서 **SQL Azure에 연결** 을 선택 합니다 .이 옵션은 프로젝트를 만든 후에 사용할 수 있습니다.  
  
    이전에 SQL Azure에 연결한 경우 명령 이름이 **SQL Azure에 다시 연결**됩니다.  
  
2.  연결 대화 상자에서 SQL Azure 서버 이름을 입력 하거나 선택 합니다.  
  
3.  데이터베이스 이름을 입력 하 고 선택 하거나 **탐색** 합니다.  
  
4.  **사용자 이름**을 입력 하거나 선택 합니다.  
  
5.  **암호**를 입력 합니다.  
  
6.  SSMA는 SQL Azure에 대 한 암호화 된 연결을 권장 합니다.  
  
7.  **연결**을 클릭합니다.  
  
> [!IMPORTANT]  
> Access 용 SSMA는 SQL Azure의 **master** 데이터베이스에 대 한 연결을 지원 하지 않습니다.  
  
SQL Azure 계정에 데이터베이스가 없는 경우 **찾아보기** 단추 클릭에 표시 되는 **Azure 데이터베이스 만들기** 옵션을 사용 하 여 첫 번째 데이터베이스를 만들 수 있습니다.  
  
## <a name="synchronizing-sql-azure-metadata"></a>SQL Azure 메타 데이터 동기화  
SQL Azure 데이터베이스에 대 한 메타 데이터는 자동으로 업데이트 되지 않습니다. SQL Azure 메타 데이터 탐색기의 메타 데이터는 SQL Azure에 처음 연결 하거나 마지막으로 메타 데이터를 마지막으로 업데이트 한 경우 메타 데이터의 스냅숏입니다. 모든 데이터베이스 또는 단일 데이터베이스 또는 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 동기화 하려면**  
  
1.  SQL Azure에 연결 되어 있는지 확인 합니다.  
  
2.  메타 데이터 탐색기 SQL Azure 업데이트 하려는 데이터베이스 또는 데이터베이스 스키마 옆의 확인란을 선택 합니다.  
  
    예를 들어 모든 데이터베이스에 대 한 메타 데이터를 업데이트 하려면 데이터베이스 옆의 상자를 선택 합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭 하거나 개별 데이터베이스 또는 데이터베이스 스키마를 클릭 한 다음 **데이터베이스와 동기화**를 선택 합니다.  
  
## <a name="refreshing-sql-azure-metadata"></a>SQL Azure 메타 데이터 새로 고침  
연결한 후에 스키마가 변경 되는 SQL Azure 경우 서버에서 메타 데이터를 새로 고칠 수 있습니다.  
  
**SQL Azure 메타 데이터를 새로 고치려면**  
  
-   메타 데이터 탐색기 SQL Azure에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭 한 다음 **데이터베이스에서 새로 고침**을 선택 합니다.  
  
## <a name="reconnecting-to-sql-azure"></a>SQL Azure에 다시 연결  
SQL Azure에 대 한 연결은 프로젝트를 닫을 때까지 활성 상태로 유지 됩니다. 프로젝트를 다시 열 때 서버에 대 한 활성 연결을 원하는 경우 SQL Azure에 다시 연결 해야 합니다. 데이터베이스 개체를 SQL Azure로 로드 하 고 데이터를 마이그레이션할 때까지 오프 라인으로 작업할 수 있습니다.  
  
SQL Azure에 다시 연결 하는 절차는 연결을 설정 하는 절차와 같습니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션의 다음 단계는 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   액세스 스키마와 SQL Azure 데이터베이스 및 스키마 간의 매핑을 사용자 지정 하려면 [Access 데이터베이스를 SQL Server 스키마에 매핑](mapping-source-and-target-databases-accesstosql.md)을 참조 하세요.  
  
-   프로젝트에 대 한 구성 옵션을 사용자 지정 하려면 [프로젝트 옵션 설정](setting-conversion-and-migration-options-accesstosql.md)을 참조 하세요.  
  
-   원본 및 대상 데이터 형식의 매핑을 사용자 지정 하려면 [원본 및 대상 데이터 형식 매핑](mapping-source-and-target-data-types-accesstosql.md)을 참조 하세요.  
  
-   이러한 작업을 수행할 필요가 없는 경우 Access 데이터베이스 개체 정의를 SQL Azure 개체 정의로 변환할 수 있습니다. 자세한 내용은 [Access 데이터베이스 변환](converting-access-database-objects-accesstosql.md) (영문)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
