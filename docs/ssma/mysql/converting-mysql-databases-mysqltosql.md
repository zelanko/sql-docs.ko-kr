---
title: MySQL 데이터베이스 (MySQLToSQL) 변환 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac21850b-fb32-4704-9985-5759b7c688c7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1211a1d5f22758b5c3732aa1b9843fe11ef8b3db
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540949"
---
# <a name="converting-mysql-databases-mysqltosql"></a>MySQL 데이터베이스 변환(MySQLToSQL)
MySQL에 연결한 후에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure 프로젝트 설정 및 데이터 매핑 옵션, MySQL 데이터베이스 개체를 변환할 수 있습니다 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터베이스 개체입니다.  
  
## <a name="the-conversion-process"></a>변환 프로세스  
MySQL에서 개체 정의 가져와서, 변환한 유사한 데이터베이스 개체 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체 및 SSMA 메타 데이터에이 정보를 로드 합니다. 인스턴스로 정보를 로드 하지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 사용 하 여 개체 및 해당 속성을 보려면 다음을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 메타 데이터 탐색기입니다.  
  
변환 중 SSMA 출력 창에 출력 메시지 및 오류 목록 창에 오류 메시지를 인쇄합니다. 출력 및 오류 정보를 사용 하 여 MySQL 데이터베이스 또는 원하는 변환 결과 얻으려면 변환 프로세스를 수정 해야 하는지 여부를 결정 합니다.  
  
