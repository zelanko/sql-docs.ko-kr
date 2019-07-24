---
title: 투명 네트워크 IP 확인 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
author: MightyPen
ms.author: genemi
ms.openlocfilehash: df5b0233168c52b4f79cdc6d2d03cd7b72e16046
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008482"
---
# <a name="using-transparent-network-ip-resolution"></a>투명 네트워크 IP 확인 사용
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution은 Microsoft ODBC Driver 13.1 for SQL Server에서 사용 가능한 기존 MultiSubnetFailover 기능의 수정 버전으로, 호스트 이름에 대 한 첫 번째 확인 된 IP가 없는 경우 드라이버의 연결 시퀀스에 영향을 줍니다. 응답 하 고 호스트 이름과 연결 된 여러 개의 Ip가 있습니다. MultiSubnetFailover와 상호 작용 하 여 다음과 같은 세 가지 연결 시퀀스를 제공 합니다.

* 0: 하나의 IP가 시도 된 후 모든 ip가 병렬로 수행 됩니다.
* 1: 모든 Ip가 병렬로 시도 됨
* 2: 모든 Ip를 차례로 시도 합니다.

|TransparentNetworkIPResolution|MultiSubnetFailover|동작은|
|:-:|:-:|:-:|
|(기본값)|(기본값)|0|
|(기본값)|설정|1|
|(기본값)|사용 안 함|0|
|설정|(기본값)|0|
|설정|설정|1|
|설정|사용 안 함|0|
|사용 안 함|(기본값)|2|
|사용 안 함|설정|1|
|사용 안 함|사용 안 함|2|

연결 `TransparentNetworkIPResolution` 문자열 및 DSN 키워드는 연결 문자열 수준에서이 설정을 제어 합니다. 기본값은 사용입니다.

키워드|값|Default
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

`SQL_COPT_SS_TNIR` 사전 연결 특성을 사용 하면 응용 프로그램에서이 설정을 프로그래밍 방식으로 제어할 수 있습니다.

연결 특성|   크기/형식|  Default| 값| 설명
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` 또는 `SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|TNIR을 사용 하거나 사용 하지 않도록 설정 합니다.

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recoveryconnectodbclinux-macodbc-driver-on-linux-support-for-high-availability-disaster-recoverymd"></a>MultiSubnetFailover에 대 한 자세한 내용은 [Linux의 ODBC 드라이버 및 macOS-고가용성 및 재해 복구](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md) 를 참조 하세요.
--------------------------------------------------
## <a name="see-also"></a>참고 항목  
* [Windows의 Microsoft ODBC Driver for SQL Server](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [SQL Server 다중 서브넷 클러스터링(SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
