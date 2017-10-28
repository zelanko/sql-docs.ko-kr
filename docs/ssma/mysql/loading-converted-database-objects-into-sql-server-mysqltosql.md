---
title: "데이터베이스 개체를 SQL Server (MySQLToSQL)로 변환 된 로드 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ac993a6d-0283-4823-8793-6b217677dfa3
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dce262249789e1b7335b1af0d8576239747d5347
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="loading-converted-database-objects-into-sql-server-mysqltosql"></a>데이터베이스 개체를 SQL Server (MySQLToSQL)로 변환 된 로드
MySQL 데이터베이스를 변환한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SQL Azure가 결과 데이터베이스 개체를 로드할 수 있습니다 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다. 개체를 만들 SSMA를 포함할 수 있고 개체를 스크립팅 합니다 스크립트를 실행할 수 있습니다. 또한 SSMA로 업데이트할 수 대상 메타 데이터의 실제 내용이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 데이터베이스입니다.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>동기화 및 스크립트 중에서 선택  
로 변환 된 데이터베이스 개체를 로드 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 하거나 수정 하지 않고 SQL Azure에서 직접 만들거나 데이터베이스 개체를 다시 만들 SSMA를 할 수 있습니다. 메서드는 빠르고 쉬우며, 하지만 정의 하는 Transact SQL 코드의 사용자 지정이 가능 하지 않습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 개체입니다.  
  
수정할 개체를 만드는 데 사용 되는 TRANSACT-SQL 또는 개체를 만드는 보다 자세히 제어 하려면 SSMA를 사용 하 여 스크립트를 만듭니다. 다음 이러한 스크립트를 수정 하 고, 각 개체를 개별적으로 만들 하 고,도 SQL Server 에이전트를 사용 하 여 이러한 개체를 만드는 예약할 수 있습니다.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>SSMA를 사용 하 여 SQL Server와 함께 개체를 동기화 하려면  
개체를 선택 하려면 SSMA를 사용 하 여 SQL Server 또는 SQL Azure 데이터베이스 개체 만들기를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 메타 데이터 탐색기를 사용 하 여 개체를 만든 다음 동기화 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure, 다음 절차에 나와 있는 것 처럼 합니다. 기본적으로 개체에 이미 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure SSMA 메타 데이터에 일부 로컬 변경 내용이 나 해당 매우 개체의 정의에 대 한 업데이트 경우 SSMA에서의 개체 정의 변경 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다. 편집 하 여 기본 동작을 변경할 수 있습니다 **프로젝트 설정**합니다.  
  
> [!NOTE]  
> 기존 선택할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 MySQL 데이터베이스에서 변환 되지 않은 SQL Azure 데이터베이스 개체입니다. 그러나 이러한 개체는 다시 작성 또는 수 SSMA에 의해 변경.  
  
##### <a name="to-synchronize-objects-with-sql-server-or-sql-azure"></a>SQL Server 또는 SQL Azure와 함께 개체를 동기화 하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 메타 데이터 탐색기를 위쪽 확장 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 노드를 확장 한 후 **데이터베이스**합니다.  
  
2.  처리할 개체를 선택 합니다.  
  
    -   전체 데이터베이스를 동기화 하려면 데이터베이스 이름 옆에 있는 확인란을 선택 합니다.  
  
    -   동기화 하거나 생략 개별 개체 또는 개체의 범주를 선택 하거나 개체 또는 폴더 옆에 있는 확인란의 선택을 취소 합니다.  
  
3.  SQL Server 또는 SQL Azure 메타 데이터 탐색기에서 처리할 개체를 선택한 후 마우스 오른쪽 단추로 클릭 **데이터베이스**, 클릭 하 고 **데이터베이스와 동기화**합니다.  
  
    개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 한 다음 클릭 하 여 개별 개체 또는 개체 범주의 동기화도 **데이터베이스와 동기화**합니다.  
  
    그 후 SSMA 표시 됩니다는 **데이터베이스와 동기화** 대화 상자에서 두 개의 항목 그룹이 확인할 수 있습니다. 왼쪽에서 SSMA 트리에 표시 되는 선택한 데이터베이스 개체를 표시 합니다. 오른쪽에서 SSMA 메타 데이터에 동일한 개체를 나타내는 트리를 볼 수 있습니다. 있습니다 수 왼쪽 이나 오른쪽을 클릭 하 여 트리를 확장 합니다. ' +' 단추입니다. 동기화 방향 두 트리 사이 배치 작업 열에 표시 됩니다.  
  
    동작 기호는 다음 세 가지 상태로 될 수 있습니다.  
  
    -   왼쪽된 화살표 메타 데이터의 내용을 (기본값) 데이터베이스에 저장할 것을 의미 합니다.  
  
    -   오른쪽 화살표 데이터베이스 내용 SSMA 메타 데이터를 덮어씁니다를 의미 합니다.  
  
    -   교차 기호 아무 작업도 수행 될 것을 의미 합니다.  
  
    -   상태를 변경 하려면 작업 기호를 클릭 합니다. 클릭할 때 실제 동기화가 수행 **확인** 의 단추는 **데이터베이스와 동기화** 대화 상자.  
  
