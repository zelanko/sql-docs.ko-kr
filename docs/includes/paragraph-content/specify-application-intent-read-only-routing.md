---
title: 파일 포함
description: 파일 포함
services: sql-database
author: MightyPen
ms.service: sql-database
ms.topic: include
ms.date: 04/05/2018
ms.author: genemi
ms.custom: include file
ms.openlocfilehash: 0e7d549c2f3b02349007815019cc47647f172f73
ms.sourcegitcommit: 87f29b23d5ab174248dab5d558830eeca2a6a0a4
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51019068"
---
## <a name="specifying-application-intent"></a>응용 프로그램 의도 지정

키워드 **ApplicationIntent** 연결 문자열에 지정할 수 있습니다. 할당 가능한 값은 **ReadWrite** 하거나 **ReadOnly**합니다. 기본값은 **ReadWrite**합니다.

**ApplicationIntent=ReadOnly**이면 클라이언트는 연결할 때 읽기 워크로드를 요청합니다. 서버 연결 시 및 시 의도 적용 한 **사용 하 여** 문을 데이터베이스.

**ApplicationIntent** 키워드는 레거시 읽기 전용 데이터베이스에 적용되지 않습니다.  


#### <a name="targets-of-readonly"></a>읽기 전용의 대상

연결이 **ReadOnly**를 선택하면 데이터베이스에 대해 존재할 수 있는 다음 특수 구성 중 하나에 연결이 할당됩니다.

- [Always On](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
    - 데이터베이스는 대상 Always On 데이터베이스에 대한 읽기 워크로드를 허용하거나 허용하지 않을 수 있습니다. 이 선택을 사용 하 여 제어 됩니다는 **ALLOW_CONNECTIONS** 절을 **PRIMARY_ROLE** 및 **SECONDARY_ROLE** Transact SQL 문입니다.

- [지역에서 복제](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)

- [읽기 확장](https://docs.microsoft.com/azure/sql-database/sql-database-read-scale-out)

사용 가능한 경우 이러한 특수 대상이 하나도 일반 데이터베이스에서 읽습니다.

&nbsp;

합니다 **ApplicationIntent** 키워드를 사용 하면 *읽기 전용 라우팅을*합니다.


## <a name="read-only-routing"></a>읽기 전용 라우팅

읽기 전용 라우팅은 데이터베이스의 읽기 전용 복제 가용성을 보장할 수 있는 기능입니다. 다음의 모든 적용을 읽기 전용 라우팅을 사용 하려면:

- AlwaysOn 가용성 그룹의 가용성 그룹 수신기에 연결해야 합니다.

- **ApplicationIntent** 연결 문자열 키워드는 **ReadOnly**로 설정해야 합니다.

- 읽기 전용 라우팅을 설정하려면 데이터베이스 관리자가 가용성 그룹을 구성해야 합니다.

각 연결이 여러 개를 사용 하 여 읽기 전용 라우팅을 일부만 동일한 읽기 전용 복제본에 연결할 수 있습니다. 데이터베이스 동기화를 변경하거나 서버 라우팅 구성을 변경하면 클라이언트를 다른 읽기 전용 복사본에 연결할 수 있습니다. 모든 읽기 전용 요청이 동일한 읽기 전용 복제본에 연결할 수 있는지 확인할 수 있습니다. 확인 하 여이 동일성 *되지* 가용성 그룹 수신기에 전달 합니다 **서버** 연결 문자열 키워드. 대신, 읽기 전용 인스턴스의 이름을 지정합니다.

읽기 전용 라우팅을 주 복제본에 연결할 때 보다 더 오래 걸릴 수 있습니다. 대기 시간이 긴 이유는 읽기 전용 라우팅은 먼저 주 복제본에 연결한 다음, 가장 잘 읽을 수 있는 보조 복제본을 찾기 때문입니다. 이러한 여러 staps 인해 30 초 이상 로그인 시간 제한을 늘려야 합니다.

