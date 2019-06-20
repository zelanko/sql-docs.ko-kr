---
title: 데이터베이스 분리 | Microsoft 문서
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.detachdatabase.f1
helpviewer_keywords:
- database detaching [SQL Server]
- detaching databases [SQL Server]
ms.assetid: f63d4107-13e4-4bfe-922d-5e4f712e472d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 050220781f484b4a9e595551496d7e58c06f954c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871958"
---
# <a name="detach-a-database"></a>데이터베이스 분리
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 데이터베이스를 분리하는 방법에 대해 설명합니다. 분리된 파일은 그대로 남아 있으며 FOR ATTACH 또는 FOR ATTACH_REBUILD_LOG 옵션과 함께 CREATE DATABASE를 사용하여 다시 연결할 수 있습니다. 또한 파일을 다른 서버로 이동하거나 첨부할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **데이터베이스를 분리하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 제한 사항 목록은 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)의 데이터베이스를 분리하는 방법에 대해 설명합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-detach-a-database"></a>데이터베이스를 분리하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 분리할 사용자 데이터베이스 이름을 선택합니다.  
  
3.  데이터베이스 이름을 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **분리**를 클릭합니다. **데이터베이스 분리** 대화 상자가 나타납니다.  
  
     **분리할 데이터베이스**  
     분리할 데이터베이스를 나열합니다.  
  
     **Database Name**  
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
     다음 상태 중 하나가 표시 됩니다. **준비** 또는 **준비 안 됨**을 표시합니다.  
  
     **메시지**  
     다음과 같이 **메시지** 열에 데이터베이스에 대한 정보가 표시될 수도 있습니다.  
  
    -   데이터베이스가 복제와 관련된 경우 **상태** 는 **준비 안 됨** 이고 **메시지** 열에는 **데이터베이스 복제 완료**가 표시됩니다.  
  
    -   데이터베이스에 하나 이상의 활성 연결이 있는 경우는 **상태** 됩니다 **준비 안 됨** 하며 **메시지** 열에 표시 됩니다 _< number_of_active_connections >_ **활성 연결** -예를 들어: **1 활성 연결**이 표시됩니다. 데이터베이스를 분리하려면 먼저 **연결 삭제**를 선택하여 모든 활성 연결을 끊어야 합니다.  
  
     메시지에 대한 자세한 내용을 보려면 하이퍼링크로 연결된 텍스트를 클릭하여 작업 모니터를 엽니다.  
  
4.  데이터베이스를 분리할 준비가 되었으면 **확인**을 클릭합니다.  
  
> [!NOTE]  
>  새로 분리된 데이터베이스는 뷰를 새로 고칠 때까지 개체 탐색기의 **데이터베이스** 노드에 계속 표시됩니다. 언제 든 지 뷰를 새로 고칠 수 있습니다. 클릭 하 고 메뉴 모음에서 개체 탐색기 창에서 선택 **뷰** 차례로 **새로 고침**합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-detach-a-database"></a>데이터베이스를 분리하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 skipchecks가 true로 설정된 AdventureWorks2012 데이터베이스를 분리합니다.  
  
```  
EXEC sp_detach_db 'AdventureWorks2012', 'true';  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)   
 [sp_detach_db&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql)  
  
  
