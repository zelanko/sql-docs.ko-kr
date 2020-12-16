---
title: '데이터베이스 엔진: 호환성이 손상되는 변경 | Microsoft Docs'
titleSuffix: SQL Server 2017
description: 이전 버전의 SQL Server에 기반을 둔 애플리케이션, 스크립트 또는 기능을 사용하지 못할 수 있는 변경 사항에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 07/22/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- breaking changes 2017 [SQL Server]
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017'
ms.openlocfilehash: bce39acebe2638016bed43219075a2d99c6efc60
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463674"
---
# <a name="breaking-changes-to-database-engine-features-in-sssqlv14-md"></a>[!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] 데이터베이스 엔진 기능의 주요 변경 사항
[!INCLUDE[SQL Server 2017](../includes/applies-to-version/sqlserver2017.md)]


  이 항목에서는 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]의 호환성이 손상되는 변경에 대해 설명합니다. 이러한 변경 내용에 따라 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 기반을 둔 애플리케이션, 스크립트 또는 기능을 사용하지 못할 수도 있습니다. 이러한 문제는 업그레이드할 때 발생할 수 있습니다.  
  
## <a name="breaking-changes-in-sssqlv14-md-ssde"></a>[!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]의 호환성이 손상되는 변경  
  
-  CLR은 더 이상 보안 경계로 지원되지 않는 .NET Framework의 CAS(코드 액세스 보안)를 사용합니다. [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)]부터 CLR 어셈블리의 보안을 강화하기 위해 `clr strict security`라는 `sp_configure` 옵션이 도입되었습니다. clr strict security는 기본적으로 사용되며 `SAFE` 및 `EXTERNAL_ACCESS` CLR 어셈블리가 `UNSAFE`로 표시된 것처럼 처리됩니다. `clr strict security` 옵션은 이전 버전과의 호환성을 위해 사용하지 않도록 설정할 수 있지만 권장하지는 않습니다. `clr strict security`를 사용하지 않도록 설정하면 `PERMISSION_SET = SAFE`로 만든 CLR 어셈블리에서 외부 시스템 리소스에 액세스하고, 비관리 코드를 호출하고, **sysadmin** 권한을 얻을 수 있습니다. strict security(엄격한 보안)를 사용하도록 설정하면 서명되지 않은 어셈블리는 로드되지 않습니다. 또한 데이터베이스에 `SAFE` 또는 `EXTERNAL_ACCESS` 어셈블리가 있으면 `RESTORE` 또는 `ATTACH DATABASE` 문을 완료할 수 있지만 어셈블리를 로드하지 못할 수 있습니다.   
  어셈블리를 로드하려면 서버에 대한 `UNSAFE ASSEMBLY` 권한이 있는 해당 로그인이 포함된 인증서 또는 비대칭 키로 서명되도록 각 어셈블리를 변경하거나 삭제한 다음 다시 만들어야 합니다. 자세한 내용은 [CLR strict security](../database-engine/configure-windows/clr-strict-security.md)를 참조하세요. 
  
-  [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]에서는 MD2, MD4, MD5, SHA 및 SHA1 알고리즘이 사용되지 않습니다. [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]까지는 자체 서명된 인증서가 SHA1을 사용하여 생성됩니다. [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]부터는 자체 서명된 인증서가 SHA2_256을 사용하여 생성됩니다.

## <a name="previous-versions"></a><a name="previous-versions"></a> 이전 버전  

- [SQL Server 2016 데이터베이스 엔진 기능의 주요 변경](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)

- [SQL Server 2014 데이터베이스 엔진 기능의 주요 변경](/previous-versions/sql/2014/database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016?view=sql-server-2014#SQL14)

#### <a name="archived-documentation-for-very-old-versions-of-sql-server"></a>이전 버전의 SQL Server에 대해 보관된 설명서

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>참고 항목  
 [SQL Server 2016 이후에는 지원되지 않는 데이터베이스 엔진 기능](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2016에서 지원되지 않는 데이터베이스 엔진 기능](./discontinued-database-engine-functionality-in-sql-server.md)   
 [SQL Server 데이터베이스 엔진의 이전 버전과의 호환성](./discontinued-database-engine-functionality-in-sql-server.md)   
 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
