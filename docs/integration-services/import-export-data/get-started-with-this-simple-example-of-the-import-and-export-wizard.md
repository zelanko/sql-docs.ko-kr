---
title: "이 간단한 예제 가져오기 및 내보내기 마법사의 시작 | Microsoft Docs"
ms.custom: 
ms.date: 02/15/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: ea3db39b-698b-4a74-8eb8-21dc7252dc1a
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 59c7e1cc3c31f77652acb21d375e1294bdc93397
ms.openlocfilehash: 9eee58be471d8b39b051c1343f9eb26a2960b6d6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="get-started-with-this-simple-example-of-the-import-and-export-wizard"></a>이 간단한 예제 가져오기 및 내보내기 마법사 시작
SQL Server 데이터베이스에는 Excel 스프레드시트에서 데이터를 가져오는-일반적인 시나리오를 통해 탐색 하 여 SQL Server 가져오기 및 내보내기 마법사에서 기대 하는 알아봅니다. 다른 원본 및 다른 위치를 사용 하려는 경우에이 항목에서는 대부분의 마법사를 실행 하는 방법에 대 한 알아야 해야 합니다.

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>필수 구성 요소-는 컴퓨터에 설치 하는 마법사?
마법사를 실행하려고 하지만 컴퓨터에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치되지 않은 경우 SSDT(SQL Server Data Tools)를 설치하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 설치할 수 있습니다. 자세한 내용은 [SSDT(SQL Server Data Tools) 다운로드](https://msdn.microsoft.com/library/mt204009.aspx)를 참조하세요.

## <a name="heres-the-excel-source-data-for-this-example"></a>다음은이 예제에 대 한 Excel 원본 데이터
-WizardWalkthrough.xlsx Excel 통합 문서의 WizardWalkthrough 워크시트의 작은 2 열 테이블을 복사 하려는 원본 데이터는 다음과 같습니다.

![Excel 원본 데이터](../../integration-services/import-export-data/media/excel-source-data.jpg)

## <a name="heres-the-sql-server-destination-database-for-this-example"></a>다음은이 예제에 대 한 SQL Server 대상 데이터베이스
여기 (SQL Server Management Studio)에 있는 원본 데이터를 복사 하려는 SQL Server 대상 데이터베이스가입니다. 대상 테이블에는 없는-마법사가 테이블을 만들 수 있도록 하려고 합니다.

![SQL Server 대상 데이터베이스](../../integration-services/import-export-data/media/sql-server-destination-database.jpg)

## <a name="step-1---start-the-wizard"></a>1 단계-마법사 시작
Windows 시작 메뉴에서 Microsoft SQL Server 2016 그룹에서 마법사를 시작 합니다.

![마법사를 시작 합니다.](../../integration-services/import-export-data/media/start-wizard.jpg)

> [!NOTE]
> 예를 들어 32 비트 버전의 Microsoft Office를 설치 해야 하므로 32 비트 마법사를 선택 합니다. 결과적으로, Excel에 연결 하는 32 비트 데이터 공급자를 사용 해야 합니다. 일반적으로 다른 많은 데이터 소스에 대 한 64 비트 마법사 중 선택할 수 있습니다.
>
> 64 비트 버전의 SQL Server 가져오기 및 내보내기 마법사를 사용 하려면 SQL Server를 설치 해야 합니다. SQL Server Data Tools (SSDT) 및 SQL Server Management Studio (SSMS)는 32 비트 응용 프로그램 및 32 비트 버전의 마법사를 포함 하 여 32 비트 파일을 설치 합니다.

자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사 시작](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)을 참조하세요.

## <a name="step-2---view-the-welcome-page"></a>2 단계-시작 페이지를 보려면
마법사의 첫 번째 페이지는 **시작** 페이지. 

하려는 경우이 페이지 다시 고 클릭 **이 시작 페이지를 다시 표시 안 함**합니다.

![마법사 시작](../../integration-services/import-export-data/media/welcome-to-the-wizard.jpg)

## <a name="step-3---pick-excel-as-your-data-source"></a>3 단계-데이터 원본으로 선택 Excel
다음 페이지에서 **데이터 원본을 선택**, 데이터 원본으로 Microsoft Excel을 선택 합니다. 그런 다음 Excel 파일 선택를 찾아봅니다. 마지막으로 파일을 만드는 데 있는 Excel 버전을 지정 합니다.

![Excel 데이터 원본 선택](../../integration-services/import-export-data/media/choose-the-excel-data-source.jpg)

Excel에 연결 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Excel 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)합니다. 마법사의이 페이지에 대 한 자세한 내용은 참조 하십시오. [데이터 원본을 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)합니다.

