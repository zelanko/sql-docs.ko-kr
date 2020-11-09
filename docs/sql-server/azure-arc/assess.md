---
title: Azure Arc 사용 SQL Server 인스턴스에서 주문형 SQL 평가 구성
description: Azure Arc 사용 SQL Server 인스턴스에서 주문형 SQL 평가 구성
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: c6f2a0989cb13253ef4a6a26e013a6b8c7a84ded
ms.sourcegitcommit: f888ac94c7b5f6b6f138ab75719dadca04e8284a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93294383"
---
# <a name="configure-sql-assessment-on-an-azure-arc-enabled-sql-server-instance"></a>Azure Arc 사용 SQL Server에서 SQL 평가 구성

SQL 평가는 SQL Server의 구성을 평가하는 메커니즘을 제공합니다. 이 문서에서는 Azure Arc 사용 SQL Server 인스턴스에서 SQL 평가를 사용하는 방법에 대한 지침을 제공합니다.

## <a name="prerequisites"></a>필수 구성 요소

* SQL Server 인스턴스가 Azure Arc에 연결되어 있어야 합니다. 지침은 [SQL Server를 Azure Arc에 연결](connect.md) 문서를 참조하세요.

* 컴퓨터에 MMA(Microsoft Monitoring Agent) 확장을 설치하고 구성해야 합니다. 지침은 [MMA 설치](configure-advanced-data-security.md#install-microsoft-monitoring-agent-mma) 문서를 참조하세요. [Log Analytics 에이전트](/azure/azure-monitor/platform/log-analytics-agent) 문서에서도 자세한 정보를 얻을 수 있습니다.

* SQL Server 인스턴스에 [TCP/IP 프로토콜](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)을 사용하도록 설정되어 있어야 합니다.

* 명명된 SQL Server 인스턴스를 운영하는 경우 [SQL Server 브라우저 서비스](../../tools/configuration-manager/sql-server-browser-service.md)가 실행되고 있어야 합니다.

* [서비스 허브 주문형 평가 필수 구성 요소](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents)에서 SQL Server 문서를 검토하세요.

## <a name="run-on-demand-sql-assessment"></a>주문형 SQL 평가 실행

1. SQL Server - Azure Arc 리소스를 열고 왼쪽 창에서 **환경 상태** 를 선택합니다.

   > [!div class="mx-imgBorder"]
   > [ ![SQL Server - Azure Arc 리소스의 환경 상태 화면을 보여 주는 스크린샷.](media/assess/sql-assessment-heading-sql-server-arc.png) ](media/assess/sql-assessment-heading-sql-server-arc.png#lightbox)

> [!IMPORTANT]
> MMA 확장이 설치되지 않은 경우에는 주문형 SQL 평가를 시작할 수 없습니다.

2. 계정 유형을 선택합니다. 관리되는 서비스 계정이 있는 경우 포털에서 직접 SQL 평가를 시작할 수 있습니다. 계정 이름을 지정합니다.

> [!NOTE]
> ‘관리되는 서비스 계정’을 지정하면 *CustomScriptExtension* 을 배포하여 포털에서 평가를 시작할 수 있도록 **SQL 평가 구성** 단추가 활성화됩니다. 한 번에 하나의 *CustomScriptExtension* 만 배포할 수 있으므로 실행 후 SQL 평가의 스크립트 확장이 자동으로 제거됩니다. 이미 또 다른 *CustomScriptExtension* 이 호스팅 머신에 배포된 경우 **SQL 평가 구성** 단추가 활성화되지 않습니다.

3. 기본값을 변경하려면 데이터 수집 머신에서 작업 디렉터리를 지정합니다. 기본적으로 `C:\sql_assessment\work_dir`가 사용됩니다. 수집 및 분석 중에 데이터가 해당 폴더에 임시로 저장됩니다. 폴더가 없으면 자동으로 생성됩니다.

4. **SQL 평가 구성** 을 클릭하여 포털에서 SQL 평가를 시작하면 표준 배포 거품이 표시됩니다.

> [!div class="mx-imgBorder"]
   > [ ![CustomScriptExtension의 배포를 보여 주는 스크린샷](media/assess/sql-assessment-custom-script-deployment.png) ](media/assess/sql-assessment-custom-script-deployment.png#lightbox)

5. 대상 머신에서 SQL 평가를 시작하는 것을 선호하는 경우 **구성 스크립트 다운로드** 를 클릭하고, 다운로드한 스크립트를 대상 머신에 복사하고, **powershell.exe** 의 관리 인스턴스에서 다음 코드 블록 중 하나를 실행합니다.

   * 도메인 계정:  사용자 계정 및 암호를 입력하라는 메시지가 표시됩니다.

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1'
      ```

   * MSA(관리 서비스 계정):

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1' -ManagedServiceAccountName <MSA account name>
      ```

> [!NOTE]
> 이 스크립트는 데이터 수집을 트리거하는 *SQLAssessment* 라는 작업을 예약합니다. 이 작업은 스크립트를 실행한 후 1시간 이내에 실행됩니다. 그런 다음 7일마다 반복됩니다.

> [!TIP]
> 작업을 다른 날짜 및 시간에 실행하도록 수정하거나 즉시 실행할 수도 있습니다. 작업 스케줄러 라이브러리에서 **Microsoft** > **Operations Management Suite** > **AOI\*\*\***  > **평가** > **SQLAssessment** 를 찾습니다.

## <a name="view-sql-assessment-results"></a>SQL 평가 결과 보기

* 환경 상태 창에서 **SQL 평가 결과 보기** 단추를 선택합니다.

   > [!NOTE]
   > Log Analytics에서 결과 준비될 때까지 **SQL 평가 결과 보기** 단추가 비활성화된 상태로 유지됩니다. 이 프로세스는 대상 컴퓨터에서 데이터 파일을 처리한 후 최대 2시간이 걸릴 수 있습니다.

   > [!div class="mx-imgBorder"]
   > [ ![SQL 평가 결과를 보여 주는 스크린샷.](media/assess/sql-assessment-results.png) ](media/assess/sql-assessment-results.png#lightbox)

* 작업 폴더에 있는 파일을 검사하여 수집 머신의 데이터 처리 상태를 확인할 수 있습니다. 예약된 작업이 완료되면 작업 디렉터리에 _new._ 접두사가 있는 파일이 여러 개 표시됩니다.

   > [!div class="mx-imgBorder"]
   > [ ![작업 폴더에 새 데이터 파일을 표시하는 파일 관리자 창을 보여 주는 스크린샷.](media/assess/sql-assessment-data-files-ready.png) ](media/assess/sql-assessment-data-files-ready.png#lightbox)

* Microsoft Monitoring Agent는 15분마다 작업 폴더를 검색합니다. 이 에이전트는 _new.*_ 파일을 찾아 데이터를 Log Analytics 작업 영역으로 보냅니다. MMA는 파일을 업로드한 후 접두사를 _new._ 에서 _processed._ 로 변경합니다.

   > [!div class="mx-imgBorder"]
   > ![처리된 데이터 파일을 표시하는 파일 관리자 창을 보여 주는 스크린샷.](media/assess/sql-assessment-data-files-processed.png)

## <a name="next-steps"></a>다음 단계

* [Services Hub 주문형 평가](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents)에서 필수 구성 요소 문서를 확인하여 추가 정보를 확인하세요.

* 주문형 SQL 평가 기능의 포괄적인 지원을 받으려면 프리미어 또는 통합 지원 구독이 필요합니다. 자세한 내용은 [Azure 프리미어 지원](https://azure.microsoft.com/support/plans/premier)을 참조하세요.
