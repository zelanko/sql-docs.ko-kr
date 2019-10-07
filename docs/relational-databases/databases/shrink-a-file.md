---
title: 파일 축소 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.shrinkfile.f1
helpviewer_keywords:
- shrinking files
- decreasing file size
- databases [SQL Server], shrinking
- reducing file size
- size [SQL Server], files
- file size [SQL Server]
ms.assetid: ce5c8798-c039-4ab2-81e7-90a8d688b893
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3adf38c1908e17dbac530cab0cc47658e9241559
ms.sourcegitcommit: 5d9ce5c98c23301c5914f142671516b2195f9018
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71961926"
---
# <a name="shrink-a-file"></a>파일 축소
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 데이터 또는 로그 파일을 축소하는 방법에 대해 설명합니다.  
  
 파일 끝에 있는 데이터 페이지를 파일 앞의 사용되지 않은 공간으로 이동하여 데이터 파일을 축소하면 공간이 복구됩니다. 파일 끝에 사용 가능한 공간을 충분히 확보한 다음 파일 끝에 있는 데이터 페이지를 할당 해제하고 파일 시스템에 반환할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **데이터 또는 로그 파일을 축소하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   주 데이터 파일은 model 데이터베이스에 있는 주 파일의 크기보다 작게 만들 수 없습니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   파일 축소를 위해 이동되는 데이터는 파일 내의 모든 사용 가능한 위치로 분산될 수 있습니다. 이로 인해 인덱스 조각화가 발생하여 인덱스 범위를 검색하는 쿼리 성능이 저하될 수 있습니다. 조각화를 방지하려면 축소 후 파일에 대한 인덱스를 다시 작성하는 것이 좋습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 또는 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-shrink-a-data-or-log-file"></a>데이터 또는 로그 파일을 축소하려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스** 를 확장한 다음 축소할 데이터베이스를 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **태스크**, **축소**를 차례로 가리킨 다음 **파일**을 클릭합니다.  
  
     **데이터베이스 백업**  
     선택한 데이터베이스의 이름을 표시합니다.  
  
     **파일 유형**  
     파일의 유형을 선택합니다. **데이터** 와 **로그** 파일 중에 선택할 수 있습니다. 기본 설정은 **데이터**입니다. 다른 파일 그룹 유형을 선택하면 변경 내용에 따라 다른 필드의 선택 내용도 변경됩니다.  
  
     **파일 그룹**  
     위의 **파일 유형** 에서 선택한 내용과 연관된 파일 그룹 목록에서 파일 그룹을 선택합니다. 다른 파일 그룹을 선택하면 변경 내용에 따라 다른 필드의 선택 내용도 변경됩니다.  
  
     **파일 이름**  
     선택한 파일 그룹 및 파일 형식의 사용 가능한 파일 목록에서 파일을 선택합니다.  
  
     **위치**  
     현재 선택된 파일의 전체 경로를 표시합니다. 이 경로는 편집할 수 없지만 클립보드로 복사할 수는 있습니다.  
  
     **현재 할당된 공간**  
     데이터 파일의 경우 현재 할당된 공간을 표시합니다. 로그 파일의 경우 DBCC SQLPERF(LOGSPACE)의 출력에 따라 계산된 현재 할당된 공간을 표시합니다.  
  
     **사용 가능한 공간**  
     데이터 파일의 경우 DBCC SHOWFILESTATS(파일 ID)의 출력에 따라 계산된 현재 사용 가능한 빈 공간을 표시합니다. 로그 파일의 경우 DBCC SQLPERF(LOGSPACE)의 출력에 따라 계산된 현재 사용 가능한 빈 공간을 표시합니다.  
  
     **사용하지 않은 공간 해제**  
     파일에서 사용되지 않는 공간을 운영 체제에 반환하고 마지막으로 할당된 익스텐트까지 파일을 축소하여 데이터를 이동하지 않고 파일 크기를 줄입니다. 할당되지 않은 페이지에 행을 다시 할당하지 않습니다.  
  
     **사용하지 않은 공간을 해제하기 전에 페이지 다시 구성**  
     대상 파일 크기를 지정하는 DBCC SHRINKFILE을 실행한 것과 동일합니다. 이 옵션을 선택한 경우 사용자가 **파일을 다음 크기로 축소** 입력란에 대상 파일 크기를 지정해야 합니다.  
  
     **파일을 다음 크기로 축소**  
     축소 작업의 대상 파일 크기를 지정합니다. 이 크기는 현재 할당된 공간의 크기보다 크고 파일에 할당된 총 익스텐트 수보다 적어야 합니다. 최소값보다 작거나 최대값보다 큰 값을 입력한 경우 포커스를 이동하거나 도구 모음의 단추를 클릭하면 최소값 또는 최대값으로 되돌아갑니다.  
  
     **같은 파일 그룹의 다른 파일로 데이터를 마이그레이션하여 파일 비우기**  
     지정한 파일의 모든 데이터를 마이그레이션합니다. 이 옵션을 선택하면 ALTER DATABASE 문을 사용하여 해당 파일을 삭제할 수 있습니다. 이 옵션은 EMPTYFILE 옵션을 사용하여 DBCC SHRINKFILE을 실행하는 것과 같은 기능을 수행합니다.  
  
