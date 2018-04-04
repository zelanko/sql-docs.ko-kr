---
title: Microsoft Drivers for PHP for SQL Server 지원 매트릭스 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
caps.latest.revision: ''
author: David-Engel
ms.author: v-daveng
manager: ''
ms.workload: On Demand
ms.openlocfilehash: 23159425e45fdc8974e0047859072654c5c77959
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>SQL Server 지원 매트릭스 용 Microsoft PHP 드라이버
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  이 페이지는 SQL Server 용 Microsoft PHP 드라이버에 대 한 지원 매트릭스 및 지원 기간 정책을 포함합니다.

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Microsoft PHP 드라이버 지원 수명 주기 매트릭스 및 정책
 MSL(Microsoft 지원 수명 주기) 정책은 Microsoft 제품 지원 수명 주기와 관련해서 투명하고 예측 가능한 정보를 제공합니다. PHP 드라이버 버전 3.x에서 4.x 및 5.x 요소로 드라이버 릴리스 날짜 로부터 5 년을 포함 합니다. 일반 지원에 정의 되는 [Microsoft 지원 수명 주기 웹 사이트](https://support.microsoft.com/lifecycle)합니다.

 확장 및 사용자 지정 지원 옵션은 Microsoft PHP 드라이버에 사용할 수 없습니다.

 다음 Microsoft PHP Driver는 지정 된 지원 종료 날짜까지 지원 됩니다.

|드라이버 이름|드라이버 패키지 버전|기본 지원의 끝|
|-|-|-|
|SQL Server 용 Microsoft PHP 드라이버 5.2|5.2|2023 년 2 월 9,|
|SQL Server 용 Microsoft PHP 드라이버 4.3|4.3|2022 년 7 월 6|
|SQL Server 용 Microsoft PHP 드라이버 4.0|4.0|2021 년 7 월 11|
|SQL Server 용 Microsoft PHP 드라이버 3.2|3.2|2020 년 3 월 9,|
|SQL Server 용 Microsoft PHP 드라이버 3.1|3.1|2019년 12월 12일|

 다음 Microsoft PHP Driver 이상 지원 되지 않습니다.

|드라이버 이름|드라이버 패키지 버전|기본 지원의 끝|
|-|-|-|
|SQL Server 용 Microsoft PHP 드라이버 3.0|3.0|2017년 3월 6일|
|SQL Server 용 Microsoft PHP 드라이버 2.0|2.0|2015 년 8 월 10 일|
|SQL Server 용 Microsoft PHP 드라이버 1.0|1.0|2014 년 4 월 28 일|

## <a name="sql-server-version-certified-compatibility"></a>호환성을 인증 하는 SQL Server 버전
 다음 표에서 테스트 되 고 해당 드라이버 버전 호환으로 인증 하는 SQL Server 버전을 나열 합니다. 이전 버전과 호환성 이전 드라이버 버전을 유지 하기 위해 노력 있지만 최신 지원된 드라이버만 테스트 하 고 SQL Server 릴리스될 때마다 새로운 SQL Server 버전으로 인증 합니다.

|PHP for SQL Server 드라이버 버전&#8594;<br />&#8595;SQL Server 버전|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|관리 되는 azure SQL 인스턴스<br/> (확장 비공개 미리 보기)|Y|Y| | | | | |
|Azure SQL 데이터 웨어하우스|Y|Y| | | | | |
|SQL Server 2017   |Y|Y| | | | | |
|SQL Server 2016   |Y|Y|Y| | | | |
|SQL Server 2014   |Y|Y|Y|Y|Y| | |
|SQL Server 2012   |Y|Y|Y|Y|Y|Y| |
|SQL Server 2008 R2|Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008   | | |Y|Y|Y|Y|Y|

## <a name="php-version-support"></a>PHP 버전 지원
 다음 버전의 PHP 나열 된 버전의 Microsoft PHP 드라이버 지원 됩니다.

|PHP for SQL Server 드라이버 버전&#8594;<br />&#8595;PHP 버전|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|7.2|Windows에서 7.2.1+<br/>다른 플랫폼에서 7.2.0+| | | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |        |        |
|5.6|       |       |       |5.6.4+  |        |        |        |
|5.5|       |       |       |5.5.16+ |5.5.16+ |        |        |
|5.4|       |       |       |5.4.32  |5.4.32  |5.4.32  |        |
|5.3|       |       |       |        |        |5.3.0   |5.3.0   |
|5.2|       |       |       |        |        |        |5.2.4<br />5.2.13|

## <a name="supported-operating-systems"></a>지원되는 운영 체제
 다음 Windows 운영 체제 버전은 나열 된 버전의 Microsoft PHP 드라이버 지원 됩니다.

|PHP for SQL Server 드라이버 버전&#8594;<br />&#8595;운영 체제|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Windows Server 2016                 |Y  |Y  |   |   |   |   |   |
|Windows Server 2012 R2              |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows Server 2012                 |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows Server 2008 R2 SP1          |   |   |Y  |Y  |Y  |Y  |   |
|Windows Server 2008 R2              |   |   |   |   |   |   |Y  |
|Windows Server 2008 SP2             |   |   |Y  |Y  |Y  |Y  |   |
|Windows Server 2008                 |   |   |   |   |   |   |Y  |
|Windows Server 2003 SP1             |   |   |   |   |   |   |Y  |
|Windows 10                          |Y  |Y  |Y  |   |   |   |   |
|Windows 8.1                         |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows 8                           |   |Y  |Y  |Y  |Y  |   |   |
|Windows 7 SP1                       |   |   |Y  |Y  |Y  |Y  |   |
|Windows Vista SP2                   |   |   |Y  |Y  |Y  |Y  |Y  |
|Windows XP SP3                      |   |   |   |   |   |   |Y  |

 나열 된 버전의 Microsoft PHP 드라이버를 사용 하는 다음 Linux 및 Mac 운영 체제 버전 (64 비트 전용)가 지원 됩니다.

|PHP for SQL Server 드라이버 버전&#8594;<br />&#8595;운영 체제|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Ubuntu 17.10 (64 비트)               |Y  |   |   |   |   |   |   |
|Ubuntu 16.04 (64 비트)               |Y  |Y  |Y  |   |   |   |   |
|Ubuntu 15.10 (64 비트)               |   |Y  |   |   |   |   |   |
|Ubuntu 15.04 (64 비트)               |   |   |Y  |   |   |   |   |
|Debian 9 (64 비트)                   |Y  |   |   |   |   |   |   |
|Debian 8 (64 비트)                   |Y  |Y  |   |   |   |   |   |
|Red Hat Enterprise Linux 7 (64 비트) |Y  |Y  |Y  |   |   |   |   |
|엔터프라이즈 Suse Linux (64 비트) 12   |Y  |   |   |   |   |   |   |
|macOS 시에라 (64 비트)               |Y  |Y  |   |   |   |   |   |
|macOS El Capitan (64 비트)           |Y  |Y  |   |   |   |   |   |

## <a name="see-also"></a>관련 항목:  
[릴리스 정보](../../connect/php/release-notes-for-the-php-sql-driver.md)

[지원 리소스](../../connect/php/support-resources-for-the-php-sql-driver.md)

[시스템 요구 사항](../../connect/php/system-requirements-for-the-php-sql-driver.md)
