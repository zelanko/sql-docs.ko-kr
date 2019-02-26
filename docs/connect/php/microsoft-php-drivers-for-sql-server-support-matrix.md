---
title: Microsoft Drivers for PHP for SQL Server 지원 매트릭스 | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: ''
ms.openlocfilehash: ec5a151d79d9a66bfd65342336ad7aa3afcf567d
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744403"
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>SQL Server Support Matrix 용 Microsoft PHP 드라이버
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  이 페이지에는 Microsoft PHP Driver for SQL Server에 대한 지원 매트릭스 및 지원 드라이버에 대한 지원 주기 정책이 포함되어 있습니다.

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Microsoft PHP 드라이버 지원 수명 주기 매트릭스 및 정책
 MSL(Microsoft 지원 수명 주기) 정책은 Microsoft 제품 지원 수명 주기와 관련해서 투명하고 예측 가능한 정보를 제공합니다. PHP Driver 버전 3.x, 4.x 및 5.x는 드라이버 릴리스 날짜로부터 5년 동안 일반 지원을 제공합니다. 일반 지원은 [Microsoft 지원 수명 주기 웹 사이트](https://support.microsoft.com/lifecycle)에 정의되어 있습니다.

 확장 및 사용자 지정 지원 옵션은 Microsoft PHP Driver에는 사용할 수 없습니다.

 다음 Microsoft PHP Driver는 지정된 지원 종료 날짜까지 지원됩니다.

|드라이버 이름|드라이버 패키지 버전|일반 지원 종료|
|-|:-:|-|
|SQL Server 용 Microsoft PHP 드라이버 5.6|5.6|2024 2 월 21,|
|SQL Server 용 Microsoft PHP 드라이버 5.3|5.3|2023 년 7 월 20,|
|Microsoft PHP Drivers 5.2 for SQL Server|5.2|2023 년 2 월 9,|
|SQL Server 용 Microsoft PHP 드라이버 4.3|4.3|2022 년 7 월 6,|
|SQL Server 용 Microsoft PHP 드라이버 4.0|4.0|2021 년 7 월 11|
|Microsoft PHP Drivers 3.2 for SQL Server|3.2|2020 년 3 월 9|
|Microsoft PHP Drivers 3.1 for SQL Server|3.1|2019년 12월 12일|

 다음 Microsoft PHP Driver는 더 이상 지원되지 않습니다.

|드라이버 이름|드라이버 패키지 버전|일반 지원 종료|
|-|:-:|-|
|Microsoft PHP Drivers 3.0 for SQL Server|3.0|2017년 3월 6일|
|Microsoft PHP Drivers 2.0 for SQL Server|2.0|2015 년 8 월 10 일|
|SQL Server 용 Microsoft PHP 드라이버 1.0|1.0|2014년 4월 28일|

## <a name="sql-server-version-certified-compatibility"></a>SQL Server 버전 호환성 인증
 다음 매트릭스는 테스트 되었으며와 호환 된다고 해당 드라이버 버전을 사용 하 여 인증 하는 SQL Server 버전을 나열 합니다. 이전 드라이버 버전에서는 이전 버전과 호환성을 유지 하기 위해 노력 하지만 최신 지원 되는 드라이버만 테스트 하 고 SQL Server가 릴리스되면 새 SQL Server 버전을 사용 하 여 인증 합니다.

|SQL Server 드라이버 버전에 대 한 PHP&#8594;<br />&#8595; SQL Server 버전|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Azure SQL 관리되는 인스턴스<br/> (확장 된 비공개 미리 보기)|Y|Y|Y|Y| | | | | |
|Azure SQL 데이터 웨어하우스|Y|Y|Y|Y| | | | | |
|SQL Server 2017         |Y|Y|Y|Y| | | | | |
|SQL Server 2016         |Y|Y|Y|Y|Y| | | | |
|SQL Server 2014         |Y|Y|Y|Y|Y|Y|Y| | |
|SQL Server 2012         |Y|Y|Y|Y|Y|Y|Y|Y| |
|SQL Server 2008 R2      |Y|Y|Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008         | | | | |Y|Y|Y|Y|Y|

## <a name="php-version-support"></a>PHP 버전 지원
 다음 버전의 PHP는 Microsoft PHP 드라이버의 나열 된 버전을 사용 하 여 지원 됩니다.

|SQL Server 드라이버 버전에 대 한 PHP&#8594;<br />&#8595; PHP 버전|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|:---:|---|---|---|---|---|---|---|---|---|
|7.3|7.3.0+          |                |                |       |       | | | | |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|       |       | | | | |
|7.1|7.1.0+          |7.1.0+          |7.1.0+          |7.1.0+ |       |        |        |        |        |
|7.0|                |7.0.0+          |7.0.0+          |7.0.0+ |7.0.0+ |        |        |        |        |
|5.6|                |                |                |       |       |5.6.4+  |        |        |        |
|5.5|                |                |                |       |       |5.5.16+ |5.5.16+ |        |        |
|5.4|                |                |                |       |       |5.4.32  |5.4.32  |5.4.32  |        |
|5.3|                |                |                |       |       |        |        |5.3.0   |5.3.0   |
|5.2|                |                |                |       |       |        |        |        |5.2.4<br />5.2.13|

1. 7.2.1 버전 이상에서 사용할 Windows, 버전 7.2.0 하는 동안 및 나중에 Linux 및 macOS에서 지원 됩니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제
 Microsoft PHP 드라이버의 나열 된 버전을 사용 하 여 다음 Windows 운영 체제 버전이 지원 됩니다.

|SQL Server 드라이버 버전에 대 한 PHP&#8594;<br />&#8595; 운영 체제|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2016                 |Y  |Y  |Y  |Y  |   |   |   |   |   |
|Windows Server 2012 R2              |Y  |Y  |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows Server 2012                 |Y  |Y  |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows Server 2008 R2 SP1          |   |   |   |   |Y  |Y  |Y  |Y  |   |
|Windows Server 2008 R2              |   |   |   |   |   |   |   |   |Y  |
|Windows Server 2008 SP2             |   |   |   |   |Y  |Y  |Y  |Y  |   |
|Windows Server 2008                 |   |   |   |   |   |   |   |   |Y  |
|Windows Server 2003 SP1             |   |   |   |   |   |   |   |   |Y  |
|Windows 10                          |Y  |Y  |Y  |Y  |Y  |   |   |   |   |
|Windows 8.1                         |Y  |Y  |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows 8                           |   |   |   |Y  |Y  |Y  |Y  |   |   |
|Windows 7 SP1                       |   |   |   |   |Y  |Y  |Y  |Y  |   |
|Windows Vista SP2                   |   |   |   |   |Y  |Y  |Y  |Y  |Y  |
|Windows XP SP3                      |   |   |   |   |   |   |   |   |Y  |

 다음 Linux 및 Mac 운영 체제 버전 (64 비트만 해당)는 Microsoft PHP 드라이버의 나열 된 버전을 사용 하 여 지원 됩니다.

|SQL Server 드라이버 버전에 대 한 PHP&#8594;<br />&#8595; 운영 체제|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|--|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Ubuntu 18.10 (64 비트)               |Y  |   |   |   |   |   |   |   |   |
|Ubuntu 18.04 (64 비트)               |Y  |Y  |   |   |   |   |   |   |   |
|Ubuntu 17.10 (64 비트)               |   |Y  |Y  |   |   |   |   |   |   |
|Ubuntu 16.04 (64 비트)               |Y  |Y  |Y  |Y  |Y  |   |   |   |   |
|Ubuntu 15.10 (64 비트)               |   |   |   |Y  |   |   |   |   |   |
|Ubuntu 15.04 (64 비트)               |   |   |   |   |Y  |   |   |   |   |
|Debian 9 (64 비트)                   |Y  |Y  |Y  |   |   |   |   |   |   |
|Debian 8 (64 비트)                   |Y  |Y  |Y  |Y  |   |   |   |   |   |
|Red Hat Enterprise Linux 7(64비트) |Y  |Y  |Y  |Y  |Y  |   |   |   |   |
|Suse Enterprise Linux 15 (64 비트)   |Y  |   |   |   |   |   |   |   |   |
|Suse Enterprise Linux 12 (64 비트)   |Y  |Y  |Y  |   |   |   |   |   |   |
|macOS Mojave (64 비트)               |Y  |   |   |   |   |   |   |   |   |
|macOS High Sierra (64 비트)          |Y  |Y  |   |   |   |   |   |   |   |
|macOS Sierra (64 비트)               |Y  |Y  |Y  |Y  |   |   |   |   |   |
|macOS El Capitan (64 비트)           |   |Y  |Y  |Y  |   |   |   |   |   |

## <a name="see-also"></a>참고 항목  
[릴리스 정보](../../connect/php/release-notes-for-the-php-sql-driver.md)

[지원 리소스](../../connect/php/support-resources-for-the-php-sql-driver.md)

[시스템 요구 사항](../../connect/php/system-requirements-for-the-php-sql-driver.md)
