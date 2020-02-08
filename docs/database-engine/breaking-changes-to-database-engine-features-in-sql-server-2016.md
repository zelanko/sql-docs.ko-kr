---
title: '데이터베이스 엔진: 호환성이 손상되는 변경 | Microsoft Docs'
titleSuffix: SQL Server 2016
description: SQL Server 2016 데이터베이스 엔진 기능의 호환성이 손상되는 변경
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], what's new
- breaking changes [SQL Server]
ms.assetid: 47edefbd-a09b-4087-937a-453cd5c6e061
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 67a37dd07810facf3e18e94dc0f9e552ea05778a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75244717"
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2016"></a>SQL Server 2016 데이터베이스 엔진 기능의 호환성이 손상되는 변경

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 및 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 대한 호환성이 손상되는 변경에 대해 설명합니다. 이러한 변경 내용에 따라 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 기반을 둔 애플리케이션, 스크립트 또는 기능을 사용하지 못할 수도 있습니다. 이러한 문제는 업그레이드할 때 발생할 수 있습니다.  
  
##  <a name="SQL15"></a>[!INCLUDE[ssSQL15](../includes/sssql15-md.md)]의 주요 변경 내용  
  
-   `sys.dm_io_virtual_file_stats`의 *sample_ms* 열은 **int**에서 **bigint** 데이터 형식으로 확장되었습니다.  
  
-   `sys.fn_virtualfilestats`의 *TimeStamp* 열은 **int**에서 **bigint** 데이터 형식으로 확장되었습니다.  

-   데이터베이스 호환성 수준 130에서 **datetime** 과 **datetime2** 데이터 형식 간 암시적 변환은 밀리초의 소수 부분을 고려하여 정확도가 향상되므로 다르게 변환된 값을 생성합니다. datetime과 datetime2 데이터 형식이 혼합된 비교 시나리오가 있을 때마다 datetime2 데이터 형식으로 명시적 캐스트를 사용합니다. 자세한 내용은 이 [Microsoft 지원 문서](https://support.microsoft.com/help/4010261)를 참조하세요.

-   데이터베이스 호환성 수준이 130 미만이면 특정 숫자 및 날짜/시간 데이터 형식 간에 암시적 변환을 수행하는 작업은 정확도가 향상되므로 다르게 변환된 값이 생성될 수 있습니다. 여기에는 `DATEDIFF` 및 `ROUND`와 같은 계산이 필요한 함수 사용이 포함됩니다. 자세한 내용은 이 [Microsoft 지원 문서](https://support.microsoft.com/help/4010261)를 참조하세요.

## <a name="previous-versions"></a> 이전 버전  

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 및 일부 이전 버전의 호환성이 손상되는 변경에 대한 자세한 내용은 [SQL Server 2014 데이터베이스 엔진 기능의 호환성이 손상되는 변경](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md?view=sql-server-2014)을 참조하세요.

#### <a name="archived-documentation-for-very-old-versions-of-sql-server"></a>이전 버전의 SQL Server에 대해 보관된 설명서

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>참고 항목  
 [SQL Server 2016 이후에는 지원되지 않는 데이터베이스 엔진 기능](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2016에서 지원되지 않는 데이터베이스 엔진 기능](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [SQL Server 데이터베이스 엔진의 이전 버전과의 호환성](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [일부 데이터 형식 및 일반적이지 않은 작업 처리 시 Windows의 SQL Server 2016 또는 SQL Server 2017 향상된 기능](https://support.microsoft.com/help/4010261)   
