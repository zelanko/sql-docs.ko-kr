---
title: 투명 네트워크 IP 확인 사용
description: ODBC Driver for SQL Server의 투명 네트워크 IP 확인과 MultiSubnetFailover 기능에 미치는 영향에 대해 알아봅니다.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 12a8a151902bd4f191fbc79f165f936e991a0226
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245002"
---
# <a name="using-transparent-network-ip-resolution-with-the-odbc-driver"></a>ODBC 드라이버에서 투명 네트워크 IP 확인 사용
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution은 호스트 이름의 첫 번째 확인된 IP가 응답하지 않고 해당 호스트 이름과 연결된 복수의 IP가 있는 경우에 드라이버의 연결 순서에 영향을 미치는 기존 MultiSubnetFailover 기능(Microsoft ODBC Driver 13.1 for SQL Server에서 사용 가능)의 개정판입니다. 이 기능은 MultiSubnetFailover와 상호 작용하여 다음과 같은 세 가지 연결 시퀀스를 제공합니다.

* 0: 하나의 IP가 시도된 후 모든 IP가 병렬로 실행됨
* 1: 모든 IP가 병렬로 시도됨
* 2: 모든 IP가 차례대로 하나씩 시도됨

|TransparentNetworkIPResolution|MultiSubnetFailover|동작|
|:-:|:-:|:-:|
|(기본값)|(기본값)|0|
|(기본값)|사용|1|
|(기본값)|사용 안 함|0|
|사용|(기본값)|0|
|사용|사용|1|
|사용|사용 안 함|0|
|사용 안 함|(기본값)|2|
|사용 안 함|사용|1|
|사용 안 함|사용 안 함|2|

`TransparentNetworkIPResolution` 연결 문자열 및 DSN 키워드는 연결 문자열 수준에서 이 설정을 제어합니다. 기본값을 사용합니다.

키워드|값|기본값
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

`SQL_COPT_SS_TNIR` 사전 연결 특성을 사용하면 애플리케이션에서 이 설정을 프로그래밍 방식으로 제어할 수 있습니다.

연결 특성|   크기/형식|  기본값| 값| Description
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` 또는 `SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|TNIR을 사용 또는 사용 안 함으로 설정합니다.

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recovery"></a>MultiSubnetFailover에 대한 자세한 내용은 [Linux 및 macOS의 ODBC 드라이버 - 고가용성 및 재해 복구](linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)를 참조하세요.
--------------------------------------------------
## <a name="see-also"></a>참고 항목  
* [Windows의 Microsoft ODBC Driver for SQL Server](windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [SQL Server 다중 서브넷 클러스터링(SQL Server)](../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)