## <a name="scripting-objects"></a>스크립팅 개체  
저장 하려면 [!INCLUDE[tsql](../../includes/tsql_md.md)] 변환 된 데이터베이스 개체 또는 개체 정의 변경 하 고 스크립트를 실행 하려면 정의 저장할 수 있습니다 변환된 데이터베이스 개체 정의를 [!INCLUDE[tsql](../../includes/tsql_md.md)] 스크립트입니다.  
  
**스크립트 개체를 저장 하려면**  
  
1.  사용자가 스크립트에 저장 하는 개체를 선택한 후 마우스 오른쪽 단추로 클릭 **데이터베이스**, 클릭 하 고 **스크립트로 저장**합니다.  
  
    개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 한 다음 클릭 하 여 개별 개체 또는 개체 범주의 스크립팅하여 수도 **스크립트로 저장**합니다.  
  
2.  에 **다른 이름으로 저장** 대화 상자에서에 파일 이름을 입력 하는 스크립트를 저장 하려는 폴더를 찾습니다는 **파일 이름** 상자 차례로 [!INCLUDE[clickOK](../../includes/clickok_md.md)] SSMA.sql 파일 이름 확장명을 추가 합니다.  
  
### <a name="modifying-scripts"></a>스크립트 수정  
스크립트와 SQL Server 또는 SQL Azure 개체 정의 저장 후 스크립트를 수정 하려면 SQL Server Management Studio를 사용할 수 있습니다.  
  
**스크립트를 수정 하려면**  
  
1.  Management Studio에서 **파일** 메뉴에서 **열려**, 클릭 하 고 **파일**합니다.  
  
2.  열기 대화 상자에서 스크립트 파일을 찾아 클릭 **확인**합니다.  
  
3.  쿼리 편집기를 사용 하 여 스크립트 파일을 편집 합니다. 쿼리 편집기에 대 한 자세한 내용은 "편집기 편의 명령 및 기능" SQL Server 온라인 설명서의를 참조 하십시오.  
  
4.  파일 메뉴에서 스크립트를 저장 하려면 선택 **저장**합니다.  
  
### <a name="running-scripts"></a>스크립트 실행  
SQL Server Management Studio에서 스크립트 또는 개별 문을 실행할 수 있습니다.  
  
**스크립트를 실행 하려면**  
  
1.  SQL Server Management Studio에서 **파일** 메뉴에서 **열려** 클릭 하 고 **파일**합니다.  
  
2.  열기 대화 상자에서 스크립트 파일을 찾아 클릭 **확인**합니다.  
  
3.  전체 스크립트를 실행 하려면는 **F5** 키입니다.  
  
4.  문 집합을 실행 하려면 쿼리 편집기 창에서 문을 선택 하 고 다음 키를 누릅니다는 **F5** 키입니다.  
  
5.  스크립트를 실행 하려면 쿼리 편집기를 사용 하는 방법에 대 한 자세한 내용은 "SQL Server Management Studio-쿼리"에서 SQL Server 온라인 설명서를 참조 하십시오.  
  
6.  사용 하 여 명령줄에서 스크립트를 실행할 수도 있습니다는 **sqlcmd** 유틸리티 및 SQL Server 에이전트에서 합니다. 에 대 한 자세한 내용은 **sqlcmd**, SQL Server 온라인 설명서의 "sqlcmd 유틸리티"를 참조 하십시오. SQL Server 에이전트에 대 한 자세한 내용은 "자동화 Administrative Tasks (SQL Server Agent)" SQL Server 온라인 설명서의를 참조 하십시오.  
  
## <a name="securing-objects-in-sql-server"></a>SQL Server 개체의에서 보안 설정  
SQL Server로 변환 된 데이터베이스 개체를 로드 하면 부여 하거나 이러한 개체에 대 한 권한을 거부할 수 있습니다. 마이그레이션하기 전에이 작업을 수행 하는 것이 좋습니다 데이터를 SQL Server. SQL Server에서 개체를 보호 하는 방법에 대 한 내용은 "보안 고려 사항에 대 한 데이터베이스 및 데이터베이스 응용 프로그램"에서 SQL Server 온라인 설명서를 참조 하십시오.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [를 Azure SQL DB &#40; SQL Server-MySQL 데이터 마이그레이션 MySQLToSQL &#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
## <a name="see-also"></a>관련 항목:  
[Azure SQL DB &#40; SQL Server-MySQL 데이터베이스 마이그레이션 MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

