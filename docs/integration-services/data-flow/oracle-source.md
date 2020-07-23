---
title: Oracle 원본
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6260504afcaabfefb6de7e6f262aa475479cf487
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913764"
---
# <a name="oracle-source"></a>Oracle 원본

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Oracle 원본은 다음 모드를 사용하여 Oracle Database에서 데이터를 추출합니다.

- 테이블 또는 뷰

- SQL 문의 결과

원본은 Oracle 연결 관리자를 사용하여 Oracle 원본에 연결합니다. 자세한 내용은 [Oracle 연결 관리자](oracle-connection-manager.md)를 참조하세요.

## <a name="error-output"></a>오류 출력.

오류 출력에는 다음과 같은 열이 포함되어 있습니다.  

- **오류 코드**: 현재 오류의 오류 유형을 나타내는 숫자입니다. 오류 코드는 다음에서 제공될 수 있습니다.
    - Oracle 서버. Oracle 데이터베이스 설명서의 자세한 오류 설명을 참조하세요.
    - SSIS 런타임. SSIS 오류 코드 목록은 SSIS 오류 코드 및 메시지 참조를 참조하십시오.
- **오류 열**: 변환 오류를 유발하는 원본 열 번호입니다.

- **오류 데이터 열**: 오류의 원인이 되는 데이터입니다.

