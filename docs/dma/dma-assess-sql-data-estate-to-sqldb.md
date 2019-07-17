---
title: Azure SQL Database로 마이그레이션할 SQL Server 데이터 자산을 준비 상태를 평가 | Microsoft Docs
description: Azure SQL Database로 마이그레이션에 대 한 SQL Server 데이터 자산을 마이그레이션하도록 Data Migration Assistant 사용 방법 알아보기
ms.custom: ''
ms.date: 07/16/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: jroth
ms.openlocfilehash: d317fb3f0c2227744318eeaead71514095afbdec
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68269385"
---
# <a name="assess-the-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql-database-using-the-data-migration-assistant"></a>Data Migration Assistant를 사용 하 여 Azure SQL Database로 마이그레이션할 SQL Server 데이터 자산을 준비 상태를 평가

SQL Server 인스턴스의 마이그레이션 수백 및 수천 개의 Azure SQL Database 서비스 (PaaS) 플랫폼을 제공 하는 데이터베이스에는 상당한 작업입니다. 가능한 한 프로세스를 간소화 하려면 마이그레이션에 대 한 상대 준비에 대 한 확신을 지정 해야 합니다. 좁혀야, 서버와 완벽 하 게 준비 되었거나, 마이그레이션을 준비 하기 위해 최소한의 노력 해야 하는 데이터베이스를 포함 하 여를 식별 용이 하 게 하 고 작업을 가속화 합니다.

