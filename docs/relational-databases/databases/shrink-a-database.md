---
title: 데이터베이스 축소 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.shrinkdatabase.f1
helpviewer_keywords:
- shrinking databases
- databases [SQL Server], shrinking
- decreasing database size
- database shrinking [SQL Server]
- reducing database size
ms.assetid: 83afbf74-fd50-4c39-831c-b1f473a50620
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f7642b2514f7a73034e8f0c2a5c75db71149d33e
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559590"
---
# <a name="shrink-a-database"></a>데이터베이스 축소
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 과 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 개체를 사용하여 데이터베이스를 축소하는 방법에 대해 설명합니다.  
  
 파일 끝에 있는 데이터 페이지를 파일 앞의 사용되지 않은 공간으로 이동하여 데이터 파일을 축소하면 공간이 복구됩니다. 파일 끝에 사용 가능한 공간을 충분히 확보한 다음 파일 끝에 있는 데이터 페이지를 할당 해제하고 파일 시스템에 반환할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **데이터베이스를 축소하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Follow Up:**  [You shrink a database](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   데이터베이스를 최소 데이터베이스 크기보다 작게 축소할 수는 없습니다. 최소 크기는 데이터베이스를 처음 만들 때 지정된 크기나 DBCC SHRINKFILE과 같은 파일 크기 변경 작업을 사용하여 명시적으로 설정한 최종 크기입니다. 예를 들어 원래 10MB로 생성된 데이터베이스가 100MB까지 증가한 경우 포함된 모든 데이터를 삭제하더라도 데이터베이스를 10MB 이하로는 축소할 수 없습니다.  
  
-   데이터베이스가 백업되는 동안에는 데이터베이스를 축소할 수 없습니다. 반대로 데이터베이스에 대한 축소 작업이 처리되는 동안에는 데이터베이스를 백업할 수 없습니다.  
  
-   xVelocity 메모리 최적화 Columnstore 인덱스가 발생할 경우 DBCC SHRINKDATABASE는 실패합니다. Columnstore 인덱스가 발생하기 전에 완료된 작업은 성공하므로 데이터베이스 크기가 작아질 수 있습니다. DBCC SHRINKDATABASE를 완료하려면 DBCC SHRINKDATABASE를 실행하기 전에 모든 columnstore 인덱스를 사용하지 않도록 설정한 다음 columnstore 인덱스를 다시 작성합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   현재 데이터베이스에 있는 여유(할당되지 않은) 공간의 양을 보려면 자세한 내용은 [데이터베이스의 데이터 및 로그 공간 정보 표시](../../relational-databases/databases/display-data-and-log-space-information-for-a-database.md)를 참조하세요.  
  
-   데이터베이스를 축소할 때는 다음을 고려하세요.  
  
    -   축소 작업은 테이블 잘라내기 또는 테이블 삭제 작업과 같이 사용되지 않는 공간이 많이 생기는 작업을 수행한 후에 가장 효과적입니다.  
  
    -   대부분의 데이터베이스에는 정기적인 일상 작업에 사용 가능한 일정 여유 공간이 필요합니다. 데이터베이스를 반복해서 축소했지만 데이터베이스 크기가 다시 늘어나는 경우 일반 작업을 위해 축소된 공간이 필요한 것입니다. 이러한 경우 데이터베이스를 반복해서 축소하는 것은 불필요한 작업입니다.  
  
    -   축소 작업은 데이터베이스 인덱스의 조각화 상태를 보존하지 않으며 일반적으로 조각화 정도를 어느 정도까지 늘리기도 합니다. 이것은 데이터베이스를 반복해서 축소하지 않아야 하는 또 다른 이유입니다.  
  
    -   특정 요구 사항이 없을 경우 AUTO_SHRINK 데이터베이스 옵션을 ON으로 설정하지 마세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 **sysadmin** 고정 서버 역할의 멤버 또는 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-shrink-a-database"></a>데이터베이스를 축소하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 축소할 데이터베이스를 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **태스크**, **축소**를 차례로 가리킨 다음 **데이터베이스**를 클릭합니다.  
  
     **데이터베이스 백업**  
     선택한 데이터베이스의 이름을 표시합니다.  
  
     **현재 할당된 공간**  
     선택한 데이터베이스의 총 사용 공간 및 사용되지 않은 공간을 표시합니다.  
  
     **사용 가능한 공간**  
     선택한 데이터베이스의 로그 및 데이터 파일의 총 사용 가능한 공간을 표시합니다.  
  
     **사용하지 않은 공간을 해제하기 전에 파일을 다시 구성합니다.**  
     이 옵션을 선택하는 것은 목표 백분율 옵션을 지정하여 DBCC SHRINKDATABASE를 실행하는 것과 같습니다. 또한 이 옵션의 선택을 취소하는 것은 TRUNCATEONLY 옵션을 사용하여 DBCC SHRINKDATABASE를 실행하는 것과 같습니다. 기본적으로 대화 상자를 열 때 이 옵션은 선택되어 있지 않습니다. 이 옵션을 선택하면 목표 백분율 옵션을 지정해야 합니다.  
  
     **축소 후 파일에 남는 최대 여유 공간**  
     데이터베이스를 축소한 후 데이터베이스 파일에 남겨둘 여유 공간의 최대 비율을 입력합니다. 허용되는 값은 0에서 99까지입니다.  
  
4.  **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-shrink-a-database"></a>데이터베이스를 축소하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md) 를 사용하여 `UserDB` 데이터베이스의 데이터 및 로그 파일 크기를 줄이고 데이터베이스에 `10` 의 여유 공간이 남도록 합니다.  
  
 [!code-sql[DBCC#DBCC_SHRINKDB1](../../relational-databases/databases/codesnippet/tsql/shrink-a-database_1.sql)]  
  
##  <a name="FollowUp"></a> 후속 작업: 데이터베이스를 축소한 후  
 파일 축소를 위해 이동되는 데이터는 파일 내의 모든 사용 가능한 위치로 분산될 수 있습니다. 이로 인해 인덱스 조각화가 발생하여 인덱스 범위를 검색하는 쿼리 성능이 저하될 수 있습니다. 조각화를 방지하려면 축소 후 파일에 대한 인덱스를 다시 작성하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목  
 [파일 축소](../../relational-databases/databases/shrink-a-file.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
 [DBCC SHRINKFILE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)   
 [데이터베이스 파일 및 파일 그룹](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
