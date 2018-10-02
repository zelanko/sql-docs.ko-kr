---
title: SQL Server 2016 데이터베이스 엔진 기능의 주요 변경 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], what's new
- breaking changes [SQL Server]
ms.assetid: 47edefbd-a09b-4087-937a-453cd5c6e061
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7cbd8baa507b681f32d2cd123f029b530fd4d100
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47788491"
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2016"></a>SQL Server 2016 데이터베이스 엔진 기능의 주요 변경
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] 및 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 대한 주요 변경 내용에 대해 설명합니다. 이러한 변경 내용에 따라 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 기반을 둔 응용 프로그램, 스크립트 또는 기능을 사용하지 못할 수도 있습니다. 이러한 문제는 업그레이드할 때 발생할 수 있습니다.  
  
##  <a name="SQL15"></a> [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]의 주요 변경 내용  
  
-   sys.dm_io_virtual_file_stats의 sample_ms 열은 **int** 에서 **bigint** 데이터 형식으로 확장되었습니다.  
  
-   sys.fn_virtualfilestats의 TimeStamp 열은 **int** 에서 **bigint** 데이터 형식으로 확장되었습니다.  

-   MD2, MD4, MD5, SHA 또는 SHA1 해시 알고리즘을 사용하는 경우(권장되지 않음) 데이터베이스 호환성 수준을 130 이전으로 설정해야 합니다.  

-   데이터베이스 호환성 수준 130에서 **datetime** 과 **datetime2** 데이터 형식 간 암시적 변환은 밀리초의 소수 부분을 고려하여 정확도가 향상되므로 다르게 변환된 값을 생성합니다. datetime과 datetime2 데이터 형식이 혼합된 비교 시나리오가 있을 때마다 datetime2 데이터 형식으로 명시적 캐스트를 사용합니다. 자세한 내용은 이 [Microsoft 지원 문서](http://support.microsoft.com/help/4010261)를 참조하세요.
  
## <a name="previous-versions"></a>이전 버전  
  
-   [SQL Server 2014 데이터베이스 엔진 기능의 주요 변경](breaking-changes-to-database-engine-features-in-sql-server-2016.md))  
  
-   [SQL Server 2012 데이터베이스 엔진 기능의 주요 변경](breaking-changes-to-database-engine-features-in-sql-server-2016.md))  
  
-   [SQL Server 2008 데이터베이스 엔진 기능의 주요 변경](breaking-changes-to-database-engine-features-in-sql-server-2016.md))  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2016 이후에는 지원되지 않는 데이터베이스 엔진 기능](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2016에서 지원되지 않는 데이터베이스 엔진 기능](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [SQL Server 데이터베이스 엔진의 이전 버전과의 호환성](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [일부 데이터 형식 및 일반적이지 않은 작업 처리 시 Windows의 SQL Server 2016 또는 SQL Server 2017 향상된 기능](http://support.microsoft.com/help/4010261)
  
  
