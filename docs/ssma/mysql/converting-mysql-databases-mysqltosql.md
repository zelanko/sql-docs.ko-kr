---
title: MySQL 데이터베이스 변환 (MySQLToSQL) | Microsoft Docs
description: 프로젝트 및 데이터 매핑 옵션을 연결 하 고 설정한 후에는 MySQL 데이터베이스 개체를 SSMA를 사용 하 SQL Server 또는 Azure SQL Database 개체로 변환 하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac21850b-fb32-4704-9985-5759b7c688c7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c6f8e53a13d5950138f71ed9b4858419eb70f07f
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823290"
---
# <a name="converting-mysql-databases-mysqltosql"></a>MySQL 데이터베이스 변환(MySQLToSQL)
MySQL에 연결 하 고,에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하거나 SQL Azure 하 고, 프로젝트 및 데이터 매핑 옵션을 설정 하 고 나면 mysql 데이터베이스 개체를로 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하거나 데이터베이스 개체를 SQL Azure 수 있습니다.  
  
## <a name="the-conversion-process"></a>변환 프로세스  
데이터베이스 개체를 변환 하는 것은 MySQL의 개체 정의를 사용 하 여 유사 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하거나 SQL Azure 개체로 변환한 후 SSMA 메타 데이터에이 정보를 로드 합니다. 인스턴스에 정보를 로드 하지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 그런 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 메타 데이터 탐색기를 사용 하 여 개체 및 해당 속성을 볼 수 있습니다.  
  
변환 하는 동안 SSMA는 출력 창에 출력 메시지를 인쇄 하 고 오류 목록 창에 오류 메시지를 출력 합니다. 출력 및 오류 정보를 사용 하 여 원하는 변환 결과를 얻기 위해 MySQL 데이터베이스 또는 변환 프로세스를 수정 해야 하는지 여부를 결정할 수 있습니다.  
  