활용에 대 한 단계별 지침을 제공 하는이 문서는 [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017) 준비 결과 요약 하 고에서 노출 하는 [Azure Migrate](https://portal.azure.com/?feature.customPortal=false#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview) 허브입니다.

## <a name="create-a-project-and-add-a-tool"></a>프로젝트를 만들고 도구 추가

Azure 구독에 새 Azure Migrate 프로젝트 설치 되며 다음 도구를 추가 합니다.

Azure Migrate 프로젝트를 검색, 평가 및 평가 또는 마이그레이션 중인 환경에서 수집 하는 마이그레이션 메타 데이터 저장에 사용 됩니다. 또한 검색 된 자산을 추적 하 고 평가 및 마이그레이션을 오케스트레이션 프로젝트를 사용 합니다.

1. 선택 된 Azure portal에 로그인 **모든 서비스**, 한 다음 Azure Migrate 검색 합니다.
2. 아래 **Services**를 선택 **Azure Migrate**합니다.

   ![Azure Migrate-서비스 선택](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-services.png)

3. 에 **개요** 페이지에서 **평가 데이터베이스 마이그레이션 및**합니다.

   ![Azure Migrate-평가 시작](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

4. **데이터베이스**아래에 있는 **Getting started**를 선택 **도구 추가**합니다.

   ![Azure Migrate-도구 추가](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tools.png)

5. 에 **마이그레이션 프로젝트** 탭 (리소스 그룹에서 만들 없는) 하는 경우 Azure 구독 및 리소스 그룹을 선택 합니다.
6. 아래 **프로젝트 세부 정보**, 프로젝트 이름과 프로젝트를 만들려고 할 수 있는 지리적 위치를 지정 합니다.

    ![Azure Migrate-추가 도구 대화 상자](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tool-dialog.png)

    이러한 지역에서 Azure Migrate 프로젝트를 만들 수 있습니다.

    | **Geography**  | **저장소 위치 지역** |
    | ------------- | ------------- |
    | 아시아 | 동남 아시아 또는 동남 아시아 |
    | Europe | 남부 유럽 또는 유럽 서 부 |
    | 영국 | 영국 남부 또는 영국 서 부 |
    | 미국 | 미국 중서부 또는 미국 서 부 2 |

    온-프레미스 Vm에서 수집 된 메타 데이터를 저장 하려면 프로젝트에 대해 지정 된 geography만 사용 됩니다. 실제 마이그레이션에 대 한 모든 대상 지역을 선택할 수 있습니다.

7. 선택 **다음**, 평가 도구를 추가 합니다.

   > [!NOTE]
   > 프로젝트를 만들 때 하나 이상의 평가 또는 마이그레이션 도구를 추가 해야 합니다.

8. 에 **선택 평가 도구** 탭을 **Azure Migrate: 데이터베이스 평가** 추가할 평가 도구로 나타납니다. 평가 도구는 현재 필요가 없는 경우 선택 합니다 **지금은 평가 도구를 추가 하지 않고 건너뛰거나** 확인란 합니다. **다음**을 선택합니다.

    ![Azure Migrate-선택 평가 도구 탭](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-assessment-tool.png)

9. 에 **선택 마이그레이션 도구** 탭을 **Azure Migrate: 데이터베이스 마이그레이션** 추가할 마이그레이션 도구로 나타납니다. 마이그레이션 도구를 현재 필요가 없는 경우 선택 합니다 **이제 마이그레이션 도구를 추가 하지 않고 건너뛰거나**합니다. **다음**을 선택합니다.

    ![Azure Migrate-선택 마이그레이션 도구 탭](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-migration-tool.png)

10. **검토 도구 추가 +** , 선택한 설정을 검토 **도구 추가**합니다.

    ![Azure Migrate-검토 + 도구 탭 추가](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-tools.png)

    프로젝트를 만든 후 서버 및 워크 로드, 데이터베이스 및 웹 앱의 마이그레이션하고 평가 위한 추가 도구를 선택할 수 있습니다.

## <a name="assess-and-upload-assessment-results"></a>평가 하 고 평가 결과 업로드 합니다.

성공적으로 만든 후 마이그레이션 프로젝트를 아래 **평가 도구**를 **Azure Migrate: 데이터베이스 평가** 상자를 다운로드 하 고 Data Migration Assistant 도구 표시 사용에 대 한 지침입니다.

   ![Azure Migrate-평가 도구 추가](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessment-tool-added.png)

1. Data Migration Assistant에서 제공 하는 링크를 사용 하 여 다운로드 하 고 원본 SQL Server 인스턴스에 대 한 액세스를 사용 하 여 컴퓨터에 설치 합니다.
2. Data Migration Assistant를 시작 합니다.

### <a name="create-an-assessment"></a>평가 만들기

1. 왼쪽에서 선택 합니다 **+** 아이콘을 선택한 후 평가 **프로젝트 형식**
2. 프로젝트 이름을 지정 하 고 원본 서버와 대상 서버 유형 중 하나를 선택 합니다.

    이상 버전의 SQL Server 또는 Azure VM에서 호스팅되는 SQL Server 온-프레미스 SQL Server 인스턴스를 업그레이드 하는 경우 원본 및 대상 서버 유형으로 설정 **SQL Server**합니다. 대상 서버 유형으로 설정 **Azure SQL Database Managed Instance** Azure SQL Database (PaaS) 대상 준비 상태 평가 대 한 합니다.

3. **만들기**를 선택합니다.

   ![Azure Migrate-Data Migration Assistant 인터페이스](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-interface.png)

### <a name="choose-assessment-options"></a>평가 옵션 선택

1. 보고서 유형을 선택 합니다.

    다음 보고서 유형 중 하나 또는 모두를 선택할 수 있습니다.
    * 데이터베이스 호환성 확인
    * 기능 패리티 확인

   ![Azure Migrate-Data Migration Assistant-평가 옵션 화면](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-options-screen.png)

2. **다음**을 선택합니다.

### <a name="add-databases-to-assess"></a>평가 하는 데이터베이스 추가

1. 선택 **소스 추가** 를 연결 플라이 아웃 메뉴를 엽니다.
2. SQL server 인스턴스 이름을 입력, 인증 유형을 선택, 올바른 연결 속성을 설정 및 선택한 **Connect**합니다.
3. 데이터베이스를 평가 하 고 선택한 선택 **추가**합니다.

   > [!NOTE]
   > Shift 또는 Ctrl 키를 누른 채로 누른 다음 원본을 제거 하는 동안 선택 하 여 여러 데이터베이스를 제거할 수 있습니다. 소스 추가 단추를 사용 하 여 여러 SQL Server 인스턴스에서 데이터베이스를 추가할 수 있습니다.

4. 선택 **다음** 평가를 시작 합니다.

   ![Azure Migrate-Data Migration Assistant-소스 선택 화면](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-select-sources-screen.png)

5. 평가가 완료 되 면 선택 **Azure Migrate 업로드할**합니다.

   ![Azure Migrate-Data Migration Assistant-검토 결과 화면](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-review-results-screen.png)

6. Azure Portal에 로그인합니다.

   ![Azure Migrate-Data Migration Assistant-검토 결과 화면](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-signin.png)

7. 평가 결과 업로드 하 여 선택한 구독 및 Azure Migrate 프로젝트를 선택 **업로드**합니다.

   평가 업로드 확인 될 때까지 기다립니다.

## <a name="view-target-readiness-assessment-results"></a>대상 준비 상태 평가 결과 보기

1. Azure portal에 로그인, Azure migrate에 대 한 검색 및 선택 **Azure Migrate**합니다.

   ![Azure 마이그레이션-Azure portal-서비스 검색](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-search.png)

2. 선택 **평가 데이터베이스 마이그레이션 및** 평가 결과 페이지로 이동 합니다.

   ![Azure Migrate-평가 결과 검토](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

    적합 한 마이그레이션 프로젝트는을 사용 하 여 다양 한 마이그레이션 프로젝트를 선택 하는 옵션을 변경 하는 고, 그렇지 해야 합니다 SQL Server 준비 상태 요약을 볼 수 있습니다.

    Azure 평가 결과 업데이트할 때마다 마이그레이션 프로젝트, Azure migrate 허브 모든 결과 통합 하 고 요약 보고서를 제공 합니다.  병렬로 여러 Data Migration Assistant 평가 실행 하 고 통합 된 준비 보고서를 가져오려면 단일 마이그레이션 프로젝트에 결과 업로드할 수 있습니다.

   ![Azure Migrate-준비 결과 검토](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-readiness.png)

    **데이터베이스 인스턴스를 평가**:  지금 평가 하는 SQL Server 인스턴스의 수입니다.
    **데이터베이스를 평가**: 평가 하는 하나 이상의 SQL Server 인스턴스 간에 평가 하는 데이터베이스의 총 **데이터베이스는 SQL DB에 대 한 준비**:  Azure SQL Database (PaaS)로 마이그레이션할 준비를 하는 데이터베이스의 수입니다.
    **Azure SQL VM에 대 한 데이터베이스 준비**:  데이터베이스 수 있지만 SQL Server Vm을 Azure로 마이그레이션할 준비를 하나 이상의 마이그레이션 블 로커를 Azure SQL Database (PaaS)을 구성 합니다.

3. 선택 **데이터베이스 인스턴스를 평가** SQL Server 인스턴스 수준 보기 페이지로 이동 합니다.

   ![Azure Migrate-검토 인스턴스 준비](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-instances.png)

    Azure SQL Database (PaaS)로 마이그레이션하는 각 SQL Server 인스턴스의 백분율 준비 상태를 찾을 수 있습니다.

4. 데이터베이스 준비 상태 보기를 이동 하려면 특정 인스턴스를 선택 합니다.

   ![Azure Migrate-검토 데이터베이스 준비](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-databases.png)

    마이그레이션 블 로커 각 데이터베이스당 위의 보기에서 각 데이터베이스 별로 권장 되는 대상의 수를 볼 수 있습니다.

5. 마이그레이션 블 로커를 해결 하는 자세한 내용을 보려면 DMA 평가 결과 검토 합니다.

   ![Azure Migrate-검토 마이그레이션 블 로커](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-migration-blockers.png)

## <a name="see-also"></a>참조

* [Data Migration Assistant (DMA)](../dma/dma-overview.md)
* [Data Migration Assistant: 구성 설정](../dma/dma-configurationsettings.md)
* [Data Migration Assistant: 모범 사례](../dma/dma-bestpractices.md)
