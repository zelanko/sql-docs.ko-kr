---
title: 트랜잭션 격리 수준 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], hints
- isolation levels [SQL Server], metadata access
- hints [SQL Server], locking
ms.assetid: 02bb71fa-1e92-4782-a9cf-6e256cc1f3ea
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1634e8bbb524744e637d1b9d0b5f7ef213ca62f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65981401"
---
# <a name="transaction-isolation-levels"></a>트랜잭션 격리 수준
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 카탈로그 뷰, 호환성 뷰, 정보 스키마 뷰, 메타데이터 내보내기 기본 제공 함수를 통해 메타데이터에 액세스하는 쿼리의 잠금 힌트를 인식하지 못할 수도 있습니다.  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 내부에서는 메타데이터 액세스에 대해 READ COMMITTED 격리 수준만 인식합니다. 트랜잭션에 SERIALIZABLE과 같은 격리 수준이 있고 트랜잭션 내에서 카탈로그 뷰 또는 메타데이터 내보내기 기본 제공 함수를 사용한 메타데이터 액세스 시도가 이루어질 경우 해당 쿼리는 READ COMMITTED로 완료될 때까지 실행됩니다. 그러나 스냅샷 격리 상태에서는 동시 DDL 작업으로 인해 메타데이터 액세스가 실패할 수도 있습니다. 이 문제는 메타데이터의 버전이 관리되지 않기 때문에 발생합니다. 따라서 스냅샷 격리 상태에서는 다음 항목에 액세스하는 데 실패할 수도 있습니다.  
  
-   카탈로그 뷰  
  
-   호환성 뷰  
  
-   정보 스키마 뷰  
  
-   메타데이터 내보내기 기본 제공 함수  
  
-   저장 프로시저의 **sp_help** 그룹  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 카탈로그 프로시저  
  
-   동적 관리 뷰 및 함수  
  
 격리 수준에 대한 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조하세요.  
  
 다음 표에서는 다양한 격리 수준에서의 메타데이터 액세스에 대해 간략하게 보여 줍니다.  
  
|격리 수준|지원됨|보장됨|  
|---------------------|---------------|-------------|  
|READ UNCOMMITTED|아니오|보장되지 않음|  
|READ COMMITTED|예|예|  
|REPEATABLE READ|아니오|아니오|  
|SNAPSHOT ISOLATION|아니오|아니오|  
|SERIALIZABLE|아니오|아니오|  
  
  