## <a name="setting-conversion-options"></a>변환 옵션 설정  
개체를 변환 하기 전에 **프로젝트 설정** 대화 상자에서 프로젝트 변환 옵션을 검토 합니다. 이 대화 상자를 사용 하 여 SSMA가 테이블과 인덱스를 변환 하는 방법을 설정할 수 있습니다. 자세한 내용은 [프로젝트 설정 &#40;변환&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md) 을 참조 하십시오.  
  
## <a name="conversion-results"></a>변환 결과  
다음 표에서는 변환 된 MySQL 개체 및 결과 개체를 보여 줍니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|MySQL 개체|결과 SQL Server 개체|  
|-|-|  
|인덱스와 같은 종속 개체가 있는 테이블|SSMA는 종속 개체가 있는 테이블을 만듭니다. 테이블은 모든 인덱스 및 제약 조건으로 변환 됩니다. 인덱스는 별도의 개체로 변환 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br />**공간 데이터 형식 매핑은** 테이블 노드 수준 에서만 수행할 수 있습니다.<br /><br />테이블 변환 설정에 대 한 자세한 내용은 [변환 설정](conversion-settings-mysqltosql.md) 을 참조 하세요.|  
|함수|함수를 Transact-sql로 직접 변환할 수 있는 경우 SSMA는 함수를 만듭니다. 경우에 따라 함수를 저장 프로시저로 변환 해야 합니다. 프로젝트 설정에서 **함수 변환을** 사용 하 여이 작업을 수행할 수 있습니다. 이 경우 SSMA는 저장 프로시저와 저장 프로시저를 호출 하는 함수를 만듭니다.<br /><br />**지정 된 항목:**<br /><br />프로젝트 설정에 따라 변환<br /><br />함수로 변환<br /><br />저장 프로시저로 변환<br /><br />함수 변환 설정에 대 한 자세한 내용은 [변환 설정](conversion-settings-mysqltosql.md) 을 참조 하세요.|  
|프로시저|프로시저를 Transact-sql로 직접 변환할 수 있으면 SSMA에서 저장 프로시저를 만듭니다. 경우에 따라 저장 프로시저를 자치 트랜잭션에서 호출 해야 합니다. 이 경우 SSMA는 두 개의 저장 프로시저를 만듭니다. 하나는 프로시저를 구현 하 고 다른 하나는 구현 하는 저장 프로시저를 호출 하는 데 사용 됩니다.|  
|데이터베이스 변환|MySQL 개체인 데이터베이스는 MySQL 용 SSMA에서 직접 변환 되지 않습니다. MySQL 데이터베이스는 스키마 이름과 유사 하 게 처리 되며, 모든 물리적 매개 변수는 변환 중에 손실 됩니다. MySQL 용 SSMA는 mysql 데이터베이스 매핑을 사용 하 여 [MySQLToSQL&#41;&#40;SQL Server 스키마를](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md) 사용 하 여 mysql 데이터베이스의 개체를 적절 한 SQL Server 데이터베이스/스키마 쌍에 매핑합니다.|  
|트리거 변환|**SSMA는 다음 규칙에 따라 트리거를 만듭니다.**<br /><br />Instead of 트리거는 T-sql 트리거 대신로 변환 됩니다.<br /><br />AFTER 트리거는 행 마다 반복을 사용 하거나 사용 하지 않고 T-sql 트리거 후에로 변환 됩니다.|  
|변환 보기|SSMA가 종속 개체를 포함 하는 뷰를 만듭니다.|  
|문 변환|-각 SQL 문 개체에는 단일 MySQL 문 (예: DDL, DML 및 기타 문 유형)이 포함 될 수 있고 BEGIN ... 종료 블록.<br />-   **다중 문 변환: 시작 ... END 블록 변환**SQL 문에는 BEGIN ... 프로시저, 함수 또는 트리거 정의에 있는 것 처럼 블록을 종료 합니다. 이러한 블록은 단일 MySQL 문 개체에 대해 변환 되는 것과 동일한 방식으로 변환 되어야 합니다.|  
  
## <a name="converting-mysql-database-objects"></a>MySQL 데이터베이스 개체 변환  
MySQL 데이터베이스 개체를 변환 하려면 먼저 변환할 개체를 선택 하 고 SSMA에서 변환을 수행 하도록 합니다. 변환 하는 동안 출력 메시지를 보려면 **보기** 메뉴에서 **출력**을 선택 합니다.  
  
**MySQL 개체를 SQL Server 또는 SQL Azure 구문으로 변환 하려면**  
  
1.  MySQL 메타 데이터 탐색기에서 MySQL 서버를 확장 한 다음 **데이터베이스**를 확장 합니다.  
  
2.  변환할 개체 선택:  
  
    -   모든 스키마를 변환 하려면 **데이터베이스**옆의 확인란을 선택 합니다.  
  
    -   데이터베이스를 변환 하거나 생략 하려면 데이터베이스 이름 옆의 확인란을 선택 합니다.  
  
    -   개체의 범주를 변환 하거나 생략 하려면 스키마를 확장 한 다음 범주 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
    -   개별 개체를 변환 하거나 생략 하려면 category 폴더를 확장 한 다음 개체 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
3.  선택한 모든 개체를 변환 하려면 **데이터베이스** 를 마우스 오른쪽 단추로 클릭 하 고 **스키마 변환**을 선택 합니다.  
  
    개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **스키마 변환**을 선택 하 여 개별 개체 또는 개체 범주를 변환할 수도 있습니다.  
  
## <a name="viewing-conversion-problems"></a>변환 문제 보기  
일부 MySQL 개체는 변환 되지 않을 수 있습니다. 요약 변환 보고서를 보면 변환 성공률을 확인할 수 있습니다.  
  
**요약 보고서를 보려면**  
  
1.  MySQL 메타 데이터 탐색기에서 **데이터베이스**를 선택 합니다.  
  
2.  오른쪽 창에서 **보고서** 탭을 선택 합니다.  
  
    이 보고서는 평가 또는 변환 된 모든 데이터베이스 개체에 대 한 요약 평가 보고서를 표시 합니다. 또한 개별 개체에 대 한 요약 보고서를 볼 수 있습니다.  
  
    -   개별 스키마에 대 한 보고서를 보려면 MySQL 메타 데이터 탐색기에서 데이터베이스를 선택 합니다.  
  
    -   개별 개체에 대 한 보고서를 보려면 MySQL 메타 데이터 탐색기에서 개체를 선택 합니다. 변환 문제가 있는 개체에는 빨간색 오류 아이콘이 있습니다.  
  
변환이 실패 한 개체의 경우 변환 실패를 일으킨 구문을 볼 수 있습니다.  
  
**개별 변환 문제를 보려면**  
  
1.  MySQL 메타 데이터 탐색기에서 **데이터베이스**를 확장 합니다.  
  
2.  빨간색 오류 아이콘이 표시 된 데이터베이스를 확장 합니다.  
  
3.  데이터베이스에서 빨간색 오류 아이콘이 있는 폴더를 확장 합니다.  
  
4.  빨간색 오류 아이콘이 있는 개체를 선택 합니다.  
  
5.  오른쪽 창에서 **보고서** 탭을 클릭 합니다.  
  
6.  **보고서** 탭의 맨 위에는 드롭다운 목록이 있습니다. 목록에 **통계가**표시 되 면 선택 항목을 **원본**으로 변경 합니다.  
  
    SSMA는 소스 코드와 코드 바로 위에 몇 개의 단추를 표시 합니다.  
  
7.  **다음 문제** 단추를 클릭 합니다. 오른쪽을 가리키는 화살표가 있는 빨간색 오류 아이콘입니다.  
  
    SSMA는 현재 개체에서 발견 된 첫 번째 문제 소스 코드를 강조 표시 합니다.  
  
변환할 수 없는 각 항목에 대해 해당 개체를 사용 하 여 수행할 작업을 결정 해야 합니다.  
  
-   MySQL 데이터베이스에서 개체를 수정 하 여 문제가 있는 코드를 제거 하거나 수정할 수 있습니다. 업데이트 된 코드를 SSMA에 로드 하려면 메타 데이터를 업데이트 해야 합니다. 자세한 내용은 [MySQL에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md) 을 참조 하세요.  
  
-   마이그레이션할 때 개체를 제외할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]또는 SQL Azure 메타 데이터 탐색기 및 Mysql 메타 데이터 탐색기에서 개체를 로드 하기 전에 항목 옆에 있는 확인란의 선택을 취소 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하거나 mysql에서 데이터를 SQL Azure 및 마이그레이션합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계에서는 변환 된 [데이터베이스 개체를 SQL Server &#40;MySQLToSQL&#41;로드](../../ssma/mysql/loading-converted-database-objects-into-sql-server-mysqltosql.md) 합니다.  
  
## <a name="see-also"></a>참고 항목  
[MySQL 데이터베이스를 SQL Server-Azure SQL Database &#40;MySQLToSql&#41;로 마이그레이션](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
