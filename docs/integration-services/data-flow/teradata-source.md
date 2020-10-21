---
description: Teradata 원본에 연결
title: Teradata 원본에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5b4e64c2d7ada0db923f1aa623576e7b2994d8e6
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194705"
---
# <a name="connect-to-the-teradata-source"></a>Teradata 원본에 연결

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Teradata 원본은 다음을 사용하여 Teradata 데이터베이스에서 데이터를 추출합니다.
- 테이블 또는 뷰
- SQL 문의 결과

이 원본은 Teradata 연결 관리자를 사용하여 Teradata 원본에 연결합니다. 자세한 내용은 [Teradata 연결 관리자 사용](teradata-connection-manager.md)을 참조하세요.

## <a name="troubleshoot-the-teradata-source"></a>Teradata 원본 문제 해결

Teradata 원본이 TPT(Teradata Parallel Transporter) API에 대해 수행하는 호출을 기록할 수 있습니다. 이렇게 하려면 패키지 로깅을 사용하도록 설정하고 패키지 수준에서 **진단** 이벤트를 선택합니다.

ODBC(Open Database Connectivity) 드라이버 관리자 추적을 사용하도록 설정하여 Teradada 원본이 Teradata ODBC 드라이버에 대해 수행하는 ODBC 호출을 기록할 수 있습니다. 자세한 내용은 [ODBC 데이터 원본 관리자를 사용하여 ODBC 추적을 생성하는 방법](../../odbc/admin/setting-tracing-options.md)을 참조하세요.

## <a name="parallelism"></a>병렬 처리

Teradata 원본은 병렬 처리를 지원합니다. 여기서 내보내기 작업은 동일한 테이블이나 다른 테이블에 동시에 액세스할 수 있습니다. `MaxLoadTasks`라는 데이터베이스 변수는 동시에 실행할 수 있는 내보내기 작업 수의 제한을 설정합니다. `MaxLoadTasks` 변수를 사용하여 이 최대 수를 정의할 수 있습니다.

## <a name="teradata-source-custom-properties"></a>Teradata 원본 사용자 지정 속성

Teradata 원본의 사용자 지정 속성은 다음 표에 나열되어 있습니다. 모든 속성은 읽기/쓰기가 가능합니다.

