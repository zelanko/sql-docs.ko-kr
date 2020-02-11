---
title: SQL Server 준비를 평가 하 여 Azure SQL Database로 마이그레이션
titleSuffix: Data Migration Assistant
description: Data Migration Assistant를 사용 하 여 마이그레이션하기 위한 SQL Server 데이터 공간을로 마이그레이션하는 방법에 대해 알아봅니다 Azure SQL Database
ms.date: 12/19/2019
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
ms.custom: seo-lt-2019
ms.openlocfilehash: 6f9d3d97d939586683015f38ab17c00dd03ca122
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75253509"
---
# <a name="assess-the-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql-database-using-the-data-migration-assistant"></a>Data Migration Assistant를 사용 하 여 Azure SQL Database으로 마이그레이션하는 SQL Server 데이터 공간 준비 상태를 평가 합니다.

수백 개의 SQL Server 인스턴스와 수천 개의 데이터베이스를 Azure SQL Database으로 마이그레이션하는 것은 PaaS (Platform as a Service) 제품으로 서 상당한 작업을 합니다. 최대한 많은 프로세스를 간소화 하려면 마이그레이션에 대 한 상대적 준비 상태를 알고 있어야 합니다. 완전히 준비 되었거나 마이그레이션을 준비 하기 위해 최소한의 노력을 해야 하는 서버 및 데이터베이스를 포함 하 여 낮은 수준의 과일을 식별 합니다.

이 문서에서는 [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017) 를 활용 하 여 준비 결과를 요약 하 고 [Azure Migrate](https://portal.azure.com/?feature.customPortal=false#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview) 허브에 노출 하는 방법에 대 한 단계별 지침을 제공 합니다.

>
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Data-Migration-Assistant/player?WT.mc_id=dataexposed-c9-niner]

## <a name="create-a-project-and-add-a-tool"></a>프로젝트 만들기 및 도구 추가

Azure 구독에 새 Azure Migrate 프로젝트를 설정 하 고 도구를 추가 합니다.

Azure Migrate 프로젝트는 평가 하거나 마이그레이션하는 환경에서 수집 된 검색, 평가 및 마이그레이션 메타 데이터를 저장 하는 데 사용 됩니다. 또한 프로젝트를 사용 하 여 검색 된 자산을 추적 하 고 평가 및 마이그레이션을 오케스트레이션 합니다.

1. Azure Portal에 로그인 하 고 **모든 서비스**를 선택한 다음 Azure Migrate를 검색 합니다.
2. 
  **서비스** 아래에서 **Azure Migrate**를 선택합니다.

   ![Azure Migrate 서비스 선택](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-services.png)

