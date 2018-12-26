---
title: 가져오기 및 내보내기 마법사의 간단한 예제 시작 | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: quickstart
ms.assetid: ea3db39b-698b-4a74-8eb8-21dc7252dc1a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8440c6111152988afaa96f8b9c2415a5055819c7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696231"
---
# <a name="get-started-with-this-simple-example-of-the-import-and-export-wizard"></a>가져오기 및 내보내기 마법사의 간단한 예제 시작
Excel 스프레드시트에서 SQL Server 데이터베이스로 데이터를 가져오는 일반적인 시나리오를 살펴봄으로써 SQL Server 가져오기 및 내보내기 마법사에서 기대할 수 있는 작업을 알아봅니다. 다른 원본과 대상을 사용하려는 경우에도 이 항목에서는 마법사를 실행하는 방법에 대해 알아야 할 사항을 대부분 보여 줍니다.

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>필수 구성 요소 - 컴퓨터에 마법사가 설치되어 있습니까?
마법사를 실행하려고 하지만 컴퓨터에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치되지 않은 경우 SSDT(SQL Server Data Tools)를 설치하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 설치할 수 있습니다. 자세한 내용은 [SSDT(SQL Server Data Tools) 다운로드](https://msdn.microsoft.com/library/mt204009.aspx)를 참조하세요.

## <a name="heres-the-excel-source-data-for-this-example"></a>이 예의 Excel 원본 데이터
WizardWalkthrough.xlsx Excel 통합 문서의 WizardWalkthrough 워크시트에 복사할 원본 데이터(2개 열의 작은 테이블)는 다음과 같습니다.

![Excel 원본 데이터](../../integration-services/import-export-data/media/excel-source-data.jpg)

## <a name="heres-the-sql-server-destination-database-for-this-example"></a>이 예의 SQL Server 대상 데이터베이스
SQL Server Management Studio에서 원본 데이터를 복사할 SQL Server 대상 데이터베이스는 다음과 같습니다. 대상 테이블이 없으며, 마법사에서 테이블을 만들도록 합니다.

![SQL Server 대상 데이터베이스](../../integration-services/import-export-data/media/sql-server-destination-database.jpg)

## <a name="step-1---start-the-wizard"></a>1단계 - 마법사 시작
Windows 시작 메뉴의 Microsoft SQL Server 2016 그룹에서 마법사를 시작합니다.

![마법사 시작](../../integration-services/import-export-data/media/start-wizard.jpg)

> [!NOTE]
> 이 예에서는 32비트 버전의 Microsoft Office가 설치되어 있으므로 32비트 마법사를 선택합니다. 결과적으로 32비트 데이터 공급자를 사용하여 Excel에 연결해야 합니다. 다른 많은 데이터 원본에서는 일반적으로 64비트 마법사를 선택할 수 있습니다.
>
> 64비트 버전의 SQL Server 가져오기 및 내보내기 마법사를 사용하려면 SQL Server를 설치해야 합니다. SSDT(SQL Server Data Tools) 및 SSMS(SQL Server Management Studio)는 32비트 애플리케이션이며, 32비트 버전의 마법사를 포함하여 32비트 파일만 설치합니다.

자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사 시작](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)을 참조하세요.

## <a name="step-2---view-the-welcome-page"></a>2단계 - 시작 페이지 보기
마법사의 첫 페이지는 **시작** 페이지입니다. 

이 페이지가 다시 표시되지 않도록 하려면 **이 시작 페이지를 다시 표시 안 함**을 클릭하고 계속 진행합니다.

![마법사 시작](../../integration-services/import-export-data/media/welcome-to-the-wizard.jpg)

## <a name="step-3---pick-excel-as-your-data-source"></a>3단계 - 데이터 원본으로 Excel 선택
다음 페이지의 **데이터 원본 선택**에서 Microsoft Excel을 데이터 원본으로 선택합니다. 그런 다음 Excel 파일을 찾아서 선택합니다. 마지막으로 파일을 만드는 데 사용한 Excel 버전을 지정합니다.

> [!IMPORTANT]
> Excel 파일 연결 및 Excel 파일에서 데이터를 로드할 때 제한 사항 및 알려진 문제에 대한 자세한 내용은 [SSIS(SQL Server Integration Services)를 통해 Excel로 데이터 로드](../load-data-to-from-excel-with-ssis.md)를 참조하세요.

![Excel 데이터 원본 선택](../../integration-services/import-export-data/media/choose-the-excel-data-source.jpg)

마법사의 이 페이지에 대한 자세한 내용은 [데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)을 참조하세요.

