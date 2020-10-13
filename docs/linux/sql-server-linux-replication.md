---
title: Linux의 SQL Server 복제
description: SQL Server 2017(14.x)(CU18) 이상에서 SQL Server on Linux 인스턴스에 대해 SQL Server 복제를 지원하는 방법을 알아봅니다.
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 12/09/2019
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 7faa2b0101ee1f54484fce2a0756812a4ad611e1
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91785017"
---
# <a name="sql-server-replication-on-linux"></a>Linux의 SQL Server 복제

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

[!INCLUDE[SQL Server 2017](../includes/sssqlv14-md.md)]([CU18](https://support.microsoft.com/help/4527377)) 이상에서는 SQL Server on Linux 인스턴스의 SQL Server 복제를 지원합니다.

SSMS(SQL Server Management Studio) [복제 저장 프로시저](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)를 사용하여 Linux에서 복제를 구성합니다.

SQL Server의 인스턴스는 모든 복제 역할에 참여할 수 있습니다.

* 게시자
* 배포자
* 가입자

복제 스키마는 운영 체제 플랫폼과 적절히 조합할 수 있습니다. 예를 들어 복제 스키마에는 게시자 및 배포자에 대한 SQL Server on Linux 인스턴스가 포함될 수 있으며, 구독자에는 Windows 및 Linux의 SQL Server 인스턴스가 포함됩니다.

Linux의 SQL Server 인스턴스는 모든 유형의 복제에 참여할 수 있습니다.

* 트랜잭션
* 스냅샷

복제에 대한 자세한 내용은 [SQL Server 복제 설명서](../relational-databases/replication/sql-server-replication.md)를 참조하세요.

## <a name="supported-features"></a>지원되는 기능

다음 복제 기능이 지원됩니다.

* 스냅샷 복제
* 트랜잭션 복제
* 기본 포트가 아닌 포트를 사용하는 복제 <!--Add link to explanation-->
* AD 인증을 사용하는 복제
* Windows 및 Linux에서 복제 구성
* 트랜잭션 복제에 대한 즉시 업데이트

## <a name="limitations"></a>제한 사항

다음 기능은 지원되지 않습니다.

* 병합 복제
* 피어 투 피어 복제
* Oracle 게시

## <a name="next-steps"></a>다음 단계

[Linux에서 SQL Server 복제 구성](sql-server-linux-replication-tutorial-tsql.md)

[샘플: Linux에서 SQL Server 복제 구성](sql-server-linux-replication-configure.md)
