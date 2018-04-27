---
title: Cron 사용 하 여 Linux에서 SSIS 패키지를 예약 | Microsoft Docs
description: 이 문서에서는 cron 서비스를 사용 하 여 Linux에서 SQL Server Integration Services (SSIS) 패키지를 예약 하는 방법을 설명 합니다.
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: e97296abfe1cdbdf331340ec77bad0f39c0110a7
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>일정 SQL Server Integration Services 패키지 cron 사용 하 여 Linux에서 실행

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Windows에서 SQL Server Integration Services (SSIS) 및 SQL Server를 실행 하는 경우에 SQL Server 에이전트를 사용 하 여 SSIS 패키지의 실행을 자동화할 수 있습니다. SQL Server 및 SSIS linux를 실행 하면 이때 SQL Server 에이전트 유틸리티 사용할 수 없습니다 Linux에서 작업을 예약 하려면. 대신, 패키지 실행을 자동화 하려면 Linux 플랫폼에서 널리 사용 되는 cron 서비스를 사용 합니다.

이 문서는 SSIS 패키지의 실행을 자동화 하는 방법을 보여 주는 예제를 제공 합니다. 예제에서는 Red Hat Enterprise에서 실행 되도록 작성 됩니다. 코드는 Ubuntu 등 다른 Linux 배포판에 대 한 유사 합니다.

## <a name="prerequisites"></a>필수 구성 요소

작업을 실행 하는 cron 서비스를 사용 하기 전에 컴퓨터에서 실행 되 고 있는지를 확인 합니다.

Cron 서비스의 상태를 확인 하려면 다음 명령을 사용 하 여: `systemctl status crond.service`합니다.

서비스가 활성화 되지 않은 경우 (즉, 실행 중이지 않으면), 설정 및 cron 서비스를 제대로 구성 하려면 관리자에 게 문의 합니다.

## <a name="create-jobs"></a>작업 만들기

Cron 작업은 지정된 된 간격으로 정기적으로 실행 되도록 구성할 수 있는 작업입니다. 작업을 일반적으로 콘솔에 직접 입력 하거나 셸 스크립트를 실행 하는 명령 처럼 간단할 수 있습니다.

쉽게 관리 및 유지 관리를 위해에 대 한 설명이 포함 된 이름을 포함 하는 스크립트에 패키지 실행 명령을 배치 하는 것이 좋습니다.

패키지를 실행 하는 간단한 셸 스크립트의 예를 들면 다음과 같습니다. 단일 명령에 포함 되어 있지만 더 많은 명령이 필요에 따라 추가할 수 있습니다.

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>서비스와의 cron 작업 예약

작업을 정의 하면 cron 서비스를 사용 하 여 자동으로 실행 되도록 예약할 수 있습니다.

실행 하는 cron에 대 한 작업을 추가 하려면 crontab 파일에 작업을 추가 합니다. Crontab 파일을 추가 하거나 작업을 업데이트할 수 있는 편집기에서 열려면 다음 명령을 사용 하 여: `crontab -e`합니다.

매일 오전 2시 10분 시에 실행 되도록 앞에서 설명한 작업을 예약 하려면 crontab 파일에 다음 줄을 추가 합니다.

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

Crontab 파일을 저장 하 고 편집기를 종료 합니다.

샘플 명령의 형식의 이해 하려면 다음 섹션의 정보를 검토 합니다.
 
## <a name="format-of-a-crontab-file"></a>Crontab 파일의 형식

다음 그림에서는 crontab 파일에 추가 하는 작업 줄에 대 한 형식 설명을 보여 줍니다.

![Crontab 파일에 있는 항목에 대 한 형식 설명](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

더 자세한 설명을 crontab 파일 형식의 가져오려면 다음 명령을 사용 하 여: `man 5 crontab`합니다.

부분적으로이 문서의 예제를 설명 하는 데 도움이 되는 출력의 예는 다음과 같습니다.

![자세한 설명은 부분 crontab 형식](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

## <a name="related-content-about-ssis-on-linux"></a>Linux에서 SSIS에 대 한 관련된 내용
-   [추출, 변환 및 SSIS와 Linux에서 데이터 로드](sql-server-linux-migrate-ssis.md)
-   [Linux에서 SQL Server Integration Services (SSIS)를 설치 합니다.](sql-server-linux-setup-ssis.md)
-   [Linux에서 SQL Server Integration Services ssis conf 구성](sql-server-linux-configure-ssis.md)
-   [Linux에서 SSIS에 대 한 알려진된 문제 및 제한](sql-server-linux-ssis-known-issues.md)
