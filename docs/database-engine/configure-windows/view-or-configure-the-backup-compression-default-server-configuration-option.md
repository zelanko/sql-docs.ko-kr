---
title: backup compression default 서버 구성 옵션 보기 또는 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], backup compression default option
- backup compression [SQL Server], backup compression default Option
ms.assetid: 23029395-3e93-4c29-b7d6-e5a47a3526ff
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 7670b7f7ac2d80f596c3a192eb23fbf2b9e94a6d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66775113"
---
# <a name="view-or-configure-the-backup-compression-default-server-configuration-option"></a>backup compression default 서버 구성 옵션 보기 또는 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 백업 압축 기본값 [!INCLUDE[tsql](../../includes/tsql-md.md)]서버 구성 옵션을 보거나 구성하는 방법에 대해 설명합니다. **백업 압축 기본값** 옵션은 서버 인스턴스가 기본적으로 압축된 백업을 만드는지 여부를 결정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이(가) 설치되면 **백업 압축 기본값** 옵션이 해제됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **백업 압축 기본값 옵션을 보거나 구성하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [백업 압축 기본값 옵션을 구성한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서는 백업 압축을 사용할 수 없습니다. 자세한 내용은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
-   기본적으로 압축하면 CPU 사용량이 크게 늘어나고 압축 프로세스로 사용되는 추가 CPU는 동시 작업에 악영향을 줄 수 있습니다. 따라서 CPU 사용량이 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)에 의해 제한되는 세션에서 우선 순위가 낮은 압축 백업을 만들 수 있습니다. 자세한 내용은 이 항목 뒷부분의 [Resource GovernoR을 사용하여 백업 압축을 통해 CPU 사용량 제한&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)에 의해 제한되는 세션에서 우선 순위가 낮은 압축 백업을 만들 수 있습니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   개별 백업을 만들거나 로그 전달을 구성하거나 유지 관리 계획을 만들 때 서버 수준 기본값을 재정의할 수 있습니다.  
  
-   백업 압축은 디스크 백업 디바이스와 테이프 백업 디바이스 모두에서 지원됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-or-configure-the-backup-compression-default-option"></a>백업 압축 기본값 옵션을 보거나 구성하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **데이터베이스 설정** 노드를 클릭합니다.  
  
3.  **백업 및 복원**아래의 **백업 압축** 에 **백업 압축 기본값** 옵션의 현재 설정이 표시됩니다. 이 설정은 다음과 같이 백업 압축의 서버 수준 기본값을 결정합니다.  
  
    -   **백업 압축** 상자가 비어 있으면 새 백업은 기본적으로 압축되지 않습니다.  
  
    -   **백업 압축** 상자가 선택되어 있으면 새 백업은 기본적으로 압축됩니다.  
  
     **sysadmin** 또는 **serveradmin** 고정 서버 역할의 멤버인 경우 **백업 압축** 상자를 클릭하여 기본 설정을 변경할 수도 있습니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-the-backup-compression-default-option"></a>백업 압축 기본값 옵션을 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예에서는 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 카탈로그 뷰를 쿼리하여 `backup compression default`의 값을 결정합니다. 값이 0이면 백업 압축이 사용되지 않고, 값이 1이면 백업 압축이 사용됩니다.  
  
```sql  
SELECT value   
FROM sys.configurations   
WHERE name = 'backup compression default' ;  
GO  
```  
  
#### <a name="to-configure-the-backup-compression-default-option"></a>백업 압축 기본값 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예제에서는 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 를 사용하여 기본적으로 압축된 백업을 만들도록 서버 인스턴스를 구성하는 방법을 보여 줍니다.  
  
```sql  
EXEC sp_configure 'backup compression default', 1 ;  
RECONFIGURE;  
GO 
```  
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)서버 구성 옵션을 보거나 구성하는 방법에 대해 설명합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 백업 압축 기본값 옵션을 구성한 후  
 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)  
  
  

