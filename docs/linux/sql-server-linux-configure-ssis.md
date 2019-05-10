---
title: Conf ssis를 사용 하 여 Linux의 SSIS 구성 | Microsoft Docs
description: 이 문서에서는 ssis conf 유틸리티를 사용 하 여 Linux에서 SQL Server Integration Services (SSIS)를 구성 하는 방법을 설명 합니다.
author: lrtoyou1223
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: c22fed22e4d2c8d2a903f72c9a28763efd491ee0
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65488363"
---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>Conf ssis를 사용 하 여 Linux에서 SQL Server Integration Services 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

실행 하는 `ssis-conf` Red Hat Enterprise Linux 및 Ubuntu 용 SQL Server Integration Services (SSIS)를 설치한 경우에 스크립트를 구성 합니다. SSIS를 설치 하는 방법에 대 한 자세한 내용은 참조 하세요. [설치 SQL Server Integration Services (SSIS) linux](sql-server-linux-setup-ssis.md)합니다.

사용할 수도 있습니다는 `ssis-conf` 유틸리티는 다음 속성을 구성 하려면:

| Command | Description |
|-------------|---------------------------------------------------------------------|
| set-edition | SQL Server의 버전 설정                                       |
| 원격 분석   | SQL Server Integration Services 원격 분석 서비스를 사용할지 설정 합니다. |
| 설치       | 초기화 하 고 Microsoft SQL Server Integration Services 설정      |
|||

## <a name="run-ssis-conf"></a>Ssis conf 실행

실행이 문서의 예제에서는 `ssis-conf` 전체 경로 지정 하 여: `/opt/ssis/bin/ssis-conf`합니다. 실행 하기 전에 해당 위치로 이동 하는 경우 `ssis-conf`, 현재 디렉터리의 컨텍스트에서 유틸리티를 실행할 수 있습니다: `./ssis-conf`합니다.

루트 권한으로이 문서에서 설명 하는 명령을 실행 해야 합니다. 예를 들어 실행할 `sudo /opt/ssis/bin/ssis-conf setup` 아닌 `/opt/ssis/bin/ssis-conf setup`합니다.

선호 하는 언어로 표시 되는 메시지를 사용 하 여 이러한 명령을 실행 하려면 로캘을 지정할 수 있습니다. 예를 들어 중국어에서 표시 되는 메시지를 수신 하려면 다음 명령을 실행: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`합니다.

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>집합 버전을 사용 하 여 SQL Server Integration Services의 버전 설정

SSIS의 버전의 SQL Server 버전에 맞춰집니다.

다음 명령을 입력 합니다. `$ sudo /opt/ssis/bin/ssis-conf set-edition`합니다.

명령을 입력 한 후 다음 프롬프트를 받게 됩니다.

```
Choose an edition of SQL Server:

1) Evaluation (free, no production use rights, 180-day limit)

2) Developer (free, no production use rights)

3) Express (free)

4) Web (PAID)

5) Standard (PAID)

6) Enterprise (PAID)

7) Enterprise Core (PAID)

8) I bought a license through a retail sales channel and have a product key to enter.

Details about editions can be found at https://go.microsoft.com/fwlink/?LinkId=852748&clcid=0x409.

Use of PAID editions of this software requires separate licensing through a Microsoft Volume Licensing program.

By choosing a PAID edition, you are verifying that you have the appropriate number of licenses in place to install and run this software.

Enter your edition (1-8):
```

값 1에서 7를 입력 하면 시스템 무료 또는 유료 버전을 구성 합니다. 8를 입력 하면 구입한 제품 키를 입력 하 라는 메시지가 표시:

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>원격 분석을 사용 하 여 고객 피드백을 구성 하려면

`telemetry` 명령은 SSIS Microsoft에 피드백을 전송 하는지 여부를 확인 합니다.

무료 버전 (즉, Express, Developer 및 Evaluation 버전)에 대 한 원격 분석 서비스가 항상 활성화 됩니다. 무료 버전을 사용 하는 경우 사용할 수 없습니다는 `telemetry` 명령을 원격 분석을 사용 하지 않도록 설정 합니다.

다음 명령을 입력 합니다. `$ sudo /opt/ssis/bin/ssis-conf telemetry`합니다.

유료 버전에 대 한 명령을 입력 한 후 받게 다음 프롬프트:

```
Send feature usage data to Microsoft. Feature usage data includes information about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

선택 하는 경우 **예**, 원격 분석 서비스 사용 가능 하 고 실행을 시작 합니다. 서비스는 각 부팅 후 자동으로 시작 됩니다. 선택 하는 경우 **No**, 원격 분석 서비스를 중지 하 고는 사용 하지 않도록 설정 합니다.

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>설치 프로그램을 초기화 하 고 Microsoft SQL Server Integration Services 설정 사용

사용 된 `setup` SSIS를 설치할 때마다 명령입니다.

다음 명령을 입력 합니다. `sudo /opt/ssis/bin/ssis-conf setup`합니다.

유틸리티를 승인 하거나 다음 항목에 대 한 값을 제공 하 라는 메시지가 표시:
-   제품 라이선스
-   EULA 계약에 동의
-   원격 분석 서비스
-   Integration Services에서 사용 되는 언어

실행 하는 `setup` 명령 언어에서 프롬프트는 원하는 로캘을 지정할 수 있습니다. 예를 들어 중국어에서 표시 되는 메시지를 수신 하려면 다음 명령을 실행: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`합니다.

## <a name="ssisconf-format"></a>ssis.conf 형식

다음 `/var/opt/ssis/ssis.conf` 파일은 각 설정에 대 한 예제를 제공 합니다.

SQL Server에 대 한 시스템 설정에서 값을 변경 하 여 변경할 수 있습니다는 `mssql.conf` 파일입니다. SSIS에 대 한 있습니다 *없습니다* 의 값을 변경 하 여 시스템 설정을 변경 합니다 `ssis.conf` 파일. `ssis.conf` 파일 설치의 결과만 표시 합니다. SSIS에 대 한 설정을 변경 하려는 경우 삭제할 수 있습니다 합니다 `ssis.conf` 파일을 실행 합니다 `setup` 명령을 다시 합니다.

다음은 샘플 `ssis.conf` 파일입니다. 각 필드 하나 설치 단계의 결과에 해당합니다.

```
[LICENSE]
                       
registered = Y        
                       
pid = enterprisecore  
                       
[EULA]
                       
accepteula = Y        
                       
[TELEMETRY]
                       
enabled = Y           
                       
[language]
                       
lcid = 2052
```

## <a name="related-content-about-ssis-on-linux"></a>Linux에서 SSIS에 대 한 관련된 콘텐츠
-   [추출, 변환 및 SSIS와 Linux에서 데이터 로드](sql-server-linux-migrate-ssis.md)
-   [Linux의 SQL Server Integration Services (SSIS)를 설치 합니다.](sql-server-linux-setup-ssis.md)
-   [제한 사항 및 Linux에서 SSIS에 대 한 알려진된 문제](sql-server-linux-ssis-known-issues.md)
-   [일정 SQL Server Integration Services 패키지 cron 사용 하 여 Linux에서 실행](sql-server-linux-schedule-ssis-packages.md)
