---
title: Linux에서 SQL Server 복제 | Microsoft Docs
description: 이 문서에서는 Linux의 SQL Server 복제를 설명 합니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/20/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.workload: On Demand
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a6c4bad8947944d59208a0516e5950d36f64a84e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734131"
---
# <a name="sql-server-replication-on-linux"></a>Linux에서 SQL Server 복제

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 에 대 한 SQL Server 복제에서는 Linux의 SQL Server의 인스턴스.

SQL Server Management Studio (SSMS) 사용 하 여 Linux에서 복제 구성 [복제 저장 프로시저](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)합니다.

SQL Server 인스턴스의 모든 복제 역할에 참여할 수 있습니다.

* 게시자
* 배포자
* 구독자

복제 스키마를 혼합 하 고 운영 체제 플랫폼과 일치 수 있습니다. 예를 들어 복제 스키마 linux 게시자 및 배포자에 대 한에 SQL Server 인스턴스를 사용할 수 있으며 구독자는 Windows의 SQL Server의 인스턴스를 포함할 수 있습니다.

Linux의 SQL Server 인스턴스에서 모든 유형의 복제에 참여할 수 있습니다.

* 트랜잭션
* 병합
* 스냅숏

복제에 대 한 자세한 내용은 [SQL Server 복제 설명서](../relational-databases/replication/sql-server-replication.md)합니다.

## <a name="supported-features"></a>지원되는 기능

에 대 한 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 다음 복제 기능이 지원 됩니다.

* 스냅숏 복제
* 트랜잭션 복제
* 병합 복제
* 피어 투 피어 복제
* 기본이 아닌 포트를 사용 하 여 복제 <!--Add link to explanation-->
* AD 인증을 사용 하 여 복제
* Windows 및 Linux에서 복제 구성
* 트랜잭션 복제에 대 한 즉시 업데이트

## <a name="limitations"></a>제한 사항

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 다음과 같은 기능을 지원 하지 않습니다.

* 즉시 업데이트 구독자

## <a name="next-steps"></a>다음 단계

[Linux에서 SQL Server 복제 구성](sql-server-linux-replication-tutorial-tsql.md)

[샘플: Linux에서 SQL Server 복제 구성](sql-server-linux-replication-configure.md)
