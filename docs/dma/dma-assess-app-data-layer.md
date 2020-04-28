---
title: Data Migration Assistant를 사용 하 여 응용 프로그램의 데이터 액세스 계층 평가
description: Data Migration Assistant를 사용 하 여 응용 프로그램의 데이터 액세스 계층을 평가 하는 방법을 알아봅니다.
ms.date: 01/23/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: 24763f190172da637d19df7ce36553b7341bd894
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "76761987"
---
# <a name="assess-an-apps-data-access-layer-with-data-migration-assistant"></a>Data Migration Assistant를 사용 하 여 응용 프로그램의 데이터 액세스 계층 평가

응용 프로그램은 일반적으로 데이터베이스에 연결 하 여 데이터를 유지 합니다. 응용 프로그램의 데이터 액세스 계층은이 데이터에 대 한 간편한 액세스를 제공 합니다. DMA (Data Migration Assistant)를 사용 하 여 사용자가 데이터베이스 및 관련 개체를 평가할 수 있습니다. 최신 버전의 DMA (v 5.0)에서는 응용 프로그램 코드에서 데이터베이스 연결 및 포함 된 SQL 쿼리를 분석 하는 기능이 도입 되었습니다.

아래 c # 코드 세그먼트를 살펴보세요.

![샘플 c # 코드 세그먼트](../dma/media/dma-assess-app-data-layer/dma-sample-c-sharp-code-segment.png)

이 경우 응용 프로그램이 SQL 쿼리를 사용 하 여 직원의 이름을 가져오는 것을 볼 수 있습니다.

![샘플 c # 코드 세그먼트 세부 정보](../dma/media/dma-assess-app-data-layer/dma-sample-c-sharp-code-detail.png)

응용 프로그램 소유자는 응용 프로그램에서 연결할 수 있는 다양 한 데이터베이스와 응용 프로그램의 데이터 액세스 계층에 포함 된 쿼리를 식별할 수 있어야 합니다. 또한 응용 프로그램을 Azure Data services로 현대화 하는 데 필요한 변경 사항을 확인 해야 합니다.

## <a name="assess-an-app-with-data-access-migration-toolkit"></a>데이터 액세스 마이그레이션 도구 키트를 사용 하 여 앱 평가

이 평가를 사용 하도록 설정 하기 위해 최근에 DAMT (Data Access Migration Toolkit) Visual Studio Code 확장을 도입 했습니다. 이 확장 (v 0.2)의 최신 버전은 .Net 응용 프로그램 및 T-sql 언어에 대 한 지원을 추가 합니다.

1. [여기](https://code.visualstudio.com/download)에서 VS Code를 다운로드 하 여 설치 합니다.
2. 확장 Marketplace에서 [Data Access Migration Toolkit 확장](https://marketplace.visualstudio.com/items?itemName=ms-databasemigration.data-access-migration-toolkit) 을 사용 하도록 설정 합니다.

   ![데이터 액세스 마이그레이션 도구 키트 확장 페이지](../dma/media/dma-assess-app-data-layer/dma-damt-extension-page.png)

3. Visual Studio Code에서 응용 프로그램 프로젝트를 엽니다.

   ![Visual Studio Code의 응용 프로그램 프로젝트](../dma/media/dma-assess-app-data-layer/dma-app-project-in-vscode.png)

4. 확장 콘솔 (Ctrl-Shft-P)을 시작한 다음 **데이터 액세스: 작업 영역 분석** 명령을 실행 합니다.

   ![Visual Studio Code 확장 콘솔](../dma/media/dma-assess-app-data-layer/dma-vscode-extension-console.png)

5. SQL Server 언어를 선택 합니다.

   ![SQL Server 언어 선택](../dma/media/dma-assess-app-data-layer/dma-sql-server-dialect.png)

   분석의 끝 부분에서 명령은 SQL 연결 명령 및 쿼리 보고서를 생성 합니다.

   ![데이터 액세스 보고서](../dma/media/dma-assess-app-data-layer/dma-data-access-report.png)

6. 강조 표시 된 데이터 연결 구성 요소 및 응용 프로그램 코드에 포함 된 SQL 쿼리에 대 한 보고서를 검토 합니다.

   ![응용 프로그램 코드의 SQL 쿼리](../dma/media/dma-assess-app-data-layer/dma-sql-queries-in-app-code.png)

   이러한 쿼리는 대상 SQL 플랫폼을 기반으로 하는 호환성 및 기능 패리티 문제에 대해 DMA를 통해 분석할 수 있습니다.

7. 응용 프로그램의 데이터 계층을 평가 하려면 보고서를 json 파일로 내보냅니다.

   ![. json 파일 내보내기](../dma/media/dma-assess-app-data-layer/dma-json-file-export.png)

   이 경우 생성 된 파일은 다음과 같습니다.

   ![Json 파일의 내용 보기](../dma/media/dma-assess-app-data-layer/dma-json-file-contents.png)

   Data Migration Assistant를 사용 하면 데이터베이스를 Azure 데이터 플랫폼으로 현대화 컨텍스트 내에서 응용 프로그램에 식별 된 쿼리를 평가할 수 있습니다.

8. Data Migration Assistant를 시작 하 고 평가 프로젝트를 만듭니다.

   ![새 평가 프로젝트 Data Migration Assistant](../dma/media/dma-assess-app-data-layer/dma-new-assessment-project.png)

9. 원본 SQL Server 인스턴스를 선택 합니다.

   ![Data Migration Assistant SQL Server 소스 선택](../dma/media/dma-assess-app-data-layer/dma-select-sql-source.png)

10. 응용 프로그램이 연결 되는 데이터베이스를 선택 합니다.

    ![데이터 액세스 마이그레이션 응용 프로그램 데이터베이스 선택](../dma/media/dma-assess-app-data-layer/dma-select-app-database.png)

    데이터 액세스 평가를 용이 하 게 하기 위해 DMA는 응용 프로그램 쿼리에 json 파일을 포함 하는 기능을 도입 합니다. 이제 응용 프로그램 쿼리를 사용 하 여 이전에 만든 json 파일을 포함 합니다.

11. 데이터베이스를 선택 하 고 데이터 액세스 마이그레이션 도구 키트에서 내보낸 json 파일로 이동 하 여 평가에 대 한 응용 프로그램의 쿼리를 포함 합니다.

    ![Json 파일에서 DMAT Data Migration Assistant](../dma/media/dma-assess-app-data-layer/dma-open-damt-json-file.png)

12. 평가를 시작 합니다.

    ![Data Migration Assistant 시작 평가](../dma/media/dma-assess-app-data-layer/dma-start-assessment.png)

13. 평가 보고서를 검토 합니다. 생성 된 보고서에는 아래와 같이 응용 프로그램 쿼리에서 검색 된 호환성 또는 기능 패리티 문제가 포함 됩니다.

    ![Data Migration Assistant 평가 보고서](../dma/media/dma-assess-app-data-layer/dma-assessment-report.png)

이제 마이그레이션의 데이터베이스 관점 뿐만 아니라 사용자도 응용 프로그램 관점에서 볼 수 있습니다.

## <a name="see-also"></a>참고 항목

* [Data Migration Assistant 개요](../dma/dma-overview.md)
* [Data Migration Assistant: 구성 설정](../dma/dma-configurationsettings.md)
* [Data Migration Assistant: 모범 사례](../dma/dma-bestpractices.md)
* [데이터 액세스 마이그레이션 도구 키트](https://marketplace.visualstudio.com/items?itemName=ms-databasemigration.data-access-migration-toolkit)