## <a name="step-4---pick-sql-server-as-your-destination"></a>4단계 - 대상으로 SQL Server 선택
다음 페이지의 **대상 선택**에서 SQL Server에 연결하는 목록에서 데이터 공급자 중 하나를 선택하여 Microsoft SQL Server를 대상으로 선택합니다. 이 예에서는 **.Net Framework Data Provider for SQL Server**를 선택합니다.

페이지에는 공급자 속성 목록이 표시됩니다. 이러한 속성 중 대부분은 이해하기 어려운 이름이거나 생소한 설정입니다. 다행히도 엔터프라이즈 데이터베이스에 연결하려면 일반적으로 세 가지 정보만 제공해야 합니다. 다른 설정의 기본값은 무시할 수 있습니다.

|필수 정보|.NET Framework Data Provider for SQL Server 속성|
|---|---|
|서버 이름|**데이터 원본**|
|인증(로그인) 정보|**통합 보안** 또는 **사용자 ID**/**암호**<br/>서버에 있는 데이터베이스의 드롭다운 목록을 보려면 먼저 유효한 로그인 정보를 제공해야 합니다.|
|데이터베이스 이름|**초기 카탈로그**|

![SQL Server 대상 선택](../../integration-services/import-export-data/media/choose-the-sql-server-destination.jpg)

SQL Server 연결에 대한 자세한 내용은 [SQL Server 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)을 참조하세요. 마법사의 이 페이지에 대한 자세한 내용은 [대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)을 참조하세요.

## <a name="step-5---copy-a-table-instead-of-writing-a-query"></a>5단계 - 쿼리를 작성하는 대신 테이블 복사
다음 페이지의 **테이블 복사 또는 쿼리 지정**에서 원본 데이터의 전체 테이블을 복사하도록 지정합니다. SQL 언어로 쿼리를 작성하여 복사할 데이터를 선택하지 않으려고 합니다.

![테이블을 복사하도록 지정](../../integration-services/import-export-data/media/specify-to-copy-a-table.jpg)

마법사의 이 페이지에 대한 자세한 내용은 [테이블 복사 또는 쿼리 지정](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)을 참조하세요.

## <a name="step-6---pick-the-table-to-copy"></a>6단계 - 복사할 테이블 선택
다음 페이지의 **원본 테이블 및 뷰 선택**에서 데이터 원본에서 복사할 테이블을 선택합니다. 그런 다음 선택한 각 원본 테이블을 새 대상 테이블 또는 기존 대상 테이블에 맵핑합니다.

이 예에서 마법사는 기본적으로 **원본** 열의 **WizardWalkthrough$** 워크시트를 SQL Server 대상에 있는 동일한 이름의 새 테이블에 매핑했습니다. (Excel 통합 문서에는 하나의 워크시트만 있습니다.)
-   원본 테이블의 이름에 있는 달러($) 기호는 Excel 워크시트를 나타냅니다. (Excel에서 명명된 범위는 이름만으로 표시됩니다.)
-   대상 테이블 아이콘의 별은 마법사에서 새 대상 테이블을 만들 것임을 나타냅니다.

![테이블 선택(이름 변경 전)](../../integration-services/import-export-data/media/select-the-table-before-renaming.jpg)

새 대상 테이블의 이름에서 달러($) 기호를 제거하려고 합니다.

![테이블 선택(이름 변경 후)](../../integration-services/import-export-data/media/select-the-table-after-renaming.jpg)

마법사의 이 페이지에 대한 자세한 내용은 [원본 테이블 및 뷰 선택](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)을 참조하세요.

## <a name="optional-step-7---review-the-column-mappings"></a>7단계(선택 사항) - 열 매핑 검토
**원본 테이블 및 뷰 선택** 페이지를 나가기 전에 필요에 따라 **매핑 편집** 단추를 클릭하여 **열 매핑** 대화 상자를 엽니다. 여기의 **매핑** 테이블에서 마법사가 원본 워크시트의 열을 새 대상 테이블의 열에 매핑하는 방법을 보여 줍니다.

![열 매핑 보기](../../integration-services/import-export-data/media/view-column-mappings.jpg)

마법사의 이 페이지에 대한 자세한 내용은 [열 매핑](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)을 참조하세요.

## <a name="optional-step-8---review-the-create-table-statement"></a>8단계(선택 사항) - CREATE TABLE 문 검토
**열 매핑** 대화 상자가 열려있는 동안 필요에 따라 **SQL 편집** 단추를 클릭하여 **테이블 생성 SQL 문** 대화 상자를 엽니다. 마법사에서 생성한 **CREATE TABLE** 문을 확인하여 새 대상 테이블을 만듭니다. 명령문은 일반적으로 변경할 필요가 없습니다.

![CREATE TABLE 문 보기](../../integration-services/import-export-data/media/view-create-table-statement.jpg)

마법사의 이 페이지에 대한 자세한 내용은 [테이블 생성 SQL 문](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)을 참조하세요.

## <a name="optional-step-9---preview-the-data-to-copy"></a>9단계(선택 사항) - 복사할 데이터 미리 보기
**확인**을 클릭하여 **테이블 생성 SQL 문** 대화 상자를 닫은 다음 **확인**을 다시 클릭하여 **열 매핑** 대화 상자를 닫으면 **원본 테이블 및 뷰 선택** 페이지로 돌아갑니다. 필요에 따라 **미리 보기** 단추를 클릭하여 마법사에서 복사할 데이터의 샘플을 볼 수 있습니다. 이 예에서는 괜찮아 보입니다.

![복사할 데이터 미리 보기](../../integration-services/import-export-data/media/preview-data-to-copy.jpg)

마법사의 이 페이지에 대한 자세한 내용은 [데이터 미리 보기](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)를 참조하세요.

## <a name="step-10---yes-you-want-to-run-the-import-export-operation"></a>10단계 - 가져오기 및 내보내기 작업 실행 지정
후속 페이지에서 **마침**을 클릭하는 즉시 데이터를 복사할 수 있도록 다음 페이지의 **패키지 저장 및 실행**에서 **즉시 실행**이 선택된 채로 그대로 둡니다. 또는 **패키지 저장 및 실행** 페이지에서 **마침**을 클릭하여 다음 페이지를 건너뛸 수 있습니다.

![패키지 실행](../../integration-services/import-export-data/media/run-the-package.jpg)

마법사의 이 페이지에 대한 자세한 내용은 [패키지 저장 및 실행](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)을 참조하세요.

## <a name="step-11---finish-the-wizard-and-run-the-import-export-operation"></a>11단계 - 마법사 완료 및 가져오기/내보내기 작업 실행
**패키지 저장 및 실행** 페이지에서 **마침** 대신 **다음**을 클릭한 경우 다음 페이지의 **마법사 완료**에서 마법사에서 수행할 작업에 대한 요약이 표시됩니다. **마침**을 클릭하여 가져오기/내보내기 작업을 실행합니다.

![마법사 완료](../../integration-services/import-export-data/media/complete-the-wizard.jpg)

마법사의 이 페이지에 대한 자세한 내용은 [마법사 완료](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)를 참조하세요.

## <a name="step-12---review-what-the-wizard-did"></a>12단계 - 마법사에서 수행한 작업 검토
마지막 페이지에서 마법사가 각 작업을 완료하는 것을 지켜본 다음 결과를 검토합니다. 강조 표시된 줄은 마법사에서 데이터를 성공적으로 복사했음을 나타냅니다. 완료했습니다!

![성공적으로 완료된 마법사](../../integration-services/import-export-data/media/the-wizard-succeeded.jpg)

마법사의 이 페이지에 대한 자세한 내용은 [작업 수행](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)을 참조하세요.

## <a name="heres-the-new-table-of-data-copied-to-sql-server"></a>SQL Server에 복사된 새 데이터 테이블
SQL Server Management Studio에서 마법사가 SQL Server에 만든 새 대상 테이블을 볼 수 있습니다.

![SQL Server에 복사된 데이터](../../integration-services/import-export-data/media/data-copied-to-sql-server.jpg)

다시 SSMS에서 마법사가 SQL Server에 복사한 데이터를 볼 수 있습니다.

![SQL Server에 복사된 데이터 2](../../integration-services/import-export-data/media/data-copied-to-sql-server-2.jpg)

## <a name="learn-more"></a>자세히 알아보기  
마법사의 작동 방식에 대해 자세히 알아봅니다.
-   **마법사에 대해 자세히 알아보기.** 마법사에 대한 개요를 살펴보려면 [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조하세요.

-   **마법사의 단계에 대해 자세히 알아보기** - 마법사의 단계에 대한 정보를 찾으려면 [SQL Server 가져오기 및 내보내기 마법사의 단계](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)의 목록에서 원하는 페이지를 선택하세요. 또한 마법사의 각 페이지마다 별도의 설명서 페이지가 있습니다.

-   **데이터 원본 및 대상에 연결하는 방법에 대해 자세히 알아보기** - 데이터에 연결하는 방법에 대한 정보를 찾으려면 [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)의 목록에서 원하는 페이지를 선택하세요. 주로 사용되는 각 데이터 원본에 대한 개별 설명서 페이지도 있습니다.

-   **Excel에서 데이터를 로드하는 방법을 자세히 알아봅니다.** Excel 파일 연결 및 Excel 파일에서 데이터를 로드할 때 제한 사항 및 알려진 문제에 대해 알아보려면 [SSIS(SQL Server Integration Services)를 통해 Excel로 데이터 로드](../load-data-to-from-excel-with-ssis.md)를 참조하세요.
