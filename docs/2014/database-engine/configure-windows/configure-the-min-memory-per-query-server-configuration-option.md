---
title: min memory per query 서버 구성 옵션 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- memory [SQL Server], queries
- minimum query memory
- queries [SQL Server], memory
- min memory per query option
ms.assetid: ecd3fb79-b4a6-432f-9ef5-530e0d42d5a6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: dfee7265529419aecf2b05831503ed134b93f525
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62787061"
---
# <a name="configure-the-min-memory-per-query-server-configuration-option"></a>min memory per query 서버 구성 옵션 구성
  이 `min memory per query` 항목에서는 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용 하 여에서 서버 구성 옵션을 구성 하는 방법에 대해 설명 합니다. 옵션 `min memory per query` 은 쿼리 실행을 위해 할당 되는 최소 메모리 양 (kb)을 지정 합니다. 예를 들어를 `min memory per query` 2048 KB로 설정 하면 쿼리는 최소한 총 메모리를 얻을 수 있도록 보장 됩니다. 기본값은 1,024KB입니다. 최소값은 512KB이고 최대값은 2,147,483,647KB(2GB)입니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **쿼리당 최소 메모리 옵션을 구성하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [쿼리당 최소 메모리 옵션을 구성한 후](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   쿼리당 min memory의 양은 [인덱스 생성 메모리 옵션](configure-the-index-create-memory-server-configuration-option.md)보다 우선 합니다. 두 옵션을 변경할 때 인덱스 생성 메모리가 쿼리당 최소 메모리보다 적은 경우 경고 메시지가 나타나지만 값은 설정됩니다. 쿼리 실행 중에도 비슷한 경고 메시지가 나타납니다.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   이 옵션은 고급 옵션으로, 숙련된 데이터베이스 관리자나 공인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술 지원 담당자만 변경해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 프로세서는 쿼리에 할당할 최적의 메모리 양을 결정하려고 합니다. min memory per query 옵션을 사용하면 관리자가 단일 쿼리에서 수신할 최소 메모리 양을 지정할 수 있습니다. 일반적으로 많은 양의 데이터에 대해 해시 및 정렬 작업을 수행하는 경우에는 쿼리가 이보다 더 많은 메모리를 수신합니다. min memory per query 값을 늘리면 크기가 작거나 중간인 일부 쿼리의 성능은 개선되지만 메모리 리소스에 대한 경합은 증가합니다. min memory per query 옵션은 정렬에 할당된 메모리를 포함합니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>쿼리당 최소 메모리 옵션을 구성하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **메모리** 노드를 클릭합니다.  
  
3.  **쿼리당 최소 메모리** 입력란에 쿼리 실행을 위해 할당할 최소 메모리 용량(KB)을 입력합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>쿼리당 최소 메모리 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예에서는 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 를 사용하여 `min memory per query` 옵션 값을 `3500` KB로 설정하는 방법을 보여 줍니다.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'min memory per query', 3500 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
##  <a name="follow-up-after-you-configure-the-min-memory-per-query-option"></a><a name="FollowUp"></a> 후속 작업: 쿼리당 최소 메모리 옵션을 구성한 후  
 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [index create memory 서버 구성 옵션 구성](configure-the-index-create-memory-server-configuration-option.md)  
  
  