## <a name="step-4---pick-sql-server-as-your-destination"></a>4 단계-대상으로 SQL Server 선택
다음 페이지에서 **대상 선택**, SQL Server에 연결 하 여 대상을 선택 하 여 데이터 공급자 중 하나는 목록에 있는 것과 Microsoft SQL Server를 선택 합니다. 이 예제에서는 선택 된 **.NET Framework Data Provider for SQL Server**합니다.

페이지에는 공급자 속성의 목록이 표시 됩니다. 이들 중 대부분은 이해 하기 어려운 이름 및 생소 한 설정입니다. 다행히 엔터프라이즈 데이터베이스를 연결 하려면 일반적으로 제공 해야만 라는 세 가지의 정보. 다른 설정에 대 한 기본값을 무시할 수 있습니다.

|필수 정보|.NET framework Data Provider for SQL Server 속성|
|---|---|
|서버 이름|**데이터 원본**|
|인증 (로그인) 정보|**통합 보안**; 또는 **사용자 ID** 및 **암호**<br/>서버에서 데이터베이스의 드롭다운 목록을 보려는 경우 먼저 유효한 로그인 정보를 제공 해야 합니다.|
|데이터베이스 이름|**초기 카탈로그**|

![SQL Server 대상을 선택 합니다.](../../integration-services/import-export-data/media/choose-the-sql-server-destination.jpg)

SQL Server에 연결 하는 방법에 대 한 자세한 내용은 참조 하십시오. [SQL Server 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)합니다. 마법사의이 페이지에 대 한 자세한 내용은 참조 하십시오. [대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)합니다.

## <a name="step-5---copy-a-table-instead-of-writing-a-query"></a>5 단계-쿼리를 작성 하는 대신 테이블 복사
다음 페이지에서 **테이블 복사 또는 쿼리 지정**, 원본 데이터의 전체 테이블을 복사 하려면 되도록 지정 합니다. 복사할 데이터를 선택 하 여 SQL 언어의 쿼리를 작성 하려면 않으려는 합니다.

![테이블을 복사 하려면 지정 합니다.](../../integration-services/import-export-data/media/specify-to-copy-a-table.jpg)

마법사의이 페이지에 대 한 자세한 내용은 참조 하십시오. [테이블 복사 또는 쿼리 지정](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)합니다.

## <a name="step-6---pick-the-table-to-copy"></a>6 단계-복사할 테이블을 선택 합니다.
다음 페이지에서 **원본 테이블 및 뷰 선택**, 테이블 또는 데이터 원본에서 복사 하려는 테이블을 선택 합니다. 그런 다음 새로운 또는 기존 대상 테이블 각 선택 된 원본 테이블을 매핑합니다.

이 예제에서는 기본적으로 마법사가 매핑는 **WizardWalkthrough$** 워크시트에는 **소스** SQL Server 대상에 같은 이름의 새 테이블에는 열입니다. (Excel 통합 문서 포함 한 워크시트 합니다.)
-   원본 테이블의 이름에 달러 기호 ($)는 Excel 워크시트를 나타냅니다. (명명 된 범위에 Excel을 표시 이름 으로만.)
-   대상 테이블 아이콘 별 마법사 새 대상 테이블을 만들려면이 있음을 나타냅니다.

![이름 바꾸기) (이전 테이블을 선택 합니다.](../../integration-services/import-export-data/media/select-the-table-before-renaming.jpg)

싶을 달러 기호 ($)를 제거 하는 새 대상 테이블의 이름에서입니다.

![이름 바꾸기) (후 테이블을 선택 합니다.](../../integration-services/import-export-data/media/select-the-table-after-renaming.jpg)

마법사의이 페이지에 대 한 자세한 내용은 참조 하십시오. [원본 테이블 및 뷰 선택](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)합니다.

## <a name="optional-step-7---review-the-column-mappings"></a>선택적 단계 7-열 매핑을 검토합니다
나가기 전에 **원본 테이블 및 뷰 선택** 페이지에서 필요에 따라 클릭는 **매핑 편집** 버튼을 클릭은 **열 매핑** 대화 상자. 여기에 **매핑** 테이블을 새 대상 테이블의 열에 원본 워크시트의 열을 매핑할 마법사 어떻게 표시 합니다.

![열 매핑 보기](../../integration-services/import-export-data/media/view-column-mappings.jpg)

마법사의이 페이지에 대 한 자세한 내용은 참조 하십시오. [열 매핑](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)합니다.

## <a name="optional-step-8---review-the-create-table-statement"></a>선택적 단계 8-CREATE TABLE 문을 검토합니다
반면는 **열 매핑** 대화 상자가 열려 있으면 필요에 따라 클릭는 **SQL 편집** 버튼을 클릭은 **테이블 생성 SQL 문** 대화 상자. 표시는 **CREATE TABLE** 새 대상 테이블을 만드는 마법사에서 생성 하는 문입니다. 일반적으로 문을 변경 필요가 없습니다.

