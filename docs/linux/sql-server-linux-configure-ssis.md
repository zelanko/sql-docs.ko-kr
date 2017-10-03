---
title: "Linux에서 ssis conf SSIS 구성 | Microsoft Docs"
description: "이 문서는 Linux에서 ssis conf 유틸리티와 SQL Server Integration Services를 구성 하는 방법을 보여 줍니다."
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.date: 09/26/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: integration-services
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 46327772e8c22f76770bc51f72817ceedffae469
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>Linux에서 SQL Server Integration Services ssis conf 구성

`ssis-conf`다음 경우에 구성 스크립트는 Red Hat Enterprise Linux 및 Ubuntu 용 SQL Server Integration Services (SSIS)를 설치 합니다. 다음 속성을 구성 하려면이 유틸리티를 사용할 수 있습니다.

| Command | Description |
|-------------|---------------------------------------------------------------------|
| set 버전 | 버전의 SQL Server 설정                                       |
| 원격 분석   | SQL Server Integration Services 원격 분석 서비스를 사용할지 설정 합니다. |
| 설치       | 초기화 하 고 Microsoft SQL Server Integration Services 설치      |
|||

## <a name="how-to-run-ssis-conf"></a>Ssis conf를 실행 하는 방법

실행이 문서의 예제 `ssis-conf` 전체 경로 지정 하 여: `/opt/ssis/bin/ssis-conf`합니다. 실행 하기 전에 해당 경로로 이동 하는 경우 `ssis-conf`, 현재 디렉터리의 컨텍스트에서 유틸리티를 실행할 수 있습니다: `./ssis-conf`합니다.

루트 권한이 있는이 문서에서 설명 하는 명령을 실행 하 고 있는지 확인 합니다. 예를 들어 실행 `sudo /opt/ssis/bin/ssis-conf setup` 아닌 `/opt/ssis/bin/ssis-conf setup`합니다.

이러한 명령은 프로그래밍 언어의 안내를 실행 하려면 로캘을 지정할 수 있습니다. 예를 들어 중국어로 표시 되는 메시지를 보려면 다음 명령을 실행 합니다.

`sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`을 참조하세요.

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>집합 버전을 사용 하 여 SQL Server Integration Services의 버전을 설정 하려면

SSIS 에디션의 SQL Server 버전에 맞춰집니다.

다음 명령을 입력합니다.

`$ sudo /opt/ssis/bin/ssis-conf set-edition`

명령을 입력 한 후 다음과 같은 메시지가 표시 됩니다.

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

Details about editions can be found at

https://go.microsoft.com/fwlink/?LinkId=852748&clcid=0x409

Use of PAID editions of this software requires separate licensing through a

Microsoft Volume Licensing program.

By choosing a PAID edition, you are verifying that you have the appropriate

number of licenses in place to install and run this software.

Enter your edition(1-8):
```

하는 경우를 시스템 무료 또는 유료일 edition을 구성 하는 1에서 7 사이의 값을 입력 합니다. 8를 입력 한 경우 구입한 제품 키를 입력 하 라는 메시지가 표시:

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>원격 분석을 사용 하 여 고객 피드백을 구성 하려면

`telemetry` 명령 SSIS에서 Microsoft에 피드백을 보낼 것인지 여부를 결정 합니다.

무료 버전 (즉,: Express, Developer 및 Evaluation edition), 원격 분석 서비스는 항상 사용 됩니다. 무료 버전을 사용 하는 경우 사용할 수 없습니다는 `telemetry` 명령을 원격 분석을 사용 하지 않도록 설정 합니다.

다음 명령을 입력합니다.

`$ sudo /opt/ssis/bin/ssis-conf telemetry`

유료 버전에 대 한 명령을 입력 한 후 다음 메시지가 나타납니다.

```
Send feature usage data to Microsoft. Feature usage data includes information
about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

경우 선택 **예**, 원격 분석 서비스는 사용 하도록 설정 하 고 실행을 시작 합니다. 서비스 자동-시작 지연 각 부팅 합니다. 경우 선택 **아니요**, 원격 분석 서비스 중지 하 고는 사용 하지 않도록 설정 합니다.

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>설치 프로그램을 사용 하 여 초기화 하 고 Microsoft SQL Server Integration Services를 설정 하려면

사용 된 `setup` SSIS를 설치할 때마다 명령입니다.

다음 명령을 입력합니다.

`sudo /opt/ssis/bin/ssis-conf setup`

유틸리티는 다음 항목에 대 한 값을 제공 하기 위해 또는 승인 하는 데 메시지가 나타납니다.
-   제품 라이선스
-   EULA 계약에 동의
-   원격 분석 서비스
-   Integration Services에서 사용 되는 언어

실행 하는 `setup` 명령 언어에 게 메시지를 표시를 원하는, 한 로캘을 지정할 수 있습니다. 예를 들어 중국어로 표시 되는 메시지를 보려면 다음 명령을 실행: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`합니다.

## <a name="ssisconf-format"></a>ssis.conf 형식

다음 `/var/opt/ssis/ssis.conf` 파일 각 설정에 대 한 예제를 제공 합니다.

SQL Server에 대 한 시스템 설정의 값을 변경 하 여 변경할 수 있습니다는 `mssql.conf` 파일입니다. SSIS에 대 한 있습니다 **없습니다** 의 값을 변경 하 여 시스템 설정을 변경는 `ssis.conf` 파일입니다. `ssis.conf` 파일 에서만 설치 프로그램의 결과 보여 줍니다. SSIS에 대 한 설정을 변경 하려는 경우 삭제할 수 있습니다는 `ssis.conf` 파일 및 실행 된 `setup` 명령을 다시 합니다.

다음은 샘플 `ssis.conf` 파일입니다. 각 필드의 한 설치 단계 결과에 해당합니다.

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
