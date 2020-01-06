---
title: 플랫 파일을 SQL로 가져오기 | Microsoft Docs
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 792cb1bcef1097c3eddaa325519b43a229bcccb4
ms.sourcegitcommit: ba44730f5cc33295ae2ed1f281186dd266bad4ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/19/2019
ms.locfileid: "74190797"
---
# <a name="import-flat-file-to-sql-wizard"></a>SQL 마법사로 플랫 파일 가져오기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
> 가져오기 및 내보내기 마법사와 관련된 콘텐츠는 [SQL Server 가져오기 및 내보내기 마법사](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard)를 참조하세요.

플랫 파일 가져오기 마법사는 플랫 파일(.csv, .txt)에서 데이터베이스의 새 테이블로 데이터를 복사하는 간단한 방법입니다. 이 개요에는 이 마법사를 사용하는 이유, 이 마법사를 찾는 방법 및 수행할 간단한 예제가 나와 있습니다.

## <a name="why-would-i-use-this-wizard"></a>이 마법사를 왜 사용해야 합니까?
이 마법사는 [PROSE](https://microsoft.github.io/prose/)(Program Synthesis using Examples)라고 하는 지능형 프레임워크를 활용하여 현재 가져오기 환경을 개선하기 위해 만들어졌습니다. 데이터 가져오기는 특별한 도메인 지식이 없는 사용자에게 복잡하고, 오류가 발생하기 쉬우며 번거로운 작업일 수 있습니다. 이 마법사는 가져오기 프로세스를 간소화하여 입력된 파일 및 고유한 테이블 이름을 선택하기만 하면 됩니다. 나머지는 PROSE 프레임워크가 처리합니다.

PROSE는 입력 파일의 데이터 패턴을 분석하여 열 이름, 형식, 구분 기호 등을 유추합니다. 이 프레임워크는 파일의 구조를 학습하고 복잡한 모든 작업을 사용자 대신 처리합니다.

플랫 파일 가져오기 마법사의 개선된 사용자 환경에 대해 자세히 알아보려면 다음 동영상을 확인하세요.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173/player?WT.mc_id=dataexposed-c9-niner]

## <a name="prerequisites"></a>사전 요구 사항
이 기능은 SSMS(SQL Server Management Studio) v17.3 이상에서만 사용할 수 있습니다. 최신 버전을 사용하고 있는지 확인하세요. 최신 버전은 [여기](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)에서 찾을 수 있습니다.
 
## <a id="started"></a>시작
플랫 파일 가져오기 마법사에 액세스하려면 다음 단계를 수행합니다.

1. **SQL Server Management Studio**를 엽니다.
2. SQL Server 데이터베이스 엔진의 인스턴스 또는 localhost에 연결합니다.
3. **데이터베이스**를 확장하고, 데이터베이스(아래 예제에서는 테스트)를 마우스 오른쪽 단추로 클릭하고, **작업**을 가리킨 다음, 데이터 가져오기 위에 있는 **플랫 파일 가져오기**를 클릭합니다.

![마법사 메뉴](media/import-flat-file-wizard/importffmenu.png)

마법사의 다른 기능에 대해 자세히 알아보려면 다음 자습서를 참조하세요.

## <a name="tutorial"></a>자습서
이 자습서의 목적을 위해 사용자 고유의 플랫 파일을 자유롭게 사용할 수 있어야 합니다. 그렇지 않으면 이 자습서는 사용자가 복사할 수 있는 Excel에서 다음 CSV를 사용합니다. 이 CSV를 사용하는 경우 제목을 **example.csv**로 지정하고 바탕 화면처럼 쉬운 위치에 csv로 저장해야 합니다.

![마법사 Excel](media/import-flat-file-wizard/importffexample.png)

### <a name="step-1-access-wizard-and-intro-page"></a>1단계: 마법사 액세스 및 소개 페이지
[여기](#started) 설명된 대로 마법사에 액세스합니다.

마법사의 첫 페이지는 시작 페이지입니다. 이 페이지를 다시 표시하지 않으려면 **이 시작 페이지를 다시 표시 안 함**을 클릭하면 됩니다.

![마법사 소개](media/import-flat-file-wizard/importffintro.png)

### <a name="step-2-specify-input-file"></a>2단계: 입력 파일 지정
찾아보기를 클릭하여 입력 파일을 선택합니다. 기본적으로 마법사는 .csv 및 .txt 파일을 검색합니다. 

새 테이블 이름은 고유해야 하며, 그렇지 않은 경우 더 이상 마법사에서 이동할 수 없습니다.

![마법사 지정](media/import-flat-file-wizard/importffspecify.png)

### <a name="step-3-preview-data"></a>3단계: 데이터 미리 보기
마법사에서는 첫 50개 행을 볼 수 있는 미리 보기가 생성됩니다. 문제가 있는 경우 취소를 클릭하고, 그렇지 않으면 다음 페이지로 진행합니다.

![마법사 미리 보기](media/import-flat-file-wizard/importffpreview.png)

### <a name="step-4-modify-columns"></a>4단계: 열 수정
마법사에서는 올바른 열 이름, 데이터 형식 등을 식별합니다. 올바르지 않은 경우(예를 들어 데이터 형식이 int가 아닌 float이여야 함) 다음에서 필드를 편집할 수 있습니다.

준비가 되면 계속 진행합니다.

![마법사 수정](media/import-flat-file-wizard/importffmodify.png)

### <a name="step-5-summary"></a>5단계: 요약
다음은 현재 구성을 표시하는 간단한 요약 페이지입니다. 문제가 있는 경우 이전 섹션으로 다시 이동할 수 있습니다. 그렇지 않으면 마침을 클릭하여 가져오기 프로세스를 시도합니다.

![마법사 요약](media/import-flat-file-wizard/importffsummary.png)

### <a name="step-6-results"></a>6단계: 결과
이 페이지는 가져오기 작업의 성공 여부를 나타냅니다. 녹색 확인 표시가 나타나는 경우 성공, 그렇지 않으면 모든 오류에 대해 구성 또는 입력 파일을 검토해야 할 수 있습니다.

![마법사 결과](media/import-flat-file-wizard/importffresults.png)

## <a name="learn-more"></a>자세한 정보

마법사에 대해 자세히 알아봅니다.
 
- **다른 원본 가져오기에 대해 자세히 알아봅니다.** 플랫 파일 이외의 항목을 가져오려는 경우 [SQL Server 가져오기 및 내보내기 마법사](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard)를 참조하세요.
- **플랫 파일 원본에 연결하기에 대해 자세히 알아봅니다.** 플랫 파일 원본에 연결하기에 대한 자세한 내용을 찾는 경우 [플랫 파일 데이터 원본에 연결](https://docs.microsoft.com/sql/integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard)을 참조하세요.
- **PROSE에 대해 자세히 알아봅니다.** 이 마법사에서 사용하는 지능형 프레임워크에 대한 개요를 찾는 경우 [PROSE SDK](https://microsoft.github.io/prose/)를 참조하세요.

