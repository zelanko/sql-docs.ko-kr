---
title: 데이터베이스 분리 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.detachdatabase.f1
helpviewer_keywords:
- database detaching [SQL Server]
- detaching databases [SQL Server]
ms.assetid: f63d4107-13e4-4bfe-922d-5e4f712e472d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 35a118575be4ac15cb44588f1773ea1bb4fbc257
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68006196"
---
# <a name="detach-a-database"></a>데이터베이스 분리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 데이터베이스를 분리하는 방법에 대해 설명합니다. 분리된 파일은 그대로 남아 있으며 FOR ATTACH 또는 FOR ATTACH_REBUILD_LOG 옵션과 함께 CREATE DATABASE를 사용하여 다시 연결할 수 있습니다. 또한 파일을 다른 서버로 이동하거나 첨부할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **데이터베이스를 분리하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
 제한 사항 목록은 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)의 데이터베이스를 분리하는 방법에 대해 설명합니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-detach-a-database"></a>데이터베이스를 분리하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 분리할 사용자 데이터베이스 이름을 선택합니다.  
  
3.  데이터베이스 이름을 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **분리**를 클릭합니다. **데이터베이스 분리** 대화 상자가 나타납니다.  
  
     **분리할 데이터베이스**  
     분리할 데이터베이스를 나열합니다.  
  
     **데이터베이스 이름**  
     분리할 데이터베이스 이름을 표시합니다.  
  
     **연결 삭제**  
     지정한 데이터베이스에 대한 연결을 끊습니다.  
  
    > [!NOTE]  
    >  활성 연결이 있는 데이터베이스는 분리할 수 없습니다.  
  
     **통계 업데이트**  
     기본적으로 분리 작업은 데이터베이스를 분리할 때 오래된 최적화 통계를 유지합니다. 기존의 최적화 통계를 업데이트하려면 이 확인란을 클릭합니다.  
  
     **전체 텍스트 카탈로그 유지**  
     기본적으로 분리 작업은 데이터베이스와 연결된 모든 전체 텍스트 카탈로그를 유지합니다. 전체 텍스트 카탈로그를 제거하려면 **전체 텍스트 카탈로그 유지** 확인란의 선택을 취소합니다. 이 옵션은 데이터베이스를 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 업그레이드하는 경우에만 표시됩니다.  
  
     **상태**  
     **준비** 또는 **준비 안 됨**상태 중 하나를 표시합니다.  
  
     **메시지**  
     다음과 같이 **메시지** 열에 데이터베이스에 대한 정보가 표시될 수도 있습니다.  
  
    -   데이터베이스가 복제와 관련된 경우 **상태** 는 **준비 안 됨** 이고 **메시지** 열에는 **데이터베이스 복제 완료**가 표시됩니다.  
  
    -   데이터베이스에 하나 이상의 활성 연결이 있는 경우 **상태**는 **준비 안 됨**이고 **메시지** 열에는 _<number_of_active_connections>_ **활성 연결**(예: **1개의 활성 연결**)이 표시됩니다. 데이터베이스를 분리하려면 먼저 **연결 삭제**를 선택하여 모든 활성 연결을 끊어야 합니다.  
  
     메시지에 대한 자세한 내용을 보려면 하이퍼링크로 연결된 텍스트를 클릭하여 작업 모니터를 엽니다.  
  
4.  데이터베이스를 분리할 준비가 되었으면 **확인**을 클릭합니다.  
  
> [!NOTE]  
>  새로 분리된 데이터베이스는 뷰를 새로 고칠 때까지 개체 탐색기의 **데이터베이스** 노드에 계속 표시됩니다. 뷰는 언제든지 새로 고칠 수 있습니다. 개체 탐색기 창을 클릭한 다음 메뉴 모음에서 **보기** , **새로 고침**을 차례로 선택합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-detach-a-database"></a>데이터베이스를 분리하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 skipchecks가 true로 설정된 AdventureWorks2012 데이터베이스를 분리합니다.  
  
```  
EXEC sp_detach_db 'AdventureWorks2012', 'true';  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_detach_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)  
  
  
