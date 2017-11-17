---
title: "트랜잭션 격리 수준 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], hints
- isolation levels [SQL Server], metadata access
- hints [SQL Server], locking
ms.assetid: 02bb71fa-1e92-4782-a9cf-6e256cc1f3ea
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0acd70fad20d0ad1c2727f93da52b2e938ee21fd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="transaction-isolation-levels"></a>트랜잭션 격리 수준
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 카탈로그 뷰, 호환성 뷰, 정보 스키마 뷰, 메타데이터 내보내기 기본 제공 함수를 통해 메타데이터에 액세스하는 쿼리의 잠금 힌트를 인식하지 못할 수도 있습니다.  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 내부에서는 메타데이터 액세스에 대해 READ COMMITTED 격리 수준만 인식합니다. 트랜잭션에 SERIALIZABLE과 같은 격리 수준이 있고 트랜잭션 내에서 카탈로그 뷰 또는 메타데이터 내보내기 기본 제공 함수를 사용한 메타데이터 액세스 시도가 이루어질 경우 해당 쿼리는 READ COMMITTED로 완료될 때까지 실행됩니다. 그러나 스냅숏 격리 상태에서는 동시 DDL 작업으로 인해 메타데이터 액세스가 실패할 수도 있습니다. 이 문제는 메타데이터의 버전이 관리되지 않기 때문에 발생합니다. 따라서 스냅숏 격리 상태에서는 다음 항목에 액세스하는 데 실패할 수도 있습니다.  
  
-   카탈로그 뷰  
  
-   호환성 뷰  
  
-   정보 스키마 뷰  
  
-   메타데이터 내보내기 기본 제공 함수  
  
-   **sp_help** 저장된 프로시저 그룹  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 카탈로그 프로시저  
  
-   동적 관리 뷰 및 함수  
  
 격리 수준에 대 한 자세한 내용은 참조 [SET TRANSACTION ISOLATION LEVEL &#40; Transact SQL &#41; ](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
 다음 표에서는 다양한 격리 수준에서의 메타데이터 액세스에 대해 간략하게 보여 줍니다.  
  
|격리 수준|지원됨|보장됨|  
|---------------------|---------------|-------------|  
|READ UNCOMMITTED|아니요|보장되지 않음|  
|READ COMMITTED|예|예|  
|REPEATABLE READ|아니요|아니요|  
|SNAPSHOT ISOLATION|아니요|아니요|  
|SERIALIZABLE|아니요|아니요|  
  
  

