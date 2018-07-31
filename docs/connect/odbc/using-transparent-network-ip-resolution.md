---
title: 투명 네트워크 IP 확인을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d76e50b4761e8d1a32bbcfc4606778f96513ed1
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38060230"
---
# <a name="using-transparent-network-ip-resolution"></a>투명 네트워크 IP 확인 사용
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution은 않습니다 호스트 이름의 첫 번째 확인 된 IP의 경우 드라이버의 연결 순서에 영향을 주는 SQL Server 용 Microsoft ODBC Driver 13.1에서 사용할 수 있는 기존 MultiSubnetFailover 기능 수정 버전 응답 되며 호스트와 연결 된 여러 Ip입니다. 다음 세 가지 연결 시퀀스를 제공 하는 MultiSubnetFailover와 상호 작용 합니다.

* 0: IP를 시도 하나 뒤에 동시에 모든 Ip
* 1: 동시에 모든 Ip는 시도
* 2: 모든 Ip 시도 한 번에 하나씩

|TransparentNetworkIPResolution|MultiSubnetFailover|동작|
|:-:|:-:|:-:|
|(기본값)|(기본값)|0|
|(기본값)|설정|@shouldalert|
|(기본값)|사용 안 함|0|
|설정|(기본값)|0|
|설정|설정|@shouldalert|
|설정|사용 안 함|0|
|사용 안 함|(기본값)|2|
|사용 안 함|설정|@shouldalert|
|사용 안 함|사용 안 함|2|

`TransparentNetworkIPResolution` DSN 및 연결 문자열 키워드에는 연결 문자열 수준에서이 설정을 제어 합니다. 기본값을 사용 합니다.

키워드|값|Default
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

`SQL_COPT_SS_TNIR` 사전 연결 특성을 사용 하면이 설정을 프로그래밍 방식으로 제어 하는 응용 프로그램:

연결 특성|   크기/유형|  Default| 값| 설명
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` 또는 `SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|사용 하거나 TNIR를 사용 하지 않도록 설정 합니다.

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recoveryconnectodbclinux-macodbc-driver-on-linux-support-for-high-availability-disaster-recoverymd"></a>MultiSubnetFailover에 대 한 자세한 내용은 참조 하세요. [Linux 및 macOS-고가용성 및 재해 복구에 대 한 ODBC 드라이버](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
--------------------------------------------------
## <a name="see-also"></a>참고 항목  
* [Windows의 Microsoft ODBC Driver for SQL Server](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [SQL Server 다중 서브넷 클러스터링(SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
