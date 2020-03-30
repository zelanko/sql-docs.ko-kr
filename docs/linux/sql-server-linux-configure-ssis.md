---
title: ssis-conf를 사용하여 Linux에서 SSIS 구성
description: 이 문서에서는 ssis-conf 유틸리티를 사용하여 Linux에서 SSIS(SQL Server Integration Services)를 구성하는 방법을 설명합니다.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 51dc2ba27e346dea75f1bd347491d4932695fd43
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68077528"
---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>ssis-conf를 사용하여 Linux에서 SQL Server Integration Services 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Red Hat Enterprise Linux 및 Ubuntu용 SSIS(SQL Server Integration Services)를 설치할 때 `ssis-conf` 구성 스크립트를 실행합니다. SSIS 설치에 대한 자세한 내용은 [Linux에서 SSIS(SQL Server Integration Services) 설치](sql-server-linux-setup-ssis.md)를 참조하세요.

또한 `ssis-conf` 유틸리티를 사용하여 다음 속성을 구성할 수 있습니다.

| 명령 | Description |
|-------------|---------------------------------------------------------------------|
| set-edition | SQL Server 버전 설정                                       |
| telemetry   | SQL Server Integration Services 원격 분석 서비스 사용 또는 사용 안 함 |
| 설치       | Microsoft SQL Server Integration Services 초기화 및 설정      |
|||

## <a name="run-ssis-conf"></a>ssis-conf 실행

이 문서의 예제에서는 전체 경로인 `ssis-conf`를 지정하여 `/opt/ssis/bin/ssis-conf`를 실행합니다. `ssis-conf`를 실행하기 전에 해당 위치로 이동하면 현재 디렉터리의 컨텍스트에서 유틸리티를 실행할 수 있습니다. `./ssis-conf`.

이 문서에 설명된 명령은 루트 권한으로 실행해야 합니다. 예를 들어 `sudo /opt/ssis/bin/ssis-conf setup`이 아닌 `/opt/ssis/bin/ssis-conf setup`를 실행합니다.

원하는 언어로 프롬프트를 사용하여 이 명령을 실행하려면 로캘을 지정하면 됩니다. 예를 들어 중국어로 메시지를 수신하려면 `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup` 명령을 실행합니다.

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>set-edition을 사용하여 SQL Server Integration Services 버전 설정

SSIS 버전은 SQL Server 버전에 맞게 조정됩니다.

`$ sudo /opt/ssis/bin/ssis-conf set-edition` 명령을 입력합니다.

명령을 입력한 후 다음과 같은 메시지가 표시됩니다.

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

1~7의 값을 입력하면 시스템에서 체험 버전 또는 유료 버전을 구성합니다. 8을 입력하면 유틸리티에서 구매한 제품 키를 입력하라는 메시지를 표시합니다.

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>원격 분석을 사용하여 고객 의견 구성

`telemetry` 명령은 SSIS에서 사용자 의견을 Microsoft에 보낼지 여부를 결정합니다.

체험 버전(Express, Developer 및 Evaluation Edition)의 경우 원격 분석 서비스는 항상 사용하도록 설정됩니다. 체험 버전이 있는 경우 `telemetry` 명령을 사용하여 원격 분석을 사용하지 않도록 설정할 수 없습니다.

`$ sudo /opt/ssis/bin/ssis-conf telemetry` 명령을 입력합니다.

유료 버전의 경우 명령을 입력한 후 다음과 같은 메시지가 표시됩니다.

```
Send feature usage data to Microsoft. Feature usage data includes information about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

**예**를 선택하면 원격 분석 서비스가 사용하도록 설정되고 실행을 시작합니다. 각 부팅 후에 서비스가 자동으로 시작됩니다. **아니요**를 선택하면 원격 분석 서비스가 중지되고 사용하지 않도록 설정됩니다.

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>설치 프로그램을 사용하여 Microsoft SQL Server Integration Services 초기화 및 설정

SSIS를 설치할 때마다 `setup` 명령을 사용합니다.

`sudo /opt/ssis/bin/ssis-conf setup` 명령을 입력합니다.

이 유틸리티는 다음 항목의 값을 승인하거나 제공하라는 메시지를 표시합니다.
-   제품 라이선스
-   EULA 계약
-   원격 분석 서비스
-   Integration Services에서 사용되는 언어

원하는 언어의 프롬프트를 통해 `setup` 명령을 실행하려면 로캘을 지정하면 됩니다. 예를 들어 중국어로 메시지를 수신하려면 `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup` 명령을 실행합니다.

## <a name="ssisconf-format"></a>ssis.conf 형식

다음 `/var/opt/ssis/ssis.conf` 파일은 각 설정의 예제를 제공합니다.

SQL Server의 경우 `mssql.conf` 파일에서 값을 변경하여 시스템 설정을 변경할 수 있습니다. SSIS의 경우  *파일에서 값을 변경하여 시스템 설정을 변경’할 수 없습니다’.* `ssis.conf` `ssis.conf` 파일에는 설정 결과만 표시됩니다. SSIS의 설정을 변경하려는 경우 `ssis.conf` 파일을 삭제하고 `setup` 명령을 다시 실행할 수 있습니다.

다음은 샘플 `ssis.conf` 파일입니다. 각 필드는 한 설정 단계의 결과에 해당합니다.

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

## <a name="related-content-about-ssis-on-linux"></a>Linux SSIS에 대한 관련 콘텐츠
-   [SSIS를 사용하여 Linux에서 데이터 추출, 변환 및 로드](sql-server-linux-migrate-ssis.md)
-   [Linux에서 SSIS(SQL Server Integration Services) 설치](sql-server-linux-setup-ssis.md)
-   [Linux SSIS의 제한 사항 및 알려진 문제](sql-server-linux-ssis-known-issues.md)
-   [cron을 사용하여 Linux에서 SQL Server Integration Services 패키지 실행 예약](sql-server-linux-schedule-ssis-packages.md)
