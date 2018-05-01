---
title: SSIS를 통해 Excel에서 데이터 로드 | Microsoft Docs
ms.description: Describes how to import data from Excel or export data to Excel with SQL Server Integration Services (SSIS). Also describes prerequisites, known issues, and limitations.
ms.date: 04/10/2018
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: article
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8c31229aab550138805a912ffe40a33d08143205
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="load-data-from-or-to-excel-with-sql-server-integration-services-ssis"></a>SSIS(SQL Server Integration Services)를 통해 Excel에서 데이터 로드

이 문서에서는 SSIS(SQL Server Integration Services)를 통해 Excel에서 데이터 가져오거나 Excel로 데이터를 내보내는 방법을 설명합니다. 또한 필수 구성 요소, 제한 사항 및 알려진 문제를 설명합니다.

SSIS 패키지를 만들고 Excel 연결 관리자 및 Excel 원본 또는 Excel 대상을 사용하여 Excel에서 데이터를 가져오거나 Excel로 데이터를 내보낼 수 있습니다. 또한 SSIS를 기반으로 하는 SQL Server 가져오기 및 내보내기 마법사를 사용할 수 있습니다.

이 아티클에는 SSIS에서 Excel을 성공적으로 사용하거나 일반적인 문제를 이해하고 해결하는 데 필요한 세 가지 정보 집합이 포함되어 있습니다.
-   [필요한 파일](#files-you-need).
-   Excel에서 또는 Excel로 데이터를 로드할 때 제공해야 하는 정보입니다.
    -   데이터 원본으로 [Excel을 지정](#specify-excel)합니다.
    -   [Excel 파일 이름 및 경로](#excel-file)를 제공합니다.
    -   [Excel 버전](#excel-version)을 선택합니다.
    -   [첫 번째 행에 열 이름을 포함](#first-row)할지 여부를 지정합니다.
    -   [데이터를 포함하는 워크시트 또는 범위](#sheets-ranges)를 제공합니다.
-   알려진 문제 및 제한 사항입니다.
    -   [데이터 형식](#issues-types) 문제입니다.
    -   [가져오기](#issues-importing) 문제입니다.
    -   [내보내기](#issues-exporting) 문제입니다.

## <a name="files-you-need"> </a> Excel에 연결하는 데 필요한 파일 가져오기

Excel에서 데이터를 가져오거나 Excel로 데이터를 내보내려면 Excel용 연결 구성 요소가 설치되어 있지 않은 경우 먼저 다운로드해야 합니다. Excel용 연결 구성 요소는 기본적으로 설치되어 있지 않습니다.

[Microsoft Access 데이터베이스 엔진 2016 재배포 가능](https://www.microsoft.com/download/details.aspx?id=54920)에서 최신 버전의 Excel용 연결 구성 요소를 다운로드합니다.
  
최신 버전 구성 요소는 이전 버전의 Excel에서 만든 파일을 열 수 있습니다.

Microsoft Access 2016 *런타임*이 아닌 Access 데이터베이스 엔진 2016 *재배포 가능 패키지*를 다운로드해야 합니다.

컴퓨터에 32비트 버전의 Office가 이미 설치되어 있는 경우 32비트 버전의 구성 요소를 설치해야 합니다. 또한 32비트 모드에서 SSIS 패키지를 실행하거나 가져오기 및 내보내기 마법사의 32비트 버전을 실행하는지 확인해야 합니다.

Office 365 구독이 있는 경우 설치 관리자를 실행할 때 오류 메시지가 나타날 수 있습니다. 오류는 Office 간편 실행 구성 요소와 함께 다운로드를 설치할 수 없음을 나타냅니다. 이 오류 메시지를 무시하려면 명령 프롬프트 창을 열고 `/quiet` 스위치를 통해 다운로드한 .EXE 파일을 실행하여 자동 모드에서 설치를 실행합니다. 예를 들어 다음과 같이 사용할 수 있습니다.

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

2016 재배포 가능을 설치하는 데 문제가 있는 경우 [Microsoft Access 데이터베이스 엔진 2010 재배포 가능](https://www.microsoft.com/download/details.aspx?id=13255)에서 2010 재배포 가능 패키지를 대신 설치합니다. (Excel 2013용 재배포 가능 패키지는 없습니다.)

## <a name="specify-excel"> </a> 시작

첫 번째 단계는 Excel에 연결하려 함을 나타내는 것입니다.

### <a name="in-ssis"></a>SSIS에서
SSIS에서 Excel 연결 관리자를 만들어 Excel 원본 또는 대상 파일에 연결합니다. 다음과 같은 여러 가지 방법으로 연결 관리자를 만들 수 있습니다.

-   **연결 관리자** 영역에서 마우스 오른쪽 단추를 클릭하고 **새 연결**을 선택합니다. **SSIS 연결 관리자 추가** 대화 상자에서 **EXCEL**을 선택한 다음, **추가**를 선택합니다.
 
-   **SSIS** 메뉴에서 **새 연결**을 선택합니다. **SSIS 연결 관리자 추가** 대화 상자에서 **EXCEL**을 선택한 다음, **추가**를 선택합니다.

-   동시에 **Excel 원본 편집기** 또는 **Excel 대상 편집기**의 **연결 관리자** 페이지에서 **Excel 원본** 또는 **Excel 대상**을 구성하는 연결 관리자를 만듭니다.

### <a name="in-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사에서
가져오기 및 내보내기 마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 **데이터 원본** 목록의 **Microsoft Excel**을 선택합니다.

데이터 원본의 목록에서 Excel이 표시되지 않는 경우 32비트 마법사를 실행하고 있는지 확인합니다. Excel 연결 구성 요소는 일반적으로 32비트 파일이며 64비트 마법사에는 표시되지 않습니다.

## <a name="excel-file"> </a> Excel 파일 및 파일 경로

제공할 정보의 첫 번째 부분은 Excel 파일에 대한 경로 및 파일 이름입니다. 이 정보는 SSIS 패키지의 **Excel 연결 관리자 편집기**나 가져오기 및 내보내기 마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 입력합니다.

다음과 같은 형식의 경로 및 파일 이름을 입력합니다.

-   로컬 컴퓨터의 파일은 **C:\\TestData.xlsx**입니다.

-   네트워크 공유의 파일은 **\\\\Sales\\Data\\TestData.xlsx**입니다.

또는 **찾아보기**를 클릭하고 **열기** 대화 상자를 사용하여 스프레드시트를 찾습니다.  
  
> [!IMPORTANT]
> 암호로 보호된 Excel 파일에는 연결할 수 없습니다.

## <a name="excel-version"></a> Excel 버전

제공할 정보의 두 번째 부분은 Excel 파일의 버전입니다. 이 정보는 SSIS 패키지의 **Excel 연결 관리자 편집기**나 가져오기 및 내보내기 마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 입력합니다.

파일을 만드는 데 사용된 Microsoft Excel의 버전 또는 다른 호환 가능한 버전을 선택합니다. 예를 들어 2016 연결 구성 요소를 설치하는 데 문제가 있으면 2010 구성 요소를 설치하고 목록에서 **Microsoft Excel 2007-2010**을 선택할 수 있습니다.

이전 버전의 연결 구성 요소가 설치되어 있는 경우 목록에서 최신 버전의 Excel 버전을 선택하지 못할 수도 있습니다. **Excel 버전** 목록에는 SSIS가 지원하는 모든 버전의 Excel이 포함됩니다. 이 목록에 포함되었다고 해서 필요한 구성 요소가 설치되었다는 뜻은 아닙니다. 예를 들어 2016 연결 구성 요소를 설치하지 않은 경우에도 **Microsoft Excel 2016**이 목록에 표시됩니다.

## <a name="first-row"></a> 첫 번째 행에 열 이름 포함

Excel에서 데이터를 가져오는 경우 다음 단계는 데이터의 첫 번째 행에 열 이름을 포함할지 여부를 나타내는 것입니다. 이 정보는 SSIS 패키지의 **Excel 연결 관리자 편집기**나 가져오기 및 내보내기 마법사의 **데이터 원본 선택** 페이지에서 입력합니다.

-   원본 데이터에 열 이름이 포함되어 있지 않아 이 옵션이 비활성화되어 있는 경우 마법사는 F1, F2 등을 열 제목으로 사용합니다.
-   데이터에 열 이름이 포함되어 있지만 이 옵션을 비활성화한 경우 마법사는 열 이름을 데이터의 첫 번째 행으로 가져옵니다.
-   데이터에 열 이름이 포함되어 있지 않은데 이 옵션을 활성화한 경우 마법사는 원본 데이터의 첫 번째 행을 열 이름으로 사용합니다. 이 경우 원본 데이터의 첫 번째 행은 더 이상 데이터 자체에 포함되지 않습니다.

Excel에서 데이터를 내보내고 이 옵션을 활성화한 경우 내보내는 데이터의 첫 번째 행은 열 이름을 포함합니다.

## <a name="sheets-ranges"></a> 워크시트 및 범위

데이터에 대해 데이터 원본이나 대상으로 사용할 수 있는 Excel 개체의 유형에는 워크시트, 명명된 된 범위 또는 해당 주소로 지정한 셀의 명명되지 않은 영역, 이렇게 세 가지가 있습니다.

-   **워크시트.** 워크시트를 지정하려면 시트 이름 끝에 `$` 문자를 추가하고 문자열 주위에 구분 기호를 추가합니다(예: **[Sheet1$]**). 또는 기존 테이블 및 뷰 목록에서 `$` 문자로 끝나는 이름을 찾습니다.

-   **명명된 범위.** 명명된 범위를 지정하려면 범위 이름을 제공합니다(예: **MyDataRange**). 또는 기존 테이블 및 뷰 목록에서 `$` 문자로 끝나지 않는 이름을 찾습니다.
    
-   **명명되지 않은 범위.** 명명하지 않은 셀의 범위를 지정하려면 시트 이름 끝에 $ 문자를 추가하고 문자열 주위에 구분 기호를 추가합니다(예: **[Sheet1$A1:B4]**).

데이터에 대해 원본 또는 대상으로 사용하려는 Excel 개체의 유형을 선택하거나 지정하려면 다음 작업 중 하나를 수행합니다.

### <a name="in-ssis"></a>SSIS에서

SSIS에서 **Excel 원본 편집기** 또는 **Excel 대상 편집기**의 **연결 관리자** 페이지에서 다음 작업 중 하나를 수행합니다.

-   **워크시트** 또는 **명명된 범위**를 사용하려면 **테이블 또는 뷰**를 **데이터 액세스 모드**로 선택합니다. 그런 다음, **Excel 시트의 이름** 목록에서 워크시트 또는 명명된 범위를 선택합니다.

-   해당 주소를 사용하여 지정한 **명명되지 않은 범위**를 사용하려면 **SQL 명령**을 **데이터 액세스 모드**로 선택합니다. 그런 다음, **SQL 명령 텍스트** 필드에 다음 예제와 같은 쿼리를 입력합니다.

    ```sql
    SELECT * FROM [Sheet1$A1:B5]
    ```

### <a name="in-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사에서
가져오기 및 내보내기 마법사에서 다음 작업 중 하나를 수행합니다.

-   Excel에서 **가져올** 경우 다음 작업 중 하나를 수행합니다.

    -   **워크시트** 또는 **명명된 범위**를 사용하려면 **테이블 복사 또는 쿼리 지정** 페이지에서 **하나 이상의 테이블 또는 뷰에서 데이터 복사**를 선택합니다. 그런 다음, **원본 테이블 및 뷰 선택** 페이지에 있는 **원본** 열에서 원본 워크시트 및 명명된 범위를 선택합니다.

    -   해당 주소를 사용하여 지정한 **명명되지 않은 범위**를 사용하려면 **테이블 복사 또는 쿼리 지정** 페이지에서 **쿼리를 작성하여 전송할 데이터 지정**을 선택합니다. 그런 다음, **원본 쿼리 입력** 페이지에서 다음 예제와 비슷한 쿼리를 입력합니다.

        ```sql
        SELECT * FROM [Sheet1$A1:B5]
        ```

-   Excel로 **내보낼** 경우 다음 작업 중 하나를 수행합니다.

    -   **워크시트** 또는 **명명된 범위**를 사용하려면 **원본 테이블 및 뷰 선택** 페이지에 있는 **대상** 열에서 대상 워크시트 및 명명된 범위를 선택합니다.

    -   해당 주소를 사용하여 지정한 **명명되지 않은 범위**를 사용하려면 **원본 테이블 및 뷰 선택** 페이지에 있는 **대상** 열에서 구분 기호 없이 다음 형식으로 범위를 입력합니다. `Sheet1$A1:B5` 마법사에서 구분 기호를 추가합니다.

가져오거나 내보낼 Excel 개체를 선택하거나 입력한 후에, 마법사의 **원본 테이블 및 뷰 선택** 페이지에서 다음과 같은 작업을 수행할 수 있습니다.

-   **매핑 편집**을 선택하여 원본과 대상 간에 열 매핑을 검토합니다.

-   **미리 보기**를 선택하여 예상 대로 표시되는지 샘플 데이터를 미리 봅니다.

## <a name="issues-types"></a> 데이터 형식 문제

### <a name="data-types"></a>데이터 형식

Excel 드라이버는 제한된 데이터 형식 집합만 인식합니다. 예를 들어 모든 숫자 열은 double(DT_R8)로 해석되고 모든 문자열 열(메모 열 제외)은 255자 유니코드 문자열(DT_WSTR)로 해석됩니다. SSIS에서는 Excel 데이터 형식을 다음과 같이 매핑합니다.

-   숫자 - 배정밀도 부동 소수점 수(DT_R8)

-   통화 - currency(DT_CY)

-   부울 - Boolean(DT_BOOL)

-   날짜/시간 - datetime(DT_DATE)

-   문자열 - 길이가 255인 유니코드 문자열(DT_WSTR)

-   메모 - 유니코드 텍스트 스트림(DT_NTEXT)

### <a name="data-type-and-length-conversions"></a>데이터 형식 및 길이 변환

SSIS에서는 데이터 형식을 암시적으로 변환하지 않습니다. 따라서 파생 열 전환이나 데이터 변환을 사용하여 Excel 데이터를 비 Excel 대상으로 로드하기 전에 명시적으로 변환하거나 비 Excel 데이터를 Excel 대상으로 로드하기 전에 변환해야 할 수 있습니다.

필요할 수 있는 일부 변환 예는 다음과 같습니다.  
  
-   유니코드 Excel 문자열 열과 특정 코드 페이지가 있는 비유니코드 문자열 열 간 변환
  
-   255자 Excel 문자열 열과 길이가 다른 문자열 열 간 변환
  
-   배정밀도 Excel 숫자 열과 다른 유형의 숫자 열 간 변환

> [!TIP]
> 가져오기 및 내보내기 마법사를 사용하고 이러한 변환의 일부가 필요한 데이터의 경우 마법사에서 필요한 변환을 구성합니다. 결과적으로, SSIS 패키지를 사용하려는 경우에도 가져오기 및 내보내기 마법사를 사용하여 초기 패키지를 만드는 데 유용할 수 있습니다. 마법사에서 사용자를 위해 연결 관리자, 원본, 변환 및 대상을 만들고 구성합니다.

## <a name="issues-importing"></a> 가져오기 문제

### <a name="empty-rows"></a>빈 행

워크시트 또는 명명된 범위를 원본으로 지정하면 드라이버는 워크시트 또는 범위의 가장 왼쪽에서 비어 있지 않은 첫 번째 셀부터 *인접한* 블록의 셀을 읽습니다. 결과적으로, 데이터가 행 1에서 시작하지 않아도 되지만 원본 데이터에 빈 행을 둘 수 없습니다. 예를 들어 열 제목과 데이터 행 사이에 빈 행을 두거나 워크시트의 맨 위에서 제목 뒤에 빈 행을 둘 수 없습니다.

데이터 위에 행이 빈 경우 워크시트로 데이터를 쿼리할 수 없습니다. Excel에서 데이터의 범위를 선택하고 범위에 이름을 할당한 다음, 워크시트 대신 명명된 범위를 쿼리해야 합니다.

### <a name="missing-values"></a>누락된 값

Excel 드라이버는 지정한 원본에서 특정 개수의 행(기본값: 8행)을 읽어 각 열의 데이터 형식을 추측합니다. 열에 혼합된 데이터 형식, 특히 숫자 데이터와 텍스트 데이터가 혼합되어 있으면 드라이버는 주로 사용된 데이터 형식을 지정하고 다른 형식의 데이터가 포함된 셀에 Null 값을 반환합니다. 사용된 횟수가 같은 경우에는 숫자 유형이 적용됩니다. Excel 워크시트에서 대부분의 셀 서식 옵션은 이러한 데이터 형식 결정에 영향을 주지 않습니다.

모든 값을 텍스트로 가져오도록 가져오기 모드를 지정하여 Excel 드라이버의 이러한 동작을 수정할 수 있습니다. 가져오기 모드를 지정하려면 속성 창에서 Excel 연결 관리자의 연결 문자열에 있는 **확장 속성** 값에 `IMEX=1`을 추가합니다. 

### <a name="truncated-text"></a>잘린 텍스트

Excel 열에 텍스트 데이터가 포함되어 있음이 확인되면 드라이버는 샘플링하는 값 중 가장 긴 값을 기준으로 데이터 형식(문자열 또는 메모)을 선택합니다. 샘플링하는 행에서 255자보다 긴 값이 검색되지 않으면 이 드라이버는 해당 열을 메모 열이 아닌 255자 문자열 열로 처리합니다. 따라서 255자보다 긴 값은 잘릴 수 있습니다.

잘림 없이 메모 열에서 데이터를 가져오려면 두 가지 옵션이 있습니다.

-   샘플링된 행 중 하나 이상의 메모 열에 255자보다 긴 값이 포함되어 있는지 확인합니다.

-   이러한 행을 포함하도록 드라이버에서 샘플링된 행 수를 늘립니다. 다음과 같은 레지스트리 키에서 **TypeGuessRows** 값을 늘려 샘플링할 행 수를 늘릴 수 있습니다.

| 재배포 가능 구성 요소 버전 | 레지스트리 키 |
|---|---|
| Excel 2016 | HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\16.0\Access Connectivity Engine\Engines\Excel |
| Excel 2010 | HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\14.0\Access Connectivity Engine\Engines\Excel |
| | |

## <a name="issues-exporting"></a> 내보내기 문제

### <a name="create-a-new-destination-file"></a>새 대상 파일 만들기

#### <a name="in-ssis"></a>SSIS에서

만들려는 새 Excel 파일의 경로 및 파일 이름으로 Excel 연결 관리자를 만듭니다. 그런 다음, **Excel 대상 편집기**에서 **Excel 시트의 이름**에 대해 **새로 만들기**를 선택하여 대상 워크시트를 만듭니다. 이 시점에서 SSIS는 지정된 워크시트를 사용하여 새 Excel 파일을 만듭니다.

#### <a name="in-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사에서

**대상 선택** 페이지에서 **찾아보기**를 선택합니다. **열기** 대화 상자에서 새 Excel 파일을 만들 폴더로 이동하고, 새 파일에 사용할 이름을 입력한 다음, **열기**를 선택합니다.

### <a name="export-to-a-large-enough-range"></a>충분히 큰 범위로 내보내기

대상으로 범위를 지정하는 경우 범위가 원본 데이터의 *열 수*보다 적으면 오류가 발생합니다. 단, 지정하는 범위가 원본 데이터의 *행 수*보다 적은 경우에는 마법사에서 오류 없이 행 쓰기를 계속하고 범위 정의를 새 행 수와 일치하도록 확장합니다.

### <a name="export-long-text-values"></a>긴 텍스트 값 내보내기

255자보다 긴 문자열을 Excel 열에 저장하려면 드라이버에서 대상 열의 데이터 형식을 **string** 이 아닌 **memo**로 인식해야 합니다.

-   기존 대상 테이블에 이미 데이터 행이 포함된 경우 드라이버에서 샘플링하는 처음 몇 개 행의 메모 열에 255자보다 긴 값의 인스턴스가 하나 이상 포함되어야 합니다.

-   패키지를 디자인하는 동안, 런타임 시 또는 가져오기 및 내보내기 마법사에 의해 새 대상 테이블을 만드는 경우 `CREATE TABLE` 문은 대상 메모 열의 데이터 형식으로 LONGTEXT(또는 해당 동의어 중 하나)를 사용해야 합니다. 마법사에서 필요한 경우 **열 매핑** 페이지의 **대상 테이블 만들기** 옵션 옆에 있는 **SQL 편집**을 클릭하여 `CREATE TABLE` 문을 확인하고 수정합니다.

## <a name="related-content"></a>관련 내용

이 문서에 설명된 구성 요소와 절차에 대한 자세한 내용은 다음 문서를 참조하세요.

### <a name="about-ssis"></a>SSIS 정보
[Excel 연결 관리자](connection-manager/excel-connection-manager.md)  
[Excel 원본](data-flow/excel-source.md)  
[Excel 대상](data-flow/excel-destination.md)  
[Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
[스크립트 태스크를 사용한 Excel 파일 작업](extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)

### <a name="about-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사 정보
[Excel 데이터 원본에 연결](import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)  
[가져오기 및 내보내기 마법사의 이 간단한 예제로 시작](import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

### <a name="other-articles"></a>기타 문서
[Excel에서 SQL Server 또는 Azure SQL Database로 데이터 가져오기](../relational-databases/import-export/import-data-from-excel-to-sql.md)  
