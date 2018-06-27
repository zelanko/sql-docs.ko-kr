---
title: SSMS를 사용하여 Azure에 SSIS 패키지 예약 | Microsoft Docs
description: SQL Server Management Studio(SSMS)에서 예약 명령을 사용하여 Azure SQL Database에 배포할 SSIS 패키지를 예약하는 방법을 설명합니다.
ms.date: 05/09/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.suite: sql
ms.custom: ''
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 89874258c7c8dd12e08ea9a37c6375257ef52c61
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35335827"
---
# <a name="schedule-the-execution-of-ssis-packages-deployed-in-azure-with-sql-server-management-studio-ssms"></a>SQL Server Management Studio(SSMS)를 사용하여 Azure에 배포된 SSIS 패키지 실행 예약

Azure SQL Database에 배포된 SSIS 패키지를 예약하려면 SQL Server Management Studio(SSMS)를 사용할 수 있습니다. 온-프레미스 SQL Server 및 SQL Database 관리되는 인스턴스(미리 보기)에는 고급 SSIS 작업 스케줄러인 SQL Server 에이전트 및 관리되는 인스턴스 에이전트가 각각 있습니다. 반면 SQL Database에는 기본 제공 고급 SSIS 작업 스케줄러가 없습니다. 이 아티클에 설명된 SSMS 기능은 SQL Database에 배포된 패키지를 예약하는 데 사용되는 SQL Server 에이전트가 유사한 기능을 제공하는 친숙한 사용자 인터페이스를 제공 합니다.

SQL Database를 사용하여 SSIS 카탈로그인 `SSISDB`를 호스팅하는 경우 이 SSMS 기능을 사용하여 SSIS 패키지를 예약하는 데 필요한 Data Factory 파이프라인, 활동 및 트리거를 생성할 수 있습니다. 나중에 Data Factory에서 이러한 개체를 선택적으로 편집하고 확장할 수 있습니다.

SSMS를 사용하여 패키지를 예약하면 SSIS에서 선택된 패키지의 이름 및 타임스탬프를 기준으로 이름이 지정된 세 개의 새로운 데이터 팩터리 개체를 자동으로 만듭니다. 예를 들어 SSIS 패키지 이름이 **MyPackage**일 경우 SSMS는 다음과 유사한 새로운 데이터 팩터리 개체를 만듭니다.

| Object | 속성 |
|---|---|
| 파이프라인 | **Pipeline_MyPackage_2018-05-08T09_00_00Z** |
| SSIS 패키지 작업 실행 | **Activity_MyPackage_2018-05-08T09_00_00Z** |
| 트리거 | **Trigger_MyPackage_2018-05-08T09_00_00Z** |
|||

## <a name="prerequisites"></a>사전 요구 사항

이 아티클에 설명된 기능을 사용하려면 SQL Server Management Studio 버전 17.7 이상이 필요합니다. SSMS의 최신 버전을 받으려면 [SSMS(SQL Server Management Studio) 다운로드](../../ssms/download-sql-server-management-studio-ssms.md)를 참조하세요.

## <a name="schedule-a-package-in-ssms"></a>SSMS에서 패키지 예약

1. SSMS의 개체 탐색기에서 SSISDB 데이터베이스, 폴더, 프로젝트, 패키지를 차례로 선택합니다. 패키지를 마우스 오른쪽 단추로 클릭하고 **예약**을 선택합니다.

    ![예약할 패키지를 선택합니다.](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image1-schedule.png)

2. **새 일정** 대화 상자가 열립니다. **새 일정** 대화 상자의 **일반** 페이지에서 새로 예약할 작업의 이름과 설명을 지정합니다.

    ![새 일정 대화 상자의 일반 페이지](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image2-new-schedule.png)

3. **새 일정** 대화 상자의 **패키지** 페이지에서 실행 시간 설정(옵션) 및 런타임 환경을 선택합니다.

    ![새 일정 대화 상자의 패키지 페이지](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image3-new-schedule2.png)

4. **새 일정** 대화 상자의 **일정** 페이지에서 빈도, 시간대 및 기간과 같은 일정 설정을 지정합니다.

    ![새 일정 대화 상자의 예약 페이지](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image4-new-schedule3.png)

5. **새 일정** 대화 상자에서 작업 생성을 완료하면 SSMS가 만드는 새로운 데이터 팩터리 개체에 대해 알려주는 확인 메시지가 나타납니다. 이 확인 대화 상자에서 **예**를 선택하면 Azure Portal에 새로운 데이터 팩터리 파이프라인이 열리고, 여기에서 검토하고 사용자 지정할 수 있습니다.

    ![새 일정 확인](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image5-confirmation.png)

6. 예약 트리거를 사용자 지정하려면 **트리거** 메뉴에서 **새로 만들기/편집**을 선택합니다.

    ![필요에 따라 새 파이프라인 편집](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image6-edit.png)

    **트리거 편집** 블레이드가 열리고 여기서 일정 옵션을 사용자 지정할 수 있습니다.

    ![트리거 편집](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image7-edit2.png)

## <a name="next-steps"></a>다음 단계

SSIS 패키지를 예약하는 다른 방법에 대해 알아보려면 [Azure에서 SSIS 패키지의 실행 예약](ssis-azure-schedule-packages.md)을 참조하세요.

Azure Data Factory 파이프라인, 활동 및 트리거에 대해 자세히 알아보려면 다음 아티클을 참조하세요.
-   [Azure Data Factory의 파이프라인 및 활동](https://docs.microsoft.com/azure/data-factory/concepts-pipelines-activities)
-   [Azure Data Factory의 파이프라인 실행 및 트리거](https://docs.microsoft.com/azure/data-factory/concepts-pipeline-execution-triggers)
