---
title: 단일 컴퓨터에서 SSIS Scale Out 시작| Microsoft Docs
description: 이 문서에서는 단일 컴퓨터에서 SSIS Scale Out을 시작하려면 알아야 할 모든 것을 보여줍니다.
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.reviewer: maghan
ms.openlocfilehash: 48ed32fedde7d3874f01644eec257f4450e0555e
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919027"
---
# <a name="get-started-with-integration-services-ssis-scale-out-on-a-single-computer"></a>단일 컴퓨터에서 Integration Services(SSIS) Scale Out 시작

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


이 섹션에서는 단일 컴퓨터 환경에서 기본 설정을 사용하여 Integration Services Scale Out을 설정하는 방법을 안내합니다.

## <a name="1-install-sql-server-features"></a>1. SQL Server 기능 설치
SQL Server 설치 마법사의 **기능 선택** 페이지에서 다음 항목을 선택합니다.
-   데이터베이스 엔진 서비스
-   Integration Services
    -   Scale Out 마스터
    -   Scale Out 작업자

![기능 선택 목록의 앞부분](media/feature-select-onebox1.PNG)

![기능 선택 목록의 뒷부분](media/feature-select-onebox2.PNG)

**서버 구성** 페이지에서 **다음**을 클릭하여 기본 서비스 계정 및 시작 유형을 적용합니다.

**데이터베이스 엔진 구성** 페이지에서 **혼합 모드**를 선택하고 **현재 사용자 추가**를 클릭합니다. 

![엔진 구성](media/engine-config.PNG)

**Integration Services Scale Out 구성 - 마스터 노드** 및 **Integration Services Scale Out 구성 - 작업자 노드** 페이지에서 **다음**을 클릭하여 포트 및 인증서의 기본 설정을 적용합니다.

SQL Server 설치 마법사를 완료합니다.

## <a name="2-install-sql-server-management-studio"></a>2. SQL Server Management Studio를 설치합니다.

[SSMS(SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md)를 다운로드하고 설치합니다.

## <a name="3-enable-scale-out"></a>3. Scale Out을 사용하도록 설정
SSMS를 열고 로컬 Sql Server 인스턴스에 연결합니다.
개체 탐색기에서 **Integration Services 카탈로그**를 마우스 오른쪽 단추로 클릭하고 **카탈로그 만들기**를 선택합니다.

**카탈로그 만들기** 대화 상자에서 **이 서버를 SSIS Scale Out 마스터로 사용** 옵션이 기본적으로 선택됩니다.

## <a name="4-enable-a-scale-out-worker"></a>4. Scale Out 작업자를 사용하도록 설정
SSMS에서 **SSISDB**를 마우스 오른쪽 단추로 클릭하고 **Scale Out 관리**를 선택합니다. 

![Scale Out 관리](media/manage-scale-out.PNG)

Integration Services Scale Out 관리자 앱이 열립니다. 자세한 내용은 [Scale Out 관리자](integration-services-ssis-scale-out-manager.md)를 참조하세요.

Scale Out 작업자를 사용하도록 설정하려면 **작업자 관리자**로 전환하고 사용하도록 설정할 작업자를 선택합니다. 작업자는 기본적으로 사용하지 않도록 설정되어 있습니다. **작업자 사용**을 클릭하여 선택된 작업자를 사용하도록 설정합니다.

## <a name="5-run-packages-in-scale-out"></a>5. 규모 확장에서 패키지 실행
이제 Scale Out에서 SSIS 패키지를 실행할 준비가 완료되었습니다. 자세한 내용은 [Integration Services(SSIS) Scale Out에서 패키지 실행](run-packages-in-integration-services-ssis-scale-out.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
-   [Scale Out 관리자를 사용하여 Scale Out 작업자 추가](add-scale-out-worker.md).
