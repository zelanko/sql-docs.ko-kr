---
title: Linux에서 cron 사용 하 여 SSIS 패키지를 예약 합니다. | Microsoft Docs
description: 이 문서에서는 Linux에서 cron 서비스를 사용 하 여 SQL Server Integration Services (SSIS) 패키지를 예약 하는 방법을 설명 합니다.
author: lrtoyou1223
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 32734698fffde10594513ad770b2129886e97b01
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65486043"
---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>일정 SQL Server Integration Services 패키지 cron 사용 하 여 Linux에서 실행

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Windows에서 SQL Server Integration Services (SSIS) 및 SQL Server를 실행 하면 SQL Server 에이전트를 사용 하 여 SSIS 패키지의 실행을 자동화할 수 있습니다. 그러나 Linux에서 SQL Server 및 SSIS를 실행 하면 SQL Server 에이전트 유틸리티를 사용할 수 없는 Linux에서 작업을 예약 합니다. 대신, 패키지 실행을 자동화 하는 Linux 플랫폼에서 널리 사용 되는 cron 서비스를 사용 합니다.

이 문서에서는 SSIS 패키지의 실행을 자동화 하는 방법을 보여주는 예제를 제공 합니다. 예제는 Red Hat Enterprise에서 실행에 기록 됩니다. 이 코드는 Ubuntu와 같은 기타 Linux 배포에 대해 유사 합니다.

## <a name="prerequisites"></a>사전 요구 사항

작업을 실행 하려면 cron 서비스를 사용 하기 전에 컴퓨터에서 실행 되 고 있는지 여부를 확인 합니다.

Cron 서비스의 상태를 확인 하려면 다음 명령을 사용 하 여: `systemctl status crond.service`합니다.

서비스가 활성화 되지 않은 경우 (즉,이 실행 하지 않는) 설정 하 고 cron 서비스를 제대로 구성 하려면 관리자에 게 문의 합니다.

## <a name="create-jobs"></a>작업 만들기

Cron 작업은 지정된 된 간격에 정기적으로 실행 되도록 구성할 수 있는 작업. 작업은 일반적으로 콘솔에 직접 입력 하거나 셸 스크립트를 실행 하는 명령 처럼 간단할 수 있습니다.

손쉬운 관리 및 유지 관리 목적에 대 한 설명이 포함 된 이름이 포함 된 스크립트에서 패키지 실행 명령을 추가 하는 것이 좋습니다.

패키지 실행에 대 한 간단한 셸 스크립트의 예는 다음과 같습니다. 단일 명령만 포함 하지만 필요에 따라 더 많은 명령을 추가할 수 있습니다.

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>Cron 사용 하 여 작업 예약

작업을 정의한 후에 cron를 사용 하 여 자동으로 실행 하도록 예약할 수 있습니다.

실행 하려면 cron에 대 한 작업을 추가 하려면 crontab 파일에서 작업을 추가 합니다. Crontab 파일을 추가 하거나 작업을 업데이트할 수 있는 편집기에서를 열려면 다음 명령을 사용 하 여: `crontab -e`합니다.

매일 오전 2 시 10을 실행 하려면 앞에서 설명한 작업을 예약 하려면 crontab 파일에 다음 줄을 추가:

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

Crontab 파일을 저장 하 고 편집기를 종료 합니다.

샘플 명령은 형식의 이해 하려면 다음 섹션의 정보를 검토 합니다.
 
## <a name="format-of-a-crontab-file"></a>Crontab 파일의 형식

다음 이미지는 형식에 대 한 설명은 crontab 파일에 추가 되는 작업 줄을 표시 합니다.

![Crontab 파일의 항목에 대 한 형식 설명](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

Crontab 파일 형식의 더 자세한 설명을 가져오려면 다음 명령을 사용 하 여: `man 5 crontab`합니다.

이 문서의 예제를 설명 하는 데 도움이 되는 출력의 일부 예제는 다음과 같습니다.

![Crontab 형식의 자세한 부분 설명](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

## <a name="related-content-about-ssis-on-linux"></a>Linux에서 SSIS에 대 한 관련된 콘텐츠
-   [추출, 변환 및 SSIS와 Linux에서 데이터 로드](sql-server-linux-migrate-ssis.md)
-   [Linux의 SQL Server Integration Services (SSIS)를 설치 합니다.](sql-server-linux-setup-ssis.md)
-   [Conf ssis를 사용 하 여 Linux에서 SQL Server Integration Services 구성](sql-server-linux-configure-ssis.md)
-   [제한 사항 및 Linux에서 SSIS에 대 한 알려진된 문제](sql-server-linux-ssis-known-issues.md)
