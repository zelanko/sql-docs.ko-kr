---
description: 단일 사용자 모드로 데이터베이스 설정
title: 단일 사용자 모드로 데이터베이스 설정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- single-user mode [SQL Server], database option
ms.assetid: fb5254eb-b635-4b39-8361-136fd36f2b1f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 591a2d22a603c51f44bdfa16d4072e6b9ad36c73
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88471157"
---
# <a name="set-a-database-to-single-user-mode"></a>단일 사용자 모드로 데이터베이스 설정
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 사용자 정의 데이터베이스를 단일 사용자 모드로 설정하는 방법에 대해 설명합니다. 단일 사용자 모드는 한 번에 하나의 사용자만 데이터베이스에 액세스할 수 있도록 지정하며 일반적으로 유지 관리 동작에 사용됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [필수 구성 요소](#Prerequisites)  
  
     [보안](#Security)  
  
-   **데이터베이스를 단일 사용자 모드로 설정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   데이터베이스를 단일 사용자 모드로 설정할 때 다른 사용자가 데이터베이스에 연결되어 있으면 해당 데이터베이스 연결이 경고 없이 닫힙니다.  
  
-   옵션을 설정한 사용자가 로그오프해도 데이터베이스는 단일 사용자 모드로 유지됩니다. 이때 다른 한 명의 사용자만 데이터베이스에 연결할 수 있습니다.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
  
-   데이터베이스를 SINGLE_USER로 설정하기 전에 AUTO_UPDATE_STATISTICS_ASYNC 옵션이 OFF로 설정되어 있는지 확인합니다. 이 옵션이 ON으로 설정되면 통계 업데이트에 사용되는 백그라운드 스레드가 데이터베이스에 대한 연결을 점유하므로 사용자는 단일 사용자 모드로 데이터베이스에 액세스할 수 없습니다. 자세한 내용은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-set-a-database-to-single-user-mode"></a>데이터베이스를 단일 사용자 모드로 설정하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  변경할 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성** 을 클릭합니다.  
  
3.  **데이터베이스 속성** 대화 상자에서 **옵션** 페이지를 클릭합니다.  
  
4.  **액세스 제한** 옵션에서 **단일** 을 선택합니다.  
  
5.  다른 사용자가 데이터베이스에 연결되어 있으면 **열린 연결** 메시지가 나타납니다. 다른 모든 연결을 닫고 속성을 변경하려면 **예** 를 클릭합니다.  
  
 이 절차에 따라 데이터베이스를 다중 또는 제한됨 액세스로 설정할 수도 있습니다. 액세스 제한 옵션에 대한 자세한 내용은 [데이터베이스 속성&#40;옵션 페이지&#41;](../../relational-databases/databases/database-properties-options-page.md)을 참조하세요.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-set-a-database-to-single-user-mode"></a>데이터베이스를 단일 사용자 모드로 설정하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 이 예에서는 데이터베이스를 `SINGLE_USER` 모드로 설정하여 배타적 액세스 권한을 확보한 다음 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 상태를 `READ_ONLY` 로 설정한 후 데이터베이스 액세스를 모든 사용자에게 반환합니다. 종료 옵션 `WITH ROLLBACK IMMEDIATE` 는 첫 번째 `ALTER DATABASE` 문에 지정됩니다. 완료되지 않은 트랜잭션은 모두 롤백되며 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스로의 다른 모든 연결은 즉시 끊어집니다.  
  
 [!code-sql[DatabaseDDL#AlterDatabase8](../../relational-databases/databases/codesnippet/tsql/set-a-database-to-single_1.sql)]  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