4.  파일 형식 및 파일 이름을 선택합니다.  
  
5.  선택적으로 **사용하지 않은 공간 해제** 확인란을 선택합니다.  
  
     이 옵션을 선택하면 파일에서 사용되지 않은 공간이 해제되어 운영 체제에서 사용할 수 있게 되며 파일이 마지막으로 할당된 범위로 축소됩니다. 이렇게 하면 데이터를 이동하지 않아도 파일 크기가 줄어듭니다.  
  
6.  선택적으로 **사용하지 않은 공간을 해제하기 전에 파일을 다시 구성** 확인란을 선택합니다. 이 확인란을 선택하면 **파일을 다음 크기로 축소** 값을 반드시 지정해야 합니다. 기본적으로 이 옵션은 선택되어 있지 않습니다.  
  
     이 옵션을 선택하면 파일에서 사용되지 않은 공간이 해제되어 운영 체제에서 사용할 수 있게 되며 행의 위치를 할당되지 않은 페이지에 지정하려고 합니다.  
  
7.  선택적으로 데이터베이스를 축소한 후 데이터베이스 파일에 남겨둘 여유 공간의 최대 비율을 입력합니다. 허용되는 값은 0에서 99까지입니다. 이 옵션은 **사용하지 않은 공간을 해제하기 전에 파일 다시 구성** 을 활성화한 경우에만 사용할 수 있습니다.  
  
8.  선택적으로 **같은 파일 그룹의 다른 파일로 데이터를 마이그레이션하여 파일 비우기** 확인란을 선택합니다.  
  
     이 옵션을 선택하면 지정된 파일의 모든 데이터가 파일 그룹 내 다른 파일로 이동합니다. 그런 다음 빈 파일을 삭제할 수 있습니다. 이 옵션은 EMPTYFILE 옵션을 사용하여 DBCC SHRINKFILE을 실행하는 것과 같은 기능을 수행합니다.  
  
9. **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-shrink-a-data-or-log-file"></a>데이터 또는 로그 파일을 축소하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) 을 사용하여 `UserDB` 데이터베이스에 있는 `DataFile1` 이라는 데이터 파일의 크기를 7MB로 축소합니다.  
  
 [!code-sql[DBCC#DBCC_SHRINKFILE1](../../relational-databases/databases/codesnippet/tsql/shrink-a-file_1.sql)]  
  
## <a name="see-also"></a>참고 항목  
 [DBCC SHRINKDATABASE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)   
 [데이터베이스 축소](../../relational-databases/databases/shrink-a-database.md)   
 [데이터베이스에서 데이터 또는 로그 파일 삭제](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
  
  
