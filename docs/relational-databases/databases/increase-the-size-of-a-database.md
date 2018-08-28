---
title: 데이터베이스의 크기 늘리기 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], size
- increasing database size
- database size [SQL Server], increasing
- size [SQL Server], databases
ms.assetid: 14f4206d-3afa-4ba9-9849-23e81d63306d
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3c3c76a8a748d9387a9f936cf4094cdcd6d8971c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43102380"
---
# <a name="increase-the-size-of-a-database"></a>데이터베이스의 크기 늘리기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 데이터베이스 크기를 늘리는 방법에 대해 설명합니다. 기존 데이터 또는 로그 파일의 크기를 늘리거나 데이터베이스에 새 파일을 추가하여 데이터베이스를 확장할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **데이터베이스의 크기를 늘리려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   BACKUP 문이 실행 중인 동안에는 파일을 추가 또는 제거할 수 없습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-increase-the-size-of-a-database"></a>데이터베이스의 크기를 늘리려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 크기를 늘릴 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **데이터베이스 속성**에서 **파일** 페이지를 선택합니다.  
  
4.  기존 파일의 크기를 늘리려면 파일의 **처음 크기(MB)** 열의 값을 늘립니다. 데이터베이스 크기는 최소 1MB 단위로 늘려야 합니다.  
  
5.  새 파일을 추가하여 데이터베이스 크기를 늘리려면 **추가** 를 클릭한 다음 새 파일에 대한 값을 입력합니다. 자세한 내용은 [Add Data or Log Files to a Database](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)을 참조하세요.  
  
6.  **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-increase-the-size-of-a-database"></a>데이터베이스의 크기를 늘리려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예에서는 `test1dat3` 파일의 크기를 늘립니다.  
  
 [!code-sql[DatabaseDDL#AlterDatabase5](../../relational-databases/databases/codesnippet/tsql/increase-the-size-of-a-d_1.sql)]  
  
 더 많은 예제를 보려면 [ALTER DATABASE 파일 및 파일 그룹 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Add Data or Log Files to a Database](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)   
 [데이터베이스 축소](../../relational-databases/databases/shrink-a-database.md)  
  
  