|속성 이름|데이터 형식|Description|
|:-|:-|:-|
|AccessMode|Integer(열거형)|데이터베이스에 액세스하는 데 사용되는 모드입니다. 가능한 값은 *테이블 이름* 및 *SQL 명령*입니다. 기본값은 *테이블 이름*입니다.|
|BlockSize|정수|클라이언트에 데이터를 반환할 때 사용되는 블록 크기(바이트)입니다. 기본값은 1048576(1MB)입니다. 최소값은 256바이트입니다. 최대값은 16775168바이트입니다.<br> 이 속성은 **고급 편집기** 창에 있습니다.|
|BufferMaxSize|정수|GetBuffer 함수에서 반환하는 데이터 버퍼의 총 최대 크기입니다. 이 크기는 행 헤더, 실제 데이터 행, 버퍼 트레일러를 포함하여 적어도 하나 이상의 데이터 행을 저장할 수 있을 만큼 커야 합니다. 데이터 버퍼의 기본 총 최대 크기는 16775552바이트입니다. <br>자세한 내용은 [GetBuffer를 사용하여 Teradata 데이터베이스에서 데이터 내보내기](https://docs.teradata.com/reader/TvVKKmxaBAoyETJZD8zz_g/oaxiwNJmnCa6UctY4k498w)를 참조하세요.|
|BufferMode|부울|기본값은 *True*입니다. PutBuffer 기능이 사용되는 경우 값이 *True*여야 합니다. 이 속성은 **고급 편집기** 창에 있습니다.|
|DataEncryption|부울|기본값은 *False*입니다. 값이 *True*일 경우 전체 보안 암호화가 사용됩니다.|
|DefaultCodePage|정수|데이터 원본에 코드 페이지 정보가 없을 때 사용할 코드 페이지입니다. 이 속성은 **고급 편집기** 창에 있습니다.|
|DetailedTracingLevel|Integer(열거형)|고급 추적에 대해 다음 옵션 중 하나를 선택합니다. <br> *Off*: 고급 로깅을 사용하지 않습니다. <br> *일반*: 드라이버별 작업 일반 추적이 기록됩니다. <br> *CLI*: CLIv2 관련 작업 추적이 기록됩니다. <br> *Notify 메서드*: Notify 기능 관련 작업 추적이 기록됩니다. <br> *공용 라이브러리*: opcommon 라이브러리 작업 추적이 기록됩니다. <br> *모두*: 위의 모든 작업 추적이 기록됩니다. <br> 고급 추적 로그 파일은 `DetailedTracingFile` 속성에서 정의됩니다. <br> 옵션이 *Off*가 아닐 경우 `DetailedTracingFile` 속성을 설정해야 합니다. 이 속성은 **고급 편집기** 창에 있습니다.|
|DetailedTracingFile|String|*DetailedTracingLevel*이 *Off*가 아닐 경우 자동으로 생성되는 로그 파일의 경로입니다. 이 속성은 **고급 편집기** 창에 있습니다.|
|DiscardLargeRow|부울|기본값은 *False*입니다. 값이 *True*일 경우 큰 행(64KB 초과)을 삭제합니다.|
|ExtendedStringColumnsAllocation|부울|값이 *True*일 경우 *최대 전송 문자 할당 인수*가 사용됩니다. <br> Teradata 데이터베이스 `Export Width Table ID` 속성이 *최대 기본값*으로 설정된 경우 이 값을 *True*로 설정해야 합니다. <br> 기본값은 *False*입니다.|
|JobMaxRowSize|정수|최대 행 크기가 지원될 수 있습니다. `DiscardLargeRow` 값이 *True*일 경우 이 값이 필요합니다.<br>유효한 값은 <br>*64*(기본값): 2바이트 행 길이가 지원될 수 있습니다. <br>*1024*: 4바이트 행 길이가 지원될 수 있습니다.|
|MaxSessions|정수|로그인된 최대 세션 수입니다. 이 값은 1보다 커야 합니다. 기본값은 사용 가능한 각 AMP(액세스 모듈 프로세서)마다 1개 세션입니다.|
|MinSessions|정수|로그인된 최소 세션 수입니다. 이 값은 1보다 커야 합니다. 기본값은 사용 가능한 각 AMP마다 1개 세션입니다.|
|QueryBandSessInfo|Varchar|연결 문자열 형식의 사용자 정의 세션 기반 쿼리 밴드 식입니다. 차지백 모니터링 및 거버넌스에 이 속성을 사용합니다. 이 속성은 **고급 편집기** 창에 있습니다.|
|SpoolMode|Varchar|유효한 값은 다음과 같습니다. <br>*Spool*: 기본값 *Spool*을 사용합니다. <br> *NoSpool*: *Spool*을 사용하지 않습니다. 이 값은 DBS(데이터베이스 서버)가 *NoSpool*을 지원하는 경우에만 유효합니다. <br>  *NoSpoolOnly*: 어떤 경우에도 *Spool*을 사용하지 않습니다. DBS가 *NoSpool*을 지원하지 않는 경우 오류가 발생하여 작업이 종료됩니다.|
|SqlCommand|String|`AccessMode`가 *SQL 명령*으로 설정될 때 실행할 SQL 명령입니다.|
|TableName|String|`AccessMode`가 *테이블 이름*으로 설정될 때 사용할 데이터가 포함된 테이블의 이름입니다.|
|TenacityHours|정수|최대 수의 로드/내보내기 작업이 이미 실행 중인 경우 TPT 드라이버가 로그인을 시도하는 시간(시)입니다. 기본값은 *4시간*입니다. 이 속성은 **고급 편집기** 창에 있습니다.|
|TenacitySleep|정수|제한에 도달했을 때 로그인을 시도하기 전에 TPT 드라이버가 일시 중지되는 시간(분)입니다. 이 제한은 `MaxSessions` 및 `TenacityHours` 속성으로 정의됩니다. 기본값은 6분입니다. 이 속성은 **고급 편집기** 창에 있습니다.|
|UnicodePassThrough|부울|*Off*(기본값): 유니코드 패스 스루를 사용하지 않습니다. <br>*On*: 유니코드 패스 스루를 사용합니다.|

## <a name="configure-the-teradata-source"></a>Teradata 원본 구성

프로그래밍 방식으로 또는 SSIS(SQL Server Integration Services) 디자이너를 사용하여 Teradata 원본을 구성할 수 있습니다.

다음 그림에는 **Teradata 원본 편집기** 창이 나와 있습니다. 자세한 내용은 다음 Teradata 원본 편집기 섹션을 참조하세요.

- [연결 관리자 창](#the-connection-manager-pane)
- [열 창](#the-columns-pane)
- [오류 출력 창](#the-error-output-pane)

![Teradata 원본 편집기](media/teradata-source.png)

**고급 편집기** 창에는 프로그래밍 방식으로 설정할 수 있는 속성이 포함됩니다. 창을 열려면
- Integration Services 프로젝트의 **데이터 흐름** 페이지에서 Oracle 원본을 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시**를 선택합니다.

**고급 편집기** 창에서 설정할 수 있는 속성에 대한 자세한 내용은 [Teradata 원본 사용자 지정 속성](#teradata-source-custom-properties)을 참조하세요.

## <a name="the-connection-manager-pane"></a>연결 관리자 창

**연결 관리자** 창을 사용하여 원본에 대한 Teradata 연결 관리자 인스턴스를 선택할 수 있습니다. 이 창에서 데이터베이스의 테이블 또는 뷰를 선택할 수도 있습니다. 창을 열려면

1. SQL Server Data Tools에서 Teradata 원본을 포함하는 SSIS 패키지를 엽니다.

1. **데이터 흐름** 탭에서 Teradata 원본을 두 번 클릭합니다.

1. Teradata 원본 편집기에서 **연결 관리자** 탭을 선택합니다.

### <a name="options"></a>옵션

**Connection manager**

* 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 선택하여 새 Teradata 연결 관리자 인스턴스를 만듭니다.

**새로 만들기**

* **새 단계**를 선택합니다. **Teradata 연결 관리자 편집기** 창이 열립니다. 이 창에서 새 연결 관리자를 만들 수 있습니다.

**데이터 액세스 모드**

* 원본에서 데이터를 선택하는 방법을 선택합니다. 옵션은 다음 표에 표시되어 있습니다.

    |옵션|Description|
    |:-|:-|
    |테이블 이름 - TPT 내보내기|Teradata 데이터 원본에 있는 테이블이나 뷰에서 데이터를 검색합니다. 이 옵션을 선택한 경우 **테이블 또는 뷰 이름** 목록에서 사용 가능한 테이블 또는 뷰를 선택합니다.|
    |SQL 명령 - TPT 내보내기|SQL 쿼리를 사용하여 Teradata 데이터 원본에서 데이터를 검색합니다. 이 옵션을 선택할 경우 다음 중 한 가지 방법으로 쿼리를 입력합니다. <ul><li>**SQL 명령 텍스트** 필드에 SQL 쿼리 텍스트를 입력합니다.</li><li>**찾아보기**를 선택하여 텍스트 파일에서 SQL 쿼리를 로드합니다.</li><li>**쿼리 구문 분석**을 선택하여 쿼리 텍스트의 구문을 확인합니다.</li></ul>|

**미리 보기**

* **미리 보기**를 선택하여 선택한 테이블 또는 뷰에서 추출된 최대 200개의 데이터 행을 봅니다.

## <a name="the-columns-pane"></a>열 창

**열** 창을 사용하여 출력 열을 각 외부(원본) 열에 매핑할 수 있습니다. 창을 열려면

1. SQL Server Data Tools에서 Teradata 원본을 포함하는 SSIS 패키지를 엽니다.

1. **데이터 흐름** 탭에서 Teradata 원본을 두 번 클릭합니다.

1. Teradata 원본 편집기에서 **열** 탭을 선택합니다.

### <a name="options"></a>옵션

**사용 가능한 외부 열**

이 테이블에는 **외부 열** 목록에 추가하도록 선택할 수 있는 외부 열이 나열됩니다. 열은 선택한 순서로 나열할 수 있습니다. 이 테이블을 사용하여 열을 추가하거나 삭제할 수는 없습니다.

* 모든 열을 선택하려면 **모두 선택** 확인란을 선택합니다.

**외부 열**

선택한 외부(원본) 열은 순서대로 나열됩니다. 순서를 변경하려면 먼저 **사용 가능한 외부 열** 목록을 지운 다음, 다른 순서로 열을 선택합니다.

**출력 열**

선택한 외부(원본) 열의 이름이 기본 출력 이름이기는 하지만 고유한 이름을 입력할 수 있습니다.

>[!NOTE]
>>지원되지 않는 데이터 형식을 포함하는 열이 있는 경우 지원되지 않는 데이터 형식을 표시하는 경고가 표시되고 관련 열이 매핑 열에서 제거됩니다.

## <a name="the-error-output-pane"></a>오류 출력 창

**오류 출력** 창을 사용하여 오류 처리 옵션을 선택할 수 있습니다. 창을 열려면

1. SQL Server Data Tools에서 Teradata 원본을 포함하는 SSIS 패키지를 엽니다.

1. **데이터 흐름** 탭에서 Teradata 원본을 두 번 클릭합니다.

1. Teradata 원본 편집기에서 **오류 출력** 탭을 선택합니다.

### <a name="options"></a>옵션

**오류 동작**

* Teradata 원본이 흐름 오류를 처리할 방법을 선택합니다. 
  * 오류 무시
  * 행 리디렉션
  * 구성 요소 실패

**관련 항목**: [데이터 오류 처리](error-handling-in-data.md)를 참조하세요.

**잘림**

* Teradata 원본이 흐름 잘림을 처리하는 방법을 선택합니다. 
  * 오류 무시
  * 행 리디렉션
  * 구성 요소 실패

## <a name="next-steps"></a>다음 단계

- [Teradata 대상](teradata-destination.md)을 구성합니다.
- 질문이 있는 경우 [기술 커뮤니티](https://aka.ms/AA6iwdw)를 방문하세요.