![CREATE TABLE 정보 보호 정책 보기](../../integration-services/import-export-data/media/view-create-table-statement.jpg)

마법사의이 페이지에 대 한 자세한 내용은 참조 하십시오. [테이블 생성 SQL 문](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)합니다.

## <a name="optional-step-9---preview-the-data-to-copy"></a>선택적 단계 9-복사할 데이터를 미리 보기
클릭 한 후 **확인** 를 닫으려면는 **테이블 생성 SQL 문** 대화 상자를 클릭 **확인** 를 다시는 **열 매핑** 다시 하는 대화 상자는 **원본 테이블 및 뷰 선택** 페이지. 필요에 따라 클릭는 **미리 보기** 데이터의 예를 보려면 단추 하는 마법사를 복사 하려고 합니다. 이 예제에서는 확인 찾습니다.

![복사할 데이터 미리 보기](../../integration-services/import-export-data/media/preview-data-to-copy.jpg)

마법사의이 페이지에 대 한 자세한 내용은 참조 하십시오. [데이터 미리 보기](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)합니다.

## <a name="step-10---yes-you-want-to-run-the-import-export-operation"></a>예-10 단계, 가져오기 내보내기 작업을 실행.
다음 페이지에서 **를 저장 하 고 패키지 실행**를 두면 **즉시 실행** 클릭 하면 되는 즉시 데이터를 복사 하도록 **마침** 다음 페이지에서. 클릭 하 여 다음 페이지를 건너뛸 수 있습니다 **마침** 에 **를 저장 하 고 패키지 실행** 페이지.

![패키지 실행](../../integration-services/import-export-data/media/run-the-package.jpg)

마법사의이 페이지에 대 한 자세한 내용은 참조 하십시오. [를 저장 하 고 패키지 실행](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)합니다.

## <a name="step-11---finish-the-wizard-and-run-the-import-export-operation"></a>11 단계-마법사를 완료 하 고 가져오기 내보내기 작업을 실행 합니다.
클릭 한 경우 **다음** 대신 **마침** 에 **를 저장 하 고 패키지 실행** 페이지의 다음 페이지에서 다음 **마법사를 완료**, 작업을 수행 하는 마법사는 상황 요약이 표시 합니다. 클릭 **마침** 가져오기 내보내기 작업을 실행 합니다.

![마법사 완료](../../integration-services/import-export-data/media/complete-the-wizard.jpg)

마법사의이 페이지에 대 한 자세한 내용은 참조 하십시오. [마법사를 완료](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)합니다.

## <a name="step-12---review-what-the-wizard-did"></a>12 단계-마법사의 않은 검토
마지막 페이지에서 감시 마법사에서 각 작업을 완료 한 다음 결과 검토 합니다. 강조 표시 된 줄 마법사 데이터를 성공적으로 복사 함을 나타냅니다. 완료 되!

![성공 마법사](../../integration-services/import-export-data/media/the-wizard-succeeded.jpg)

마법사의이 페이지에 대 한 자세한 내용은 참조 하십시오. [작업을 수행](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)합니다.

## <a name="heres-the-new-table-of-data-copied-to-sql-server"></a>다음은 새 데이터 테이블의 SQL Server로 복사
여기 (SQL Server Management Studio)에서 마법사는 SQL Server에서 생성 되는 새 대상 테이블을 참조 있습니다.

![SQL Server로 복사 되는 데이터](../../integration-services/import-export-data/media/data-copied-to-sql-server.jpg)

여기서 (SSMS)에서 다시 SQL Server로 복사 마법사는 데이터를 확인할 수 있습니다.

![SQL Server 2에 복사 된 데이터](../../integration-services/import-export-data/media/data-copied-to-sql-server-2.jpg)

## <a name="learn-more"></a>자세한 정보  
마법사의 작동 방식에 대해 자세히 알아보기
-   **마법사에 대해 자세히 알아보기** 마법사에 대한 개요를 살펴보려면 [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조하세요.

-   **마법사의 단계에 알아봅니다.** 마법사의 단계에 대 한 정보를 찾고 있는 경우 여기-목록에서 원하는 페이지를 선택 [SQL Server 가져오기 및 내보내기 마법사의 단계를](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)합니다. 마법사의 각 페이지에 대 한 설명서의 개별 페이지 이기도합니다.

-   **데이터 원본 및 대상에 연결 하는 방법을 알아봅니다.** 데이터에 연결 하는 방법에 대 한 정보를 찾고 있는 경우 여기-목록에서 원하는 페이지를 선택 [SQL Server 가져오기 및 내보내기 마법사와 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)합니다. 각 몇 가지 자주 사용 되는 데이터 원본에 대 한 설명서의 개별 페이지가 있습니다.



