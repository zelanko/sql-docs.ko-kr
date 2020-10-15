---
title: Azure Arc 사용 SQL Server에 대해 SQL 평가 구성
titleSuffix: ''
description: Azure Arc 사용 SQL Server 인스턴스에 대해 주문형 평가 구성
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 41a7f1f4edc247f211ee5b3cdcaddfd139c5027c
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988019"
---
# <a name="configure-on-demand-sql-assessment-for-azure-arc-enabled-sql-server-instance"></a>Azure Arc 사용 SQL Server 인스턴스에 대해 주문형 SQL 평가 구성

다음 단계를 수행하여 SQL Server 인스턴스에 SQL 평가를 사용하도록 설정할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

* SQL Server 인스턴스가 Azure Arc에 연결되어 있습니다. 지침에 따라 [SQL Server 인스턴스를 Arc 사용 SQL Server에 온보딩](connect.md)합니다.

* MMA 확장이 머신에 설치되었으며 구성되어 있습니다. 지침에 따라 [MMA(Microsoft Monitoring Agent)를 설치](configure-advanced-data-security.md#install-microsoft-monitoring-agent-mma)합니다. 자세한 내용은 [Log Analytics 에이전트](/azure/azure-monitor/platform/log-analytics-agent)를 참조하세요.

* SQL Server에서 [TCP/IP 프로토콜을 사용](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)할 수 있습니다.

* 명명된 SQL Server 인스턴스를 운영하는 경우 [SQL Server Browser](../../tools/configuration-manager/sql-server-browser-service.md)가 실행되고 있습니다.

* [서비스 허브 주문형 평가 필수 조건](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents)에서 SQL Server 문서를 검토했습니다.

## <a name="enable-on-demand-sql-assessment"></a>주문형 SQL 평가 사용

1. SQL Server - Azure Arc 리소스를 열고 왼쪽 메뉴에서 __환경 상태__를 선택합니다.

   ![SQL 평가 선택](media/assess/sql-assessment-heading-sql-server-arc.png)

1. 데이터 수집 머신의 작업 디렉터리를 지정합니다. 기본적으로 `C:\sql_assessment\work_dir`이 사용됩니다. 수집 및 분석 중에 데이터가 해당 폴더 아래에 임시로 저장됩니다. 폴더가 없으면 자동으로 생성됩니다.

1. __구성 스크립트 다운로드__를 클릭하고 다운로드한 스크립트를 대상 머신에 복사합니다.

1. __powershell.exe__의 관리자 인스턴스를 시작하고 다음 중 하나를 수행합니다. 
   * 도메인 계정을 사용하는 경우 다음 명령을 실행합니다. 사용자 계정 및 암호를 입력하라는 메시지가 표시됩니다. 

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1'
      ```

    * MSA 계정을 사용하는 경우 다음 명령을 실행합니다.

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1' -ManagedServiceAccountName <MSA account name>
      ```

   > [!NOTE]
   > 이 스크립트는 이전 스크립트를 실행한 후 1시간 이내에 실행된 다음, 7일마다 실행되도록 *SQLAssessment*라는 작업을 예약합니다. 작업 스케줄러 라이브러리 > Microsoft > Operations Management Suite > AOI*** > 평가 > SQLAssessment에서 다른 날짜 및 시간에 실행되도록 작업을 수정하거나 강제로 즉시 실행할 수도 있습니다. 이 작업은 데이터 수집을 트리거합니다.

## <a name="view-the-assessment-results"></a>평가 결과 보기

Log Analytics에서 결과가 준비되기 전에는 환경 상태 블레이드의 __SQL 평가 결과 보기__ 단추를 사용할 수 없습니다. 단추가 활성화되면 클릭하여 결과를 볼 수 있습니다. 대상 머신에서 데이터 파일을 처리한 후 Log Analytics에 결과가 표시되기까지 최대 2시간이 걸릴 수 있습니다.

![SQL 평가 결과](media/assess/sql-assessment-results.png)

작업 폴더에 있는 파일을 검사하여 수집 머신의 데이터 처리 상태를 확인할 수 있습니다. 예약된 작업이 완료되면 작업 디렉터리에 _new._ 접두사가 있는 파일이 여러 개 표시됩니다.

![데이터 파일 준비 완료](media/assess/sql-assessment-data-files-ready.png)

Microsoft Monitoring Agent는 15분마다 작업 폴더를 검사하여 _new.*_ 파일을 찾은 다음, 데이터를 Log Analytics 작업 영역으로 보냅니다. 파일이 업로드되면 접두사가 _new._ 에서 _processed._ 로 변경됩니다.

![데이터 파일 처리됨](media/assess/sql-assessment-data-files-processed.png)

## <a name="next-steps"></a>다음 단계

자세한 내용은 [서비스 허브 주문형 평가 필수 조건](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents)에서 SQL Server 문서를 참조하세요.

주문형 SQL 평가의 포괄적인 지원을 받으려면 프리미어 또는 통합 지원 구독이 필요합니다. 자세한 내용은 [Azure 프리미어 지원](https://azure.microsoft.com/support/plans/premier)을 확인하세요.