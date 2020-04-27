---
title: 파워 쿼리 원본 | Microsoft Docs
description: SQL Server Integration Services 데이터 흐름에서 파워 쿼리 원본을 구성하는 방법 알아보기
ms.date: 12/27/2019
ms.prod: sql
ms.prod_service: integration-services
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.powerqueryconnmgr.f1
- sql13.ssis.designer.powerquerysource.queries.f1
- sql13.ssis.designer.powerquerysource.connmgrs.f1
- sql14.ssis.designer.powerqueryconnmgr.f1
- sql14.ssis.designer.powerquerysource.queries.f1
- sql14.ssis.designer.powerquerysource.connmgrs.f1
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: d164711a45b34b0974b2cca3d13fc216c378ed8b
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82087423"
---
# <a name="power-query-source-preview"></a>파워 쿼리 원본(미리 보기)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

이 문서에서는 SSIS(SQL Server Integration Services) 데이터 흐름에서 파워 쿼리 원본의 속성을 구성하는 방법에 대해 설명합니다. 파워 쿼리는 Excel/Power BI Desktop을 사용하여 다양한 데이터 원본에 연결하고 데이터를 변환할 수 있는 기술입니다. 자세한 내용은 [파워 쿼리 - 개요 및 학습](https://support.office.com/article/power-query-overview-and-learning-ed614c81-4b00-4291-bd3a-55d80767f81d) 문서를 참조하세요. 파워 쿼리에서 생성된 스크립트를 복사하여 SSIS 데이터 흐름의 파워 쿼리 원본에 붙여넣어 스크립트를 구성할 수 있습니다.
  
> [!NOTE]
> 현재 미리 보기 릴리스의 경우 파워 쿼리 원본은 ADF(Azure Data Factory)의 SQL Server 2017/2019 및 Azure-SSIS IR(Integration Runtime)에서만 사용할 수 있습니다. SQL Server 2017/2019용 최신 파워 쿼리 원본은 [여기](https://www.microsoft.com/download/details.aspx?id=100619)에서 다운로드하여 설치할 수 있습니다. Azure-SSIS IR용 파워 쿼리 원본이 미리 설치되어 있습니다. Azure-SSIS IR을 프로비전하려면 [ADF에서 SSIS 프로비전](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure) 문서를 참조하세요.

## <a name="configure-the-power-query-source"></a>파워 쿼리 원본 구성

SSDT에서 **파워 쿼리 원본 편집기**를 열려면 SSIS 도구 상자에서 데이터 흐름 디자이너로 **파워 쿼리 원본**을 끌어서 놓고 두 번 클릭합니다.  

![PQ 원본](media/power-query-source/pq-source.png)

세 개의 탭이 왼쪽에 표시됩니다. **쿼리** 탭의 드롭다운 메뉴에서 쿼리 모드를 선택할 수 있습니다.
-   **단일 쿼리** 모드를 사용하면 Excel/Power BI Desktop에서 단일 파워 쿼리 스크립트를 복사하여 붙여넣을 수 있습니다.
-   **변수의 단일 쿼리** 모드를 사용하면 실행할 쿼리를 포함하는 문자열 변수를 지정할 수 있습니다.

![PQ 원본 쿼리 탭 단일](media/power-query-source/pq-source-queries-tab-single.png)

**연결 관리자** 탭에서 데이터 원본 액세스 자격 증명이 포함된 파워 쿼리 연결 관리자를 추가하거나 제거할 수 있습니다. **데이터 원본 검색** 단추를 선택하면 쿼리에서 참조된 데이터 원본이 식별되고 적절한 기존 파워 쿼리 연결 관리자를 할당하거나 새 연결 관리자를 만들 수 있도록 데이터 원본이 나열됩니다.

![PQ 원본 연결 관리자 탭 검색](media/power-query-source/pq-source-connection-managers-tab-detect.png)

![PQ 원본 연결 관리자 탭 추가](media/power-query-source/pq-source-connection-managers-tab-add.png)

마지막으로 **열** 탭에서 출력 열 정보를 편집할 수 있습니다.

![PQ 원본 열 탭](media/power-query-source/pq-source-columns-tab.png)

## <a name="configure-the-power-query-connection-manager"></a>파워 쿼리 연결 관리자 구성

SSDT에서 파워 쿼리 원본을 사용하여 데이터 흐름을 디자인할 때 다음 방법으로 새 파워 쿼리 연결 관리자를 만들 수 있습니다.
- **추가**/**데이터 원본 검색** 단추를 선택하고 위에 설명된 대로 드롭다운 메뉴에서 **<New connection...>** 을 선택한 후 파워 쿼리 원본의 **연결 관리자** 탭에서 간접적으로 만듭니다.
- 패키지의 **연결 관리자** 패널을 마우스 오른쪽 단추로 클릭하고 드롭다운 메뉴에서 **새 연결...** 을 선택하여 직접적으로 만듭니다.

![PQ 원본 연결 관리자 패널 추가](media/power-query-source/pq-source-connection-managers-panel-add.png)

**SSIS 연결 관리자 추가** 대화 상자에서 연결 관리자 유형 목록에서 **PowerQuery**를 두 번 클릭합니다.

![PQ 원본 연결 관리자 패널 추가 대화 상자](media/power-query-source/pq-source-connection-managers-panel-add-dialog.png)

**파워 쿼리 연결 관리자 편집기**에서 **데이터 원본 종류**, **데이터 원본 경로** 및 **인증 종류**를 지정하고 적절한 액세스 자격 증명을 할당해야 합니다. **데이터 원본 종류**의 경우 현재 드롭다운 메뉴에서 22개 종류 중 하나를 선택할 수 있습니다.

![PQ 원본 연결 관리자 편집기 종류](media/power-query-source/pq-source-connection-manager-editor-kind.png)

**Oracle**, **DB2**, **MySQL**, **PostgreSQL**, **Teradata**, **Sybase**와 같은 일부 원본을 사용하려면 [파워 쿼리 필수 구성 요소](/power-bi/desktop-data-source-prerequisites) 문서에서 가져올 수 있는 ADO.NET 드라이버를 추가로 설치해야 합니다. 사용자 지정 설정 인터페이스를 사용하여 Azure-SSIS IR에 해당 드라이버를 설치할 수 있습니다. [Azure-SSIS IR 사용자 지정](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup) 문서를 참조하세요.

**데이터 원본 경로**의 경우 인증 정보 없이 연결 문자열을 형성하는 데이터 원본별 속성을 입력할 수 있습니다. 예를 들어 **SQL** 데이터 원본의 경로는 `<Server>;<Database>`로 형성됩니다. **편집** 단추를 선택하여 경로를 형성하는 데이터 원본별 속성에 값을 할당할 수 있습니다.

![PQ 원본 연결 관리자 편집기 경로](media/power-query-source/pq-source-connection-manager-editor-path.png)

마지막으로 **인증 종류**의 경우 드롭다운 메뉴에서 **익명**/**Windows 인증**/**사용자 이름 암호**/**키**를 선택하고, 적절한 액세스 자격 증명을 입력하고, **연결 테스트** 단추를 선택하여 파워 쿼리 원본이 제대로 구성되었는지 확인할 수 있습니다.

![PQ 원본 연결 관리자 편집기 인증](media/power-query-source/pq-source-connection-manager-editor-authentication.png)

### <a name="current-limitations"></a>현재 제한 사항

-   현재 Azure-SSIS IR에서는 Oracle ADO.NET 드라이버를 설치할 수 없어 **Oracle** 데이터 원본을 사용할 수 없으므로, 지금은 Oracle ODBC 드라이버를 대신 설치하고 **ODBC** 데이터 원본을 사용하여 Oracle에 연결하세요. [Azure-SSIS IR 사용자 지정](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup) 문서의 **ORACLE STANDARD ODBC** 예제를 참조하세요.

-   사용자 지정 설정으로 AZURE-SSIS IR에서 **웹** 데이터 원본을 사용할 수 없으므로, 지금은 사용자 지정 설정 없이 AZURE-SSIS IR에서 해당 데이터 원본을 사용하세요.

## <a name="next-steps"></a>다음 단계
ADF 파이프라인의 첫 번째 클래스 작업으로 Azure-SSIS IR에서 SSIS 패키지를 실행하는 방법에 대해 알아봅니다. [SSIS 패키지 작업 실행 런타임](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity) 문서를 참조하세요.
