---
title: "Cron 사용 하 여 Linux에서 SSIS 패키지를 예약 | Microsoft Docs"
description: "이 문서에서는 cron 서비스를 사용 하 여 Linux에서 SQL Server Integration Services 패키지를 예약 하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 31d5fb63a9c2a4d8825aa39c6fa7e3377ddc8d91
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>일정 SQL Server Integration Services 패키지 cron 사용 하 여 Linux에서 실행

Windows에서 SQL Server Integration Services (SSIS) 및 SQL Server를 실행 하는 경우에 SQL Server 에이전트를 사용 하 여 SSIS 패키지의 실행을 자동화할 수 있습니다. SQL Server 및 SSIS linux를 실행 하면 이때 SQL Server 에이전트 유틸리티 사용할 수 없습니다 Linux에서 작업을 예약 하려면. 대신 사용 하 여 **Cron** 패키지 실행을 자동화 하려면 Linux 플랫폼에서 광범위 하 게 사용 되는 서비스입니다.

이 문서는 SSIS 패키지의 실행을 자동화 하는 방법을 보여 주는 예제를 제공 합니다. 예제에서는 Red Hat Enterprise에서 실행 되도록 작성 되었습니다. 코드는 Ubuntu와 같은 다른 Linux 배포판에 대 한 유사 합니다.

## <a name="prerequisites"></a>필수 구성 요소

작업을 실행 하는 Cron 서비스를 사용 하려면 먼저 Cron 서비스가 컴퓨터에서 실행 되 고 있는지 여부를 확인 해야 합니다.

다음 Cron 서비스의 상태를 확인 하는 명령을 사용 합니다.

`systemctl status crond.service`

서비스를 없는 경우 활성 (즉, 실행 중 아님)를 설정 하 고 Cron 서비스를 제대로 구성 관리자에 게 문의 합니다.

## <a name="create-jobs"></a>작업 만들기

Cron 작업은 지정된 된 간격으로 정기적으로 실행 되도록 구성할 수 있는 작업입니다. 작업을 일반적으로 콘솔에 직접 입력 하거나 셸 스크립트를 실행 하는 명령 처럼 간단할 수 있습니다.

쉽게 관리 및 유지 관리를 위해에 대 한 것이 좋습니다 설명적인 이름으로 스크립트에 패키지 실행 명령을 배치 합니다.

패키지를 실행 하는 단일 명령만 포함 하는 셸 스크립트의 간단한 예는 다음과 같습니다. 필요에 따라 더 많은 명령이 추가할 수 있습니다.

```
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>서비스와의 Cron 작업 예약

작업을 정의 하면 Cron 서비스를 사용 하 여 자동으로 실행 되도록 예약할 수 있습니다.

실행 하는 Cron에 대 한 작업을 추가 하려면 작업에 추가 해야는 `crontab` 파일입니다. 열려면는 `crontab` 파일을 추가 하거나 작업을 업데이트할 수 있습니다는 편집기에서 다음 명령을 사용 합니다.

`crontab -e`

매일 오전 2시 10분에 실행 되도록 앞에서 설명한 작업을 예약 하려면 다음 줄을 추가 `crontab` 파일:

```
# run SSIS package Name at 2:10AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

저장 된 `crontab` 파일을 편집기를 종료 합니다.

샘플 명령의 형식의 이해 하려면 다음 섹션의 정보를 검토 합니다.
 
## <a name="format-of-a-crontab-file"></a>Crontab 파일의 형식

다음 이미지는 표시에 추가 하는 작업 줄의 형식 설명의 `crontab` 파일입니다.

![Crontab 파일에 있는 항목에 대 한 형식 설명](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

더 자세한 설명을 가져올는 `crontab` 형식 파일에서 다음 명령을 사용 합니다.

`man 5 crontab`

부분적으로이 문서의 예제를 설명 하는 데 도움이 되는 출력의 예는 다음과 같습니다.

![자세한 설명은 부분 crontab 형식](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

