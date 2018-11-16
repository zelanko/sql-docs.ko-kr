---
title: 데이터베이스에 데이터 또는 로그 파일 추가 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], files
- adding data files
- adding files
- adding log files
- file additions [SQL Server], steps
- files [SQL Server], adding
- data additions [SQL Server]
ms.assetid: 8ead516a-1334-4f40-84b2-509d0a8ffa45
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7de1896d8c94113070dbfc57e31e7af8851b5ce0
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51560198"
---
# <a name="add-data-or-log-files-to-a-database"></a>데이터베이스에 데이터 또는 로그 파일 추가
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 데이터베이스에 데이터 또는 로그 파일을 추가하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **데이터베이스에 데이터 또는 로그 파일을 추가하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   BACKUP 문이 실행 중인 동안에는 파일을 추가 또는 제거할 수 없습니다.  
  
-   각 데이터베이스에 최대 32,767개의 파일과 32,767개의 파일 그룹을 지정할 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-add-data-or-log-files-to-a-database"></a>데이터베이스에 데이터 또는 로그 파일을 추가하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 파일을 추가할 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **데이터베이스 속성** 대화 상자에서 **파일** 페이지를 선택합니다.  
  
4.  데이터 또는 트랜잭션 로그 파일을 추가하려면 **추가**를 클릭합니다.  
  
5.  **데이터베이스 파일** 표에서 파일의 논리적 이름을 입력합니다. 파일 이름은 데이터베이스 내에서 고유해야 합니다.  
  
6.  데이터 또는 로그 중에서 원하는 파일 형식을 선택합니다.  
  
7.  데이터 파일을 선택한 경우 파일을 포함할 파일 그룹을 목록에서 선택하거나 **\<새 파일 그룹>** 을 선택하여 새 파일 그룹을 만듭니다. 트랜잭션 로그는 파일 그룹에 포함할 수 없습니다.  
  
8.  파일의 처음 크기를 지정합니다. 데이터베이스에서 예상되는 최대 데이터 양을 고려하여 데이터 파일의 크기를 최대한 크게 지정합니다.  
  
9. 파일 증가 방법을 지정하려면**자동 증가**열에서 ( **…** )를 클릭합니다. 다음 옵션 중에서 선택합니다.  
  
    1.  현재 선택한 파일이 데이터 공간이 추가로 필요할 때마다 증가되도록 하려면 **자동 증가 사용** 확인란을 선택하고 다음 옵션 중에서 선택합니다.  
  
    2.  파일이 고정된 증가분만큼 증가하도록 지정하려면 **MB 단위로** 를 선택하고 값을 지정합니다.  
  
    3.  파일이 현재 파일 크기의 비율에 따라 증가하도록 지정하려면 **백분율 단위로** 를 선택하고 값을 지정합니다.  
  
10. 최대 파일 크기를 제한하려면 다음 옵션 중에서 선택합니다.  
  
    1.  파일이 증가할 수 있는 최대 크기를 지정하려면 **제한된 파일 증가(MB)** 를 선택하고 값을 지정합니다.  
  
    2.  파일이 필요에 따라 무제한 증가하도록 하려면 **파일 무제한 증가**를 선택합니다.  
  
    3.  파일이 증가되지 않도록 하려면 **자동 증가 사용** 확인란의 선택을 취소합니다. **처음 크기(MB)** 열에 지정된 값에 도달하면 파일 크기가 더 이상 증가하지 않습니다.  
  
    > [!NOTE]  
    >  데이터베이스 최대 크기는 사용 가능한 디스크 공간 크기에 따라 결정되며 라이선스 제한은 사용 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 버전에 따라 결정됩니다.  
  
11. 파일 경로를 지정합니다. 지정한 경로가 있어야 파일을 추가할 수 있습니다.  
  
    > [!NOTE]  
    >  기본적으로 데이터와 트랜잭션 로그는 단일 디스크 시스템에 맞게 동일한 드라이브와 경로에 배치되지만 프로덕션 환경에서는 적절하지 않을 수도 있습니다. 자세한 내용은 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)을 참조하세요.  
  
12. **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-add-data-or-log-files-to-a-database"></a>데이터베이스에 데이터 또는 로그 파일을 추가하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 데이터베이스에 두 개의 파일이 포함된 파일 그룹을 추가합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 `Test1FG1` 파일 그룹을 만들고 이 파일 그룹에 두 개의 5MB 파일을 추가합니다.  
  
 [!code-sql[DatabaseDDL#AlterDatabase2](../../relational-databases/databases/codesnippet/tsql/add-data-or-log-files-to_1.sql)]  
  
 더 많은 예제를 보려면 [ALTER DATABASE 파일 및 파일 그룹 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)   
 [데이터베이스에서 데이터 또는 로그 파일 삭제](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)   
 [데이터베이스의 크기 늘리기](../../relational-databases/databases/increase-the-size-of-a-database.md)  
  
  