## <a name="setting-conversion-options"></a>변환 옵션 설정  
개체를 변환 하기 전에 프로젝트 변환 옵션을 검토 합니다 **프로젝트 설정** 대화 상자. 이 대화 상자를 사용 하 여 SSMA 테이블 및 인덱스를 변환 하는 방법을 설정할 수 있습니다. 자세한 내용은 참조 하십시오 [프로젝트 설정 &#40;변환&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
## <a name="conversion-results"></a>변환 결과  
다음 표에서 MySQL 개체가 변환 되 고 결과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체:  
  
|||  
|-|-|  
|**MySQL 개체**|**결과 SQL Server 개체**|  
|인덱스와 같은 종속 개체를 사용 하 여 테이블|SSMA는 종속 개체를 사용 하 여 테이블을 만듭니다. 테이블은 모든 인덱스 및 제약 조건으로 변환 됩니다. 인덱스는 별도 변환 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체입니다.<br /><br />**공간 데이터 형식 매핑** 테이블 노드 수준 에서만 수행할 수 있습니다.<br /><br />테이블 변환 설정에 대 한 자세한 내용은 참조 하세요. [변환 설정](conversion-settings-mysqltosql.md)|  
|함수|Transact-sql 함수를 직접 변환할 수 있으면 SSMA 함수를 만듭니다. 일부 경우에는 저장된 프로시저에 함수를 변환 합니다. 사용 하 여 이렇게 **함수 변환** 프로젝트 설정에서. 이 경우 SSMA는 저장된 프로시저 및 저장된 프로시저를 호출 하는 함수를 만듭니다.<br /><br />**지정 된 선택 사항:**<br /><br />프로젝트 설정에 따라 변환<br /><br />함수 변환<br /><br />저장된 프로시저 변환<br /><br />함수 변환 설정에 대 한 자세한 내용은 참조 하세요. [변환 설정](conversion-settings-mysqltosql.md)|  
|절차|SSMA는 transact-sql 프로시저를 직접 변환할 수 있으면 저장된 프로시저를 만듭니다. 일부 경우에서 자치 트랜잭션을에서 저장된 프로시저를 호출 합니다. 이 경우 SSMA 두 개의 저장된 프로시저를 만듭니다: 하 고 구현 하는 호출에 사용 되는 다른 프로시저를 구현 하는 저장 프로시저입니다.|  
|데이터베이스 변환|MySQL 개체로 데이터베이스는 직접 변환 하지 SSMA MySQL에 대 한 합니다. MySQL 데이터베이스 스키마 이름 같은 더 처리 됩니다 하 고 모든 실제 매개 변수가 변환 중에 손실 됩니다. 다음을 사용 하 여 MySQL 용 SSMA [MySQL 데이터베이스를 SQL Server 스키마에 매핑 &#40;MySQLToSQL&#41; ](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md) 적절 한 SQL Server 데이터베이스/스키마 쌍에 MySQL 데이터베이스에서 개체를 매핑합니다.|  
|트리거 변환|**SSMA는 다음 규칙을 기준으로 하는 트리거를 만듭니다.**<br /><br />트리거는 INSTEAD OF T-SQL 트리거에만로 변환 되기 전에<br /><br />AFTER 트리거 후 T-SQL 트리거에만 행 마다 반복 없이 변환 됩니다.|  
|뷰 변환|SSMA는 종속 개체를 사용 하 여 뷰를 만듭니다.|  
|문 변환|-각 SQL 문의 개체 (예: DDL, DML 및 다른 형식의 문의) 단일 MySQL 문을 포함 될 수 있습니다 또는 시작 하는 중... 끝 블록입니다.<br />-   **다중 문 변환: 시작 하는 중... 최종 블록이 변환**SQL 문을 BEGIN을 포함할 수도 있습니다... 프로시저, 함수 또는 트리거 정의 같은 최종 블록입니다. 해당 블록에는 단일 MySQL statement 개체에 대 한 변환 되는 동일한 방식으로 변환 되어야 합니다.|  
  
## <a name="converting-mysql-database-objects"></a>MySQL 데이터베이스 개체 변환  
MySQL 데이터베이스 개체를 변환 하려면 먼저 변환 하려는 개체를 선택 및 SSMA 변환을 수행 해야 합니다. 변환 하는 동안 출력 메시지를 볼 수는 **뷰** 메뉴에서 **출력**합니다.  
  
**SQL Server 또는 SQL Azure 구문 MySQL 개체 변환**  
  
1.  MySQL 메타 데이터 탐색기에서 MySQL 서버를 확장 한 다음 확장 **데이터베이스**합니다.  
  
2.  변환할 개체를 선택 합니다.  
  
    -   모든 스키마로 변환 하려면 확인란을 선택 합니다 옆 **데이터베이스**합니다.  
  
    -   를 변환 하거나 데이터베이스를 생략 하려면 데이터베이스 이름 옆의 확인란을 선택 합니다.  
  
    -   를 변환 하거나 개체의 범주를 생략 하려면 스키마를 확장 한 다음 선택 하거나 범주 옆에 있는 확인란의 선택을 취소 합니다.  
  
    -   를 변환 하거나 개별 개체를 생략 하려면 범주 폴더를 확장 한 다음 선택 하거나 개체 옆에 있는 확인란의 선택을 취소 합니다.  
  
3.  선택한 모든 개체를 변환 하려면 마우스 오른쪽 단추로 클릭 **데이터베이스** 선택한 **스키마 변환**합니다.  
  
    개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 한 다음 선택 하 여 개별 개체 또는 개체 범주의 변환할 수도 있습니다 **스키마 변환**합니다.  
  
## <a name="viewing-conversion-problems"></a>변환 문제 보기  
일부 MySQL 개체를 변환 될 수 있습니다. 변환 요약 보고서를 확인 하 여 성공 전환율을 확인할 수 있습니다.  
  
**요약 보고서를 보려면**  
  
1.  MySQL 메타 데이터 탐색기에서 선택 **데이터베이스**합니다.  
  
2.  오른쪽 창에서 선택 합니다 **보고서** 탭 합니다.  
  
    이 보고서는 평가 되거나 변환 된 모든 데이터베이스 개체에 대 한 요약 평가 보고서를 표시 합니다. 또한 개별 개체에 대 한 요약 보고서를 볼 수 있습니다.  
  
    -   개별 스키마에 대 한 보고서를 보려면 MySQL 메타 데이터 탐색기에서 데이터베이스를 선택 합니다.  
  
    -   개별 개체에 대 한 보고서를 보려면 MySQL 메타 데이터 탐색기에서 개체를 선택 합니다. 변환 문제가 발생 하는 개체에는 빨간색 오류 아이콘이 있습니다.  
  
변환에 실패 한 개체에 대 한 변환 오류가 발생 하는 구문을 볼 수 있습니다.  
  
**개별 변환 문제를 보려면**  
  
1.  MySQL 메타 데이터 탐색기에서 확장 **데이터베이스**합니다.  
  
2.  빨간색 오류 아이콘이 표시 된 데이터베이스를 확장 합니다.  
  
3.  데이터베이스에서 빨간색 오류 아이콘이 있는 폴더를 확장 합니다.  
  
4.  빨간색 오류 아이콘이 있는 개체를 선택 합니다.  
  
5.  오른쪽 창에서을 클릭 합니다 **보고서** 탭 합니다.  
  
6.  맨 위에 있는 합니다 **보고서** 탭은 드롭 다운 목록. 목록에 표시 되 면 **통계**, 선택 영역을 변경 **원본**합니다.  
  
    SSMA는 소스 코드 및 코드 바로 위의 여러 개의 단추가 표시 됩니다.  
  
7.  클릭 합니다 **문제** 단추입니다. 이것이 오른쪽을 가리키는 화살표를 사용 하 여 빨간색 오류 아이콘입니다.  
  
    SSMA는 현재 개체에서 찾은 첫 번째 문제가 있는 소스 코드를 강조 표시 됩니다.  
  
변환 될 수 있는 각 항목에 대해 해당 개체를 사용 하 여 수행 하려는 항목을 확인 해야 합니다.  
  
-   MySQL 데이터베이스를 제거 하거나 수정 하는 문제가 있는 코드에서 개체를 수정할 수 있습니다. SSMA에 업데이트 된 코드를 로드 하는 메타 데이터를 업데이트 해야 합니다. 자세한 내용은 [MySQL에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   마이그레이션에서 개체를 제외할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure 메타 데이터 탐색기 및 MySQL 메타 데이터 탐색기, 개체를 로드 하기 전에 항목 옆의 확인란의 선택을 취소 하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 및 MySQL에서 데이터를 마이그레이션.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계 [SQL Server로 변환 된 데이터베이스 개체 로드 &#40;MySQLToSQL&#41;](../../ssma/mysql/loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>관련 항목  
[SQL Server-Azure SQL DB로 마이그레이션 MySQL 데이터베이스 &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