3. **개요** 페이지에서 **데이터베이스 평가 및 마이그레이션**을 선택 합니다.

   ![Azure Migrate-평가 시작](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

4. **데이터베이스**의 **시작**에서 **도구 추가**를 선택 합니다.

   ![Azure Migrate 도구 추가](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tools.png)

5. **프로젝트 마이그레이션** 탭에서 Azure 구독 및 리소스 그룹을 선택 합니다 (리소스 그룹이 아직 없는 경우 새로 만듭니다).
6. 프로젝트 **세부 정보**아래에서 프로젝트 이름을 지정 하 고 프로젝트를 만들려는 지리를 지정 합니다.

    ![Azure Migrate-도구 추가 대화 상자](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tool-dialog.png)

    Azure Migrate 프로젝트는 다음 지역 중 하나에서 만들 수 있습니다.

    | **요인**  | **저장소 위치 영역** |
    | ------------- | ------------- |
    | 아시아 | 동남 아시아 또는 동아시아 |
    | 유럽 | 남부 유럽 또는 유럽 서부 |
    | 영국 | 영국 남부 또는 영국 서부 |
    | 미국 | 미국 중부 또는 미국 서 부 2 |

    프로젝트에 대해 지정된 지리는 온-프레미스 VM에서 수집된 메타데이터를 저장하는 데 사용됩니다. 실제 마이그레이션에 대한 대상 지역을 선택할 수 있습니다.

7. **다음**을 선택한 다음 평가 도구를 추가 합니다.

   > [!NOTE]
   > 프로젝트를 만들 때 하나 이상의 평가 또는 마이그레이션 도구를 추가 해야 합니다.

8. **평가 도구 선택** 탭에서 **Azure Migrate: 데이터베이스 평가** 가 추가할 평가 도구로 표시 됩니다. 현재 평가 도구가 필요 하지 않은 경우 **지금 평가 도구 추가 건너뛰기** 확인란을 선택 합니다. **다음**을 선택합니다.

    ![Azure Migrate 선택 평가 도구 탭](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-assessment-tool.png)

9. **마이그레이션 도구 선택** 탭의 **Azure Migrate: 데이터베이스 마이그레이션이** 추가할 마이그레이션 도구로 표시 됩니다. 현재 마이그레이션 도구가 필요 하지 않은 경우 **지금은 마이그레이션 도구 추가 건너뛰기**를 선택 합니다. **다음**을 선택합니다.

    ![Azure Migrate-마이그레이션 도구 탭 선택](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-migration-tool.png)

10. **검토 + 도구 추가**에서 설정을 검토 하 고 **추가 도구**를 선택 합니다.

    ![Azure Migrate-검토 + 도구 추가 탭](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-tools.png)

    프로젝트를 만든 후에는 서버와 작업, 데이터베이스 및 웹 앱의 평가 및 마이그레이션을 위한 추가 도구를 선택할 수 있습니다.

## <a name="assess-and-upload-assessment-results"></a>평가 결과 평가 및 업로드

마이그레이션 프로젝트를 성공적으로 만든 후 **평가 도구**의 **Azure Migrate: 데이터베이스 평가** 상자에서 Data Migration Assistant 도구를 다운로드 하 고 사용 하는 방법에 대 한 지침을 표시 합니다.

   ![Azure Migrate-평가 도구가 추가 됨](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessment-tool-added.png)

1. 제공 된 링크를 사용 하 여 Data Migration Assistant를 다운로드 한 다음 원본 SQL Server 인스턴스에 액세스할 수 있는 컴퓨터에 설치 합니다.
2. Data Migration Assistant를 시작 합니다.

### <a name="create-an-assessment"></a>평가 만들기

1. 왼쪽에서 **+** 아이콘을 선택한 다음 평가 **프로젝트 형식을** 선택 합니다.
2. 프로젝트 이름을 지정 하 고 원본 서버 및 대상 서버 유형을 선택 합니다.

    온-프레미스 SQL Server 인스턴스를 SQL Server의 이후 버전으로 업그레이드 하는 경우 또는 Azure VM에서 호스트 되는 SQL Server 원본 및 대상 서버 유형을 **SQL Server**로 설정 합니다. 대상 서버 유형을 PaaS (Azure SQL Database) 대상 준비 평가에 **Azure SQL Database Managed Instance** 로 설정 합니다.

3. **만들기**를 선택합니다.

   ![Azure Migrate-Data Migration Assistant 인터페이스](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-interface.png)

### <a name="choose-assessment-options"></a>평가 옵션 선택

1. 보고서 유형을 선택 합니다.

    다음 보고서 유형 중 하나 또는 둘 다를 선택할 수 있습니다.
    * 데이터베이스 호환성 확인
    * 기능 패리티 확인

   ![Azure Migrate-Data Migration Assistant 평가 옵션 화면](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-options-screen.png)

2. **다음**을 선택합니다.

### <a name="add-databases-to-assess"></a>평가할 데이터베이스 추가

1. **원본 추가** 를 선택 하 여 연결 플라이 아웃 메뉴를 엽니다.
2. SQL server 인스턴스 이름을 입력 하 고 인증 유형을 선택한 다음 올바른 연결 속성을 설정 하 고 **연결**을 선택 합니다.
3. 평가할 데이터베이스를 선택 하 고 **추가**를 선택 합니다.

   > [!NOTE]
   > Shift 또는 Ctrl 키를 누른 채 원본 제거를 클릭 하 여 여러 데이터베이스를 선택 하 여 제거할 수 있습니다. 소스 추가 단추를 사용 하 여 여러 SQL Server 인스턴스에서 데이터베이스를 추가할 수도 있습니다.

4. **다음** 을 선택 하 여 평가를 시작 합니다.

   ![Azure Migrate-Data Migration Assistant 소스 선택 화면](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-select-sources-screen.png)

5. 평가가 완료 되 면 **Azure Migrate 업로드를**선택 합니다.

   ![Azure Migrate-Data Migration Assistant-결과 검토 화면](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-review-results-screen.png)

6. Azure 포털에 로그인합니다.

   ![Azure Migrate-Data Migration Assistant-결과 검토 화면](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-signin.png)

7. 평가 결과를 업로드 하려는 구독 및 Azure Migrate 프로젝트를 선택 하 고 **업로드**를 선택 합니다.

   평가 업로드 확인이 완료 될 때까지 기다립니다.

## <a name="view-target-readiness-assessment-results"></a>대상 준비 평가 결과 보기

1. Azure Portal에 로그인 하 고, Azure 마이그레이션을 검색 하 고, 선택 **Azure Migrate**합니다.

   ![Azure Migrate-Azure Portal 서비스 검색](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-search.png)

2. 평가 **및 마이그레이션 데이터베이스** 를 선택 하 여 평가 결과를 가져옵니다.

   ![Azure Migrate-평가 결과 검토](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

    SQL Server 준비 요약을 볼 수 있습니다. 올바른 마이그레이션 프로젝트에 있는지 확인 하 고, 그렇지 않은 경우 변경 옵션을 사용 하 여 다른 마이그레이션 프로젝트를 선택 합니다.

    평가 결과를 Azure 마이그레이션 프로젝트로 업데이트할 때마다 Azure 마이그레이션 허브는 모든 결과를 통합 하 고 요약 보고서를 제공 합니다.  여러 Data Migration Assistant 평가를 병렬로 실행 하 고 결과를 단일 마이그레이션 프로젝트에 업로드 하 여 통합 된 준비 보고서를 가져올 수 있습니다.

   ![Azure Migrate-준비 결과 검토](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-readiness.png)

    **평가 된 데이터베이스 인스턴스**: 지금까지 평가한 SQL Server 인스턴스 수입니다.
    **평가 된 데이터베이스**: 하나 이상의 SQL Server 인스턴스에서 평가 된 데이터베이스의 총 수입니다. **SQL DB에 대해 준비 된 데이터베이스**: PaaS (Azure SQL Database로 마이그레이션할 준비가 된 데이터베이스 수).
    **AZURE SQL VM에 대해 준비 된 데이터베이스**: 데이터베이스 수는 PaaS (Azure SQL Database)로 하나 이상의 마이그레이션 차단기를 구성 했지만 Azure SQL Server vm으로 마이그레이션할 준비가 되었습니다.

3. SQL Server 인스턴스 수준 뷰로 가져올 **평가 데이터베이스 인스턴스** 를 선택 합니다.

   ![Azure Migrate-인스턴스 준비 검토](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-instances.png)

    Azure SQL Database (PaaS)로 마이그레이션하는 각 SQL Server 인스턴스의 준비 상태를 확인할 수 있습니다.

4. 데이터베이스 준비 뷰로 가져올 특정 인스턴스를 선택 합니다.

   ![Azure Migrate-데이터베이스 준비 상태 검토](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-databases.png)

    위의 보기에서 각 데이터베이스당 권장 대상인 각 데이터베이스당 마이그레이션 차단기 수를 확인할 수 있습니다.

5. DMA 평가 결과를 검토 하 여 마이그레이션 차단기에 대 한 자세한 내용을 확인 하세요.

   ![Azure Migrate-마이그레이션 차단기 검토](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-migration-blockers.png)

## <a name="see-also"></a>참고 항목

* [Data Migration Assistant(DMA)](../dma/dma-overview.md)
* [Data Migration Assistant: 구성 설정](../dma/dma-configurationsettings.md)
* [Data Migration Assistant: 모범 사례](../dma/dma-bestpractices.md)