Oracle 원본은 로드 및 추출 프로세스 동안 발생한 오류를 오류 출력에 반환합니다. 자세한 내용은 [Oracle 원본 편집기(오류 출력 페이지)](#oracle-source-editor-error-output-page)를 참조하세요.

## <a name="troubleshooting-the-oracle-source"></a>Oracle 원본 문제 해결

Oracle 원본이 Oracle 데이터 원본에 대해 수행하는 ODBC 호출을 기록하여 데이터 내보내기 문제를 해결할 수 있습니다. Oracle 원본이 Oracle 데이터 원본에 대해 수행하는 ODBC 호출을 기록하려면 ODBC 드라이버 관리자 추적을 사용하도록 설정합니다. 자세한 내용은 *ODBC 데이터 원본 관리자를 사용하여 ODBC 추적을 생성하는 방법*에 대한 Microsoft 설명서를 참조하십시오.

## <a name="oracle-source-custom-properties"></a>Oracle 원본 사용자 지정 속성

Oracle 원본의 사용자 지정 속성은 다음과 같습니다. 모든 속성은 읽기/쓰기가 가능합니다.

|속성 이름|데이터 형식|Description|
|:-|:-|:-|
|AccessMode|Integer(열거형)|데이터베이스에 액세스하는 데 사용되는 모드입니다. 가능한 값은 **테이블 이름** 및 **SQL 명령**입니다. 기본값은 **테이블 이름**입니다.|
|BatchSize|정수|대량 로드에 대한 일괄 처리 크기입니다. 배열로 추출되는 레코드의 수입니다. <br>이 속성은 **고급 편집기**에서만 설정됩니다.|
|DefaultCodePage|정수|데이터 원본에 코드 페이지 정보가 없을 때 사용할 코드 페이지입니다. <br>이 속성은 **고급 편집기**에서만 설정됩니다.|
|PreFetchCount|정수|미리 가져온 행의 수입니다. <br>이 속성은 **고급 편집기**에서만 설정됩니다.|
|SqlCommand|String|AccessMode가 SQL 명령으로 설정될 때 실행할 SQL 명령입니다.|
|TableName|String|AccessMode가 테이블 이름으로 설정될 때 사용되는 데이터가 포함된 테이블의 이름입니다.|

## <a name="configuring-the-oracle-source"></a>Oracle 원본 구성

SSIS 디자이너를 사용하거나 프로그래밍 방식으로 Oracle 원본을 구성할 수 있습니다.

Oracle 원본 편집기는 아래 그림에 나와 있습니다. 여기에는 연결 관리자 페이지, 열 페이지 및 오류 출력 페이지가 포함되어 있습니다.

자세한 내용은 다음 섹션 중 하나를 참조하세요.

- [Oracle 원본 편집기(연결 관리자 페이지)](#oracle-source-editor-connection-manager-page)
- [Oracle 원본 편집기(열 페이지)](#oracle-source-editor-columns-page)
- [Oracle 원본 편집기(오류 출력 페이지)](#oracle-source-editor-error-output-page)

![Oracle 원본](media/oracle-source.png)

**고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 포함됩니다.

**고급 편집기** 대화 상자를 열려면

- Integration Services 프로젝트의**데이터 흐름** 화면에서 Oracle 원본을 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시**를 선택합니다.

**고급 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [Oracle 원본 사용자 지정 속성](#oracle-source-custom-properties)을 참조하세요.

## <a name="oracle-source-editor-connection-manager-page"></a>Oracle 원본 편집기(연결 관리자 페이지)

**연결 관리자** 페이지의 **Oracle 원본 편집기** 대화 상자에서는 Oracle Database를 데이터베이스의 원본, 테이블 또는 뷰로 선택할 수 있습니다.

**Oracled 원본 편집기의 연결 관리자 페이지를 열려면**

- SQL Server Data Tools에서 Oracle 원본이 있는 SSIS(SQL Server Integration Services) 패키지를 엽니다.

- 데이터 흐름 탭에서 Oracle 원본을 두 번 클릭합니다.
### <a name="options"></a>옵션

**Connection manager**

목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 Oracle 연결 관리자를 만듭니다.

**새로 만들기**

**새로 만들기**를 클릭합니다. 새 연결 관리자를 만들 수 있는 **Oracle 연결 관리자 편집기** 대화 상자가 열립니다.

**데이터 액세스 모드**

원본에서 데이터를 선택하는 방법을 선택합니다. 옵션은 다음 표에 표시되어 있습니다.

|옵션|Description|
|:-|:-|
|테이블 또는 뷰|Oracle 데이터 원본에 있는 테이블이나 뷰에서 데이터를 검색합니다. 이 옵션을 선택한 경우 **테이블 또는 뷰 이름** 목록에서 사용 가능한 테이블 또는 뷰를 선택합니다.|
|SQL 명령|SQL 쿼리를 사용하여 Oracle 데이터 원본에서 데이터를 검색합니다. 이 옵션을 선택할 경우 다음 중 한 가지 방법으로 쿼리를 입력합니다. <br>**SQL 명령 텍스트** 필드에 SQL 쿼리 텍스트를 입력합니다. <br>**찾아보기** 를 클릭하여 텍스트 파일에서 SQL 쿼리를 로드합니다. <br>**쿼리 구문 분석** 을 클릭하여 쿼리 텍스트의 구문을 확인합니다.|

**미리 보기**

**미리 보기** 를 클릭하면 선택한 테이블 또는 뷰에서 추출된 최대 200개의 데이터 행을 볼 수 있습니다.

## <a name="oracle-source-editor-columns-page"></a>원시 파일 원본 편집기(열 페이지)

**Oracle 원본 편집기** 대화 상자의 **열** 페이지에서 출력 열을 각 외부(원본) 열에 매핑할 수 있습니다.

**Oracle 원본 편집기의 열 페이지를 열려면**

- SQL Server Data Tools에서 Oracle 원본이 있는 SSIS(SQL Server Integration Services) 패키지를 엽니다.

- 데이터 흐름 탭에서 Oracle 원본을 두 번 클릭합니다.

- Oracle 원본 편집기에서 열을 클릭합니다.

### <a name="options"></a>옵션

**사용 가능한 외부 열**

선택한 순서대로 **외부 열** 목록에 추가하기 위해 선택할 수 있는 사용 가능한 외부 열의 목록입니다. 이 테이블은 열을 추가하거나 삭제하는 데 사용할 수 없습니다.

모든 열을 선택하려면 **모두 선택** 확인란을 선택합니다.

**외부 열**

선택한 외부(원본) 열은 순서대로 나열됩니다.
순서를 변경하려면 먼저 **사용 가능한 외부 열"목록을 지운 다음, 다른 순서로 열을 선택합니다.

**출력 열**

선택된 외부(원본) 열의 이름이 기본 출력 이름입니다. 그렇지만 아무 고유 이름을 입력할 수 있습니다.
> [!NOTE]
>
>지원되지 않는 데이터 형식의 열이 있는 경우 데이터 형식이 지원되지 않는다는 경고가 표시되고 관련 열이 매핑 열에서 제거됩니다.

## <a name="oracle-source-editor-error-output-page"></a>Oracle 원본 편집기(오류 출력 페이지)

**Oracle 원본 편집기** 대화 상자의 **오류 출력** 페이지를 사용하여 오류 처리 옵션을 선택할 수 있습니다.

**Oracle 원본 편집기 오류 출력 페이지를 열려면**

- SQL Server Data Tools에서 Oracle 원본이 있는 SSIS(SQL Server Integration Services) 패키지를 엽니다.

- 데이터 흐름 탭에서 Oracle 원본을 두 번 클릭합니다.

- Oracle 원본 편집기에서 오류 출력을 클릭합니다.

### <a name="options"></a>옵션

**오류 동작**

Oracle 원본에서 흐름의 오류를 처리하는 방법을 선택합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.
**관련 섹션**: [데이터 오류 처리](https://docs.microsoft.com/sql/integration-services/data-flow/error-handling-in-data?view=sql-server-2017)

**잘림**

Oracle 원본에서 흐름의 잘림을 처리하는 방법을 선택합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [Oracle 대상](oracle-destination.md)을 구성합니다.
- 질문이 있는 경우 [TechCommunity](https://aka.ms/AA5u35j)을 방문하세요.
