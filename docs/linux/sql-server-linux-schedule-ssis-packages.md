---
title: cron을 사용하여 Linux에서 SSIS 패키지 예약
description: 이 문서에서는 cron 서비스를 사용하여 Linux에서 SSIS(SQL Server Integration Services) 패키지를 예약하는 방법을 설명합니다.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: ac7648287b4e4b609f4dd4f25b1b07a512065364
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68065157"
---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>cron을 사용하여 Linux에서 SQL Server Integration Services 패키지 실행 예약

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Windows에서 SSIS(SQL Server Integration Services)와 SQL Server를 실행하는 경우 SQL Server 에이전트를 사용하여 SSIS 패키지 실행을 자동화할 수 있습니다. 그러나 Linux에서 SQL Server와 SSIS를 실행하는 경우에는 SQL Server 에이전트 유틸리티를 사용하여 Linux에서 작업을 예약할 수 없습니다. 대신, Linux 플랫폼에서 주로 사용되는 cron 서비스를 통해 패키지 실행을 자동화합니다.

이 문서에서는 SSIS 패키지 실행을 자동화하는 방법을 보여 주는 예제를 제공합니다. 예제는 Red Hat Enterprise에서 실행되도록 작성되었습니다. 하지만 코드는 Ubuntu 등의 다른 Linux 배포에서도 유사합니다.

## <a name="prerequisites"></a>사전 요구 사항

cron 서비스를 사용하여 작업을 실행하기 전에 컴퓨터에서 서비스가 실행되고 있는지 확인합니다.

cron 서비스의 상태를 확인하려면 `systemctl status crond.service` 명령을 사용합니다.

서비스가 활성화되지 않은 경우(즉, 실행되고 있지 않음), 관리자에게 cron 서비스를 올바르게 설정하고 구성하도록 요청합니다.

## <a name="create-jobs"></a>작업 만들기

cron 작업은 지정된 간격마다 주기적으로 실행되도록 구성할 수 있는 태스크입니다. 작업은 일반적으로 콘솔에서 직접 입력하거나 셸 스크립트로 실행하는 명령처럼 간단할 수 있습니다.

간편한 관리 및 유지 관리를 위해 설명이 포함된 이름을 가진 스크립트에 패키지 실행 명령을 저장하는 것이 좋습니다.

다음은 패키지를 실행하기 위한 간단한 셸 스크립트의 예입니다. 이 스크립트에는 단일 명령만 포함되어 있지만, 필요에 따라 더 많은 명령을 추가할 수 있습니다.

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>cron 서비스를 사용하여 작업 예약

작업을 정의한 후에 cron 서비스를 사용하여 자동으로 실행되도록 예약할 수 있습니다.

cron에서 실행할 작업을 추가하려면 crontab 파일에 작업을 추가합니다. 작업을 추가하거나 업데이트할 수 있는 crontab 파일을 편집기에서 열려면 `crontab -e` 명령을 사용합니다.

앞서 설명한 작업이 매일 오전 2:10에 실행되도록 예약하려면 crontab 파일에 다음 줄을 추가합니다.

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

crontab 파일을 저장하고 편집기를 종료합니다.

샘플 명령의 형식을 파악하려면 다음 섹션의 정보를 검토합니다.
 
## <a name="format-of-a-crontab-file"></a>crontab 파일의 형식

다음 그림은 crontab 파일에 추가된 작업 줄의 형식 설명을 보여 줍니다.

![crontab 파일 항목의 형식 설명](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

crontab 파일 형식에 대한 자세한 설명을 보려면 `man 5 crontab` 명령을 사용합니다.

다음은 이 문서의 예제를 설명하는 데 도움이 되는 출력의 일부 예입니다.

![crontab 형식에 대한 자세한 설명의 일부](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

## <a name="related-content-about-ssis-on-linux"></a>Linux SSIS에 대한 관련 콘텐츠
-   [SSIS를 사용하여 Linux에서 데이터 추출, 변환 및 로드](sql-server-linux-migrate-ssis.md)
-   [Linux에서 SSIS(SQL Server Integration Services) 설치](sql-server-linux-setup-ssis.md)
-   [ssis-conf를 사용하여 Linux에서 SQL Server Integration Services 구성](sql-server-linux-configure-ssis.md)
-   [Linux SSIS의 제한 사항 및 알려진 문제](sql-server-linux-ssis-known-issues.md)
