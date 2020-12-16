---
title: 플랫 파일을 SQL로 가져오기 | Microsoft Docs
description: 플랫 파일 가져오기 마법사는 .csv 또는 .txt 파일의 데이터를 새 데이터베이스 테이블에 복사하는 간단한 방법입니다. 이 문서에서는 마법사를 사용해야 하는 경우와 방법을 보여 줍니다.
ms.custom: ''
ms.date: 09/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: data-movement
ms.topic: conceptual
f1_keywords:
- sql13.swb.importflatfile.f1
author: yualan
ms.author: alayu
ms.reviewer: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 74c52322158826787cbb467b70a5c48dd8c845f0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473934"
---
# <a name="import-flat-file-to-sql-wizard"></a>SQL 마법사로 플랫 파일 가져오기
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
> 가져오기 및 내보내기 마법사와 관련된 콘텐츠는 [SQL Server 가져오기 및 내보내기 마법사](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조하세요.

플랫 파일 가져오기 마법사는 플랫 파일(.csv, .txt)에서 데이터베이스의 새 테이블로 데이터를 복사하는 간단한 방법입니다.  플랫 파일 가져오기 마법사는 쉼표로 구분된 서식 파일과 고정 너비 서식 파일을 모두 지원합니다. 이 개요에는 이 마법사를 사용하는 이유, 이 마법사를 찾는 방법 및 수행할 간단한 예제가 나와 있습니다.

## <a name="why-would-i-use-this-wizard"></a>이 마법사를 왜 사용해야 합니까?
이 마법사는 [PROSE](https://microsoft.github.io/prose/)(Program Synthesis using Examples)라고 하는 지능형 프레임워크를 활용하여 현재 가져오기 환경을 개선하기 위해 만들어졌습니다. 데이터 가져오기는 특별한 도메인 지식이 없는 사용자에게 복잡하고, 오류가 발생하기 쉬우며 번거로운 작업일 수 있습니다. 이 마법사는 가져오기 프로세스를 간소화하여 입력된 파일 및 고유한 테이블 이름을 선택하기만 하면 됩니다. 나머지는 PROSE 프레임워크가 처리합니다.

PROSE는 입력 파일의 데이터 패턴을 분석하여 열 이름, 형식, 구분 기호 등을 유추합니다. 이 프레임워크는 파일의 구조를 학습하고 복잡한 모든 작업을 사용자 대신 처리합니다.

플랫 파일 가져오기 마법사의 개선된 사용자 환경에 대해 자세히 알아보려면 다음 동영상을 확인하세요.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173/player?WT.mc_id=dataexposed-c9-niner]

## <a name="prerequisites"></a>사전 요구 사항
이 기능은 SSMS(SQL Server Management Studio) v17.3 이상에서 사용할 수 있습니다. 최신 버전을 사용하고 있는지 확인하세요. 최신 버전은 [여기](../../ssms/download-sql-server-management-studio-ssms.md)에서 찾을 수 있습니다.
 
## <a name="getting-started"></a><a id="started"></a>시작
플랫 파일 가져오기 마법사에 액세스하려면 다음 단계를 수행합니다.

1. **SQL Server Management Studio** 를 엽니다.
2. SQL Server 데이터베이스 엔진의 인스턴스 또는 localhost에 연결합니다.
3. **데이터베이스** 를 확장하고, 데이터베이스(아래 예제에서는 테스트)를 마우스 오른쪽 단추로 클릭하고, **작업** 을 가리킨 다음, 데이터 가져오기 위에 있는 **플랫 파일 가져오기** 를 클릭합니다.

![마법사 메뉴](media/import-flat-file-wizard/import-flat-file-menu.png)

마법사의 다른 기능에 대해 자세히 알아보려면 다음 자습서를 참조하세요.

## <a name="tutorial"></a>자습서
이 자습서의 목적을 위해 사용자 고유의 플랫 파일을 자유롭게 사용할 수 있어야 합니다. 그렇지 않으면 이 자습서는 사용자가 복사할 수 있는 Excel에서 다음 CSV를 사용합니다. 이 CSV를 사용하는 경우 제목을 **example.csv** 로 지정하고 바탕 화면처럼 쉬운 위치에 csv로 저장해야 합니다.

![마법사 Excel](media/import-flat-file-wizard/import-flat-file-example.png)

개요:
1. [액세스 마법사](#step-1-access-wizard-and-intro-page)
2. [입력 파일 지정](#step-2-specify-input-file)
3. [데이터 미리 보기](#step-3-preview-data)
4. [열 수정](#step-4-modify-columns)
5. [요약](#step-5-summary)
6. [결과](#step-6-results)

### <a name="step-1-access-wizard-and-intro-page"></a>1단계: 마법사 액세스 및 소개 페이지
[여기](#started) 설명된 대로 마법사에 액세스합니다.

마법사의 첫 페이지는 시작 페이지입니다. 이 페이지를 다시 표시하지 않으려면 **이 시작 페이지를 다시 표시 안 함** 을 클릭하면 됩니다.

![마법사 소개](media/import-flat-file-wizard/import-flat-file-intro.png)

### <a name="step-2-specify-input-file"></a>2단계: 입력 파일 지정
찾아보기를 클릭하여 입력 파일을 선택합니다. 기본적으로 마법사는 .csv 및 .txt 파일을 검색합니다. PROSE는 파일 확장명과 무관하게 파일이 쉼표로 구분된 서식과 고정 너비 서식 중 어떤 서식인지 감지합니다.

새 테이블 이름은 고유해야 하며, 그렇지 않은 경우 더 이상 마법사에서 이동할 수 없습니다.

![마법사 지정](media/import-flat-file-wizard/import-flat-file-specify.png)

### <a name="step-3-preview-data"></a>3단계: 데이터 미리 보기
마법사에서는 첫 50개 행을 볼 수 있는 미리 보기가 생성됩니다. 문제가 있는 경우 취소를 클릭하고, 그렇지 않으면 다음 페이지로 진행합니다.

![마법사 미리 보기](media/import-flat-file-wizard/import-flat-file-preview.png)

### <a name="step-4-modify-columns"></a>4단계: 열 수정
마법사에서는 올바른 열 이름, 데이터 형식 등을 식별합니다. 올바르지 않은 경우(예를 들어 데이터 형식이 int가 아닌 float이여야 함) 다음에서 필드를 편집할 수 있습니다.

빈 값이 검색되는 열에는 “Null 허용”이 선택되어 있습니다. 그러나 열에 null을 허용해야 하는데 “Null 허용”이 선택되지 않은 경우에는 하나 또는 모든 열에 null을 허용하도록 테이블 정의를 업데이트할 수 있습니다.

준비가 되면 계속 진행합니다.

![마법사 수정](media/import-flat-file-wizard/import-flat-file-modify.png)

### <a name="step-5-summary"></a>5단계: 요약
다음은 현재 구성을 표시하는 간단한 요약 페이지입니다. 문제가 있는 경우 이전 섹션으로 다시 이동할 수 있습니다. 그렇지 않으면 마침을 클릭하여 가져오기 프로세스를 시도합니다.

![마법사 요약](media/import-flat-file-wizard/import-flat-file-summary.png)

### <a name="step-6-results"></a>6단계: 결과
이 페이지는 가져오기 작업의 성공 여부를 나타냅니다. 녹색 확인 표시가 나타나는 경우 성공, 그렇지 않으면 모든 오류에 대해 구성 또는 입력 파일을 검토해야 할 수 있습니다.

![마법사 결과](media/import-flat-file-wizard/import-flat-file-results.png)

## <a name="troubleshooting"></a>문제 해결
플랫 파일 가져오기 마법사는 처음 200개의 행을 기반으로 데이터 형식을 검색합니다.  플랫 파일의 데이터가 자동으로 검색된 데이터 형식에 더 이상 맞지 않는 시나리오에서는 가져오는 중에 오류가 발생합니다. 오류 메시지는 다음과 유사합니다.
```
Error inserting data into table. (Microsoft.SqlServer.Prose.Import)
The given value of type String from the data source cannot be converted to type nvarchar of the specified target column. (System.Data)
String or binary data would be truncated. (System.Data)
```
이러한 오류를 완화하기 위한 전술은 다음과 같습니다.
- [열 수정 단계](#step-4-modify-columns)에서 nvarchar 열의 길이와 같은 데이터 형식 크기를 확장하여 플랫 파일의 나머지 부분에 있는 데이터의 변형을 보정할 수 있습니다.
- [열 수정 단계](#step-4-modify-columns)에서 특히 더 작은 수로 오류 보고를 사용하도록 설정하면 선택한 데이터 형식에 맞지 않는 데이터가 포함된 플랫 파일의 행이 표시됩니다. 예를 들어 두 번째 행에서 오류가 발생하는 플랫 파일의 경우 범위가 1인 오류 보고가 있는 가져오기를 실행하면 특정 오류 메시지를 제공합니다.  해당 위치에서 직접 파일을 검사하면 식별된 행의 데이터를 기반으로 데이터 형식에 대한 더 많은 대상 변경 내용이 제공될 수 있습니다.

![오류 보고 결과](media/import-flat-file-wizard/import-flat-file-error.png)

```
Error inserting data into table occured while inserting rows 1 - 2. (Microsoft.SqlServer.Prose.Import)
The given value of type String from the data source cannot be converted to type float of the specified target column. (System.Data)
Failed to convert parameter value from a String to a Double. (System.Data)
```


## <a name="learn-more"></a>자세한 정보

마법사에 대해 자세히 알아봅니다.
 
- **다른 원본 가져오기에 대해 자세히 알아봅니다.** 플랫 파일 이외의 항목을 가져오려는 경우 [SQL Server 가져오기 및 내보내기 마법사](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조하세요.
- **플랫 파일 원본에 연결하기에 대해 자세히 알아봅니다.** 플랫 파일 원본에 연결하기에 대한 자세한 내용을 찾는 경우 [플랫 파일 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)을 참조하세요.
- **PROSE에 대해 자세히 알아봅니다.** 이 마법사에서 사용하는 지능형 프레임워크에 대한 개요를 찾는 경우 [PROSE SDK](https://microsoft.github.io/prose/)를 참조하세요.