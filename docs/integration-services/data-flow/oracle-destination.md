---
title: Oracle 대상 | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9ee964e5c1c58ea54da3f3451c0ffdde29e71b23
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246936"
---
# <a name="oracle-destination"></a>Oracle 대상

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Oracle 대상은 데이터를 Oracle Database에 대량으로 로드합니다.

이 대상은 Oracle 연결 관리자를 사용하여 데이터 원본에 연결합니다. 자세한 내용은 [Oracle 연결 관리자](oracle-connection-manager.md)를 참조하세요.

Oracle 대상에는 입력 열과 대상 데이터 원본 열 사이의 매핑이 포함됩니다. 입력 열을 모든 대상 열로 매핑할 필요는 없지만 입력 열이 대상 열에 매핑되지 않은 경우 대상 열의 속성에 따라 오류가 발생할 수 있습니다. 예를 들어 대상 열에 Null 값이 허용되지 않는 경우에는 입력 열을 해당 열에 매핑해야 합니다. 또한 입력 데이터가 대상 열 유형과 호환되지 않으면 런타임에 오류가 발생합니다. 오류 동작 설정에 따라 오류가 무시되거나, 오류가 발생하거나, 행이 오류 출력으로 리디렉션됩니다.

Oracle 대상에는 하나의 일반 입력과 하나의 오류 출력이 있습니다.

매핑 전에 경고를 사용하여 열에서 지원되지 않는 데이터 형식 열이 삭제됩니다.
자세한 내용은 [데이터 형식 지원](oracle-data-type-support.md)을 참조하세요.

## <a name="load-options"></a>로드 옵션

두 개의 액세스 로드 모드가 지원됩니다. 모드는 [Oracle 대상 편집기(연결 관리자 페이지)](#oracle-destination-editor-connection-manager-page)에서 설정할 수 있습니다. 두 모드는 다음과 같습니다.

- 일괄 로드: 이 모드는 데이터를 Oracle 테이블에 일괄로 로드하고 동일한 트랜잭션에 전체 일괄 처리를 삽입합니다.
이 모드를 구성하는 방법에 대한 자세한 내용은 [Oracle 대상 편집기(연결 관리자 페이지)](#oracle-destination-editor-connection-manager-page) 및 [Oracle 대상 사용자 지정 속성](#oracle-destination-custom-properties)을 참조하세요.

- 직접 경로를 사용하는 빠른 로드: 이 모드는 Oracle 테이블을 로드하기 위해 드라이버의 직접 경로 모드를 사용하는 것입니다. 이 모드를 사용할 때는 다음과 같은 제한 사항이 있습니다. 자세한 내용은 Oracle 설명서를 참조하세요.  
이 모드를 구성하는 방법에 대한 자세한 내용은 [Oracle 대상 편집기(연결 관리자 페이지)](#oracle-destination-editor-connection-manager-page) 및 [Oracle 대상 사용자 지정 속성](#oracle-destination-custom-properties)을 참조하세요.

## <a name="error-handling"></a>오류 처리

Oracle 대상에는 하나의 오류 출력이 있습니다. 구성 요소 오류 출력에 다음과 같은 출력 열이 포함됩니다.

- **오류 코드**: 현재 오류의 오류 유형을 나타내는 숫자입니다. 오류 코드는 다음에서 제공될 수 있습니다.
    - Oracle 서버. Oracle 데이터베이스 설명서의 자세한 오류 설명을 참조하세요.
    - SSIS 런타임. SSIS 오류 코드 목록은 SSIS 오류 코드 및 메시지 참조를 참조하십시오.
- **오류 열**: 변환 오류를 유발하는 원본 열 번호입니다.

- **오류 데이터 열**: 오류의 원인이 되는 데이터입니다.

지원되는 로드 프로세스 동안의 출력 오류의 유형으로, 데이터 변환, 잘림 또는 제약 조건 위반 등이 있습니다. [Oracle 대상 편집기(오류 출력 페이지)](#oracle-destination-editor-error-output-page)를 참조하세요.

**최대 오류 개수(MaxErrors)** 속성은 발생할 수 있는 최대 오류 수를 설정합니다. 최대 개수에 도달하면 실행이 중지되고 오류가 반환됩니다. 최대 오류 수에 도달하기 전의 실행 레코드만 대상 테이블에 포함됩니다. 자세한 구성은 [Oracle 대상 편집기(연결 관리자 페이지)](#oracle-destination-editor-connection-manager-page)를 참조하세요.

## <a name="parallelism"></a>병렬 처리

일괄 로드 모드에서는 병렬 실행의 구성에 제한이 없지만, 성능이 표준 레코드 잠금 메커니즘의 영향을 받을 수 있습니다. 성능 손실의 양은 데이터와 테이블 구성에 따라 달라집니다.

직접 경로 프로토콜(빠른 로드)에서는 동일한 테이블에 대해 하나의 Oracle 대상만 동시에 실행되도록 구성할 수 있지만 병렬 모드를 사용할 수 있습니다.

병렬 직접 경로를 사용하면 여러 직접 경로 로드가 허용되므로 동일한 테이블에 대해 여러 Oracle 대상을 동시에 실행하도록 구성할 수 있습니다. Oracle은 빠른 로드 세션에서 단독으로 사용하기 위해 대상 테이블을 잠그지 않으므로 추가적인 빠른 로드 대상 구성 요소를 실행하여 동일한 대상 테이블을 동시에 로드할 수 있도록 합니다.
병렬 직접 경로는 미리 계획해야 하는 좀 더 제한적인 병렬 처리 방식입니다.

단일 병렬 세션을 사용할 이유는 없습니다.

병렬 직접 경로 로드를 사용할 때의 제한 사항에 대해서는 Oracle 설명서를 참조하세요.

자세한 내용은 [Oracle 대상 사용자 지정 속성](#oracle-destination-custom-properties)을 참조하세요.

## <a name="troubleshooting-the-oracle-destination"></a>Oracle 대상 문제 해결

Oracle 원본이 Oracle 데이터 원본에 대해 수행하는 ODBC 호출을 기록하여 데이터 내보내기 문제를 해결할 수 있습니다. Oracle 원본이 Oracle 데이터 원본에 대해 수행하는 ODBC 호출을 기록하려면 ODBC 드라이버 관리자 추적을 사용하도록 설정합니다. 자세한 내용은 *ODBC 데이터 원본 관리자를 사용하여 ODBC 추적을 생성하는 방법*에 대한 Microsoft 설명서를 참조하십시오.

## <a name="oracle-destination-custom-properties"></a>Oracle 대상 사용자 지정 속성

다음 표에서는 Oracle 대상의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.

|속성 이름|데이터 형식|Description|로드 모드|
|:-|:-|:-|:-|
|BatchSize|정수|대량 로드에 대한 일괄 처리 크기입니다. 일괄 처리로 로드되는 행의 개수입니다.|일괄 처리 모드에서만 사용됩니다.|
|DefaultCodePage|정수|데이터 원본에 코드 페이지 정보가 없을 때 사용할 코드 페이지입니다. <br>**참고**: 이 속성은 **고급 편집기**에서만 설정됩니다.|두 모드에 사용합니다.|
|FastLoad|부울|빠른 로드 사용 여부입니다. 기본 값은 **false**입니다. [Oracle 대상 편집기(연결 관리자 페이지)](#oracle-destination-editor-connection-manager-page)에서 설정할 수도 있습니다. |두 모드에 사용합니다.|
|MaxErrors|정수|데이터 흐름이 중지되기 전에 발생할 수 있는 오류 수입니다. 기본값은 오류 번호 제한이 없음을 의미하는 **0**입니다.<br> **오류 처리** 페이지에서 **흐름 리디렉션**을 선택한 경우입니다. 오류 번호 제한에 도달하기 전에 오류 출력에 모든 오류가 반환됩니다. 자세한 내용은 [오류 처리](#error-handling)를 참조하세요.|빠른 로드 모드에서만 사용됩니다.|
|NoLogging|부울|데이터베이스 로깅을 사용하지 않도록 설정할지 여부입니다. 기본값은 로깅을 사용하도록 설정함을 의미하는 **False**입니다.|두 모드에 사용합니다.|
|병렬|부울|병렬 로드 허용 여부입니다. **True**는 다른 로드 세션이 동일한 대상 테이블에 대해 실행될 수 있음을 나타냅니다.<br> 자세한 내용은 [병렬 처리](#parallelism)를 참조하세요.|빠른 로드 모드에서만 사용됩니다.|
|TableName|String|사용되는 데이터가 포함된 테이블의 이름입니다.|두 모드에 사용합니다.|
|TableSubName|String|하위 이름 또는 하위 파티션입니다. 이 값은 선택 사항입니다.<br> **참고**: 이 속성은 **고급 편집기**에서만 설정할 수 있습니다.|빠른 로드 모드에서만 사용됩니다.|
|TransactionSize|정수|단일 트랜잭션에서 수행할 수 있는 삽입 수입니다. 기본값은 **BatchSize**입니다.|일괄 처리 모드에서만 사용됩니다.|
|TransferBufferSize|정수|전송 버퍼의 크기입니다. 기본값은 64KB입니다.|빠른 로드 모드에서만 사용됩니다.|

## <a name="configuring-the-oracle-destination"></a>Oracle 대상 구성

SSIS 디자이너를 사용하거나 프로그래밍 방식으로 Oracle 대상을 구성할 수 있습니다.

Oracle 대상 편집기는 아래 그림에 나와 있습니다. 여기에는 연결 관리자 페이지, 매핑 페이지 및 오류 출력 페이지가 포함되어 있습니다.

자세한 내용은 다음 섹션 중 하나를 참조하세요.

- [Oracle 대상 편집기(연결 관리자 페이지)](#oracle-destination-editor-connection-manager-page)
- [Oracle 대상 편집기(매핑 페이지)](#oracle-destination-editor-mappings-page)
- [Oracle 대상 편집기(오류 출력 페이지)](#oracle-destination-editor-error-output-page)

![Oracle 대상](media/oracle-destination.png)

**고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 포함됩니다.
**고급 편집기** 대화 상자를 열려면

- Integration Services 프로젝트의**데이터 흐름** 화면에서 Oracle 대상을 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시**를 선택합니다.

고급 편집기 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [Oracle 대상 사용자 지정 속성](#oracle-destination-custom-properties)을 참조하세요.

## <a name="oracle-destination-editor-connection-manager-page"></a>Oracle 대상 편집기(연결 관리자 페이지)

**Oracle 대상 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 대상에 대한 Oracle 연결 관리자를 선택할 수 있습니다. 이 페이지를 사용하면 데이터베이스에서 테이블이나 뷰를 선택할 수도 있습니다.

**Oracle 대상 편집기의 연결 관리자 페이지를 열려면**

- SQL Server Data Tools에서 Oracle 대상이 있는 SSIS(SQL Server Integration Services) 패키지를 엽니다.

- 데이터 흐름 탭에서 Oracle 대상을 두 번 클릭합니다.

- Oracle 대상 편집기에서 연결 관리자를 클릭합니다.

### <a name="options"></a>옵션

**Connection manager**

목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 Oracle 연결 관리자를 만듭니다.

**새로 만들기**

**새로 만들기**를 클릭합니다. 새 연결 관리자를 만들 수 있는 **Oracle 연결 관리자 편집기** 대화 상자가 열립니다.

**데이터 액세스 모드**

원본에서 데이터를 선택하는 방법을 선택합니다. 옵션은 다음 표에 표시되어 있습니다.

|옵션|Description|
|:-|:-|
|테이블 이름|일괄 처리 모드에서 작동하도록 Oracle 대상을 구성합니다. 옵션:<br><br> **테이블 또는 뷰 이름**: 목록의 데이터베이스에서 사용 가능한 테이블이나 뷰를 선택합니다.<br><br> **트랜잭션 크기**: 단일 트랜잭션에서 수행할 수 있는 삽입 수를 입력합니다. 기본값은 **BatchSize**입니다.<br><br> **일괄 처리 크기**: 대량 로드에 대한 일괄 처리 크기(로드한 행 수)를 입력합니다.
|테이블 이름 – 빠른 로드|빠른(직접 경로) 로드 모드에서 작동하도록 Oracle 대상을 구성합니다. <br><br>다음과 같은 옵션을 사용할 수 있습니다.<br><br> **테이블 또는 뷰 이름**: 목록의 데이터베이스에서 사용 가능한 테이블이나 뷰를 선택합니다.<br><br> **병렬 로드**: 병렬 로드 사용 여부입니다. 자세한 내용은 [병렬 처리](#parallelism)를 참조하세요.<br><br> **로깅 안 함**: 데이터베이스 로깅을 사용하지 않도록 설정하기 위한 확인란입니다. 이 로깅은 추적이 아닌 복구 목적으로 사용되는 Oracle 데이터베이스입니다.<br><br> **최대 오류 개수**: 데이터 흐름이 중지되기 전에 발생할 수 있는 최대 오류 수입니다. 기본값은 개수 제한이 없음을 의미하는 0입니다.<br><br> 오류 출력에 모든 오류가 반환될 수 있습니다.<br><br> **전송 버퍼 크기(KB)** : 전송 버퍼의 크기를 입력합니다. 기본 크기는 64KB입니다.|

**기존 데이터 보기**

**기존 데이터 보기**를 클릭하면 선택한 테이블의 데이터 행을 최대 200개까지 볼 수 있습니다.

## <a name="oracle-destination-editor-mappings-page"></a>Oracle 대상 편집기(매핑 페이지)

**Oracle 대상 편집기** 대화 상자의 **매핑** 페이지를 사용하여 입력 열을 대상 열에 매핑할 수 있습니다.

**Oracle 대상 편집기(매핑 페이지)를 열려면**

- SQL Server Data Tools에서 Oracle 대상이 있는 SSIS(SQL Server Integration Services) 패키지를 엽니다.

- 데이터 흐름 탭에서 Oracle 대상을 두 번 클릭합니다.

- Oracle 대상 편집기에서 매핑을 클릭합니다.

### <a name="options"></a>옵션

**사용 가능한 입력 열**

사용 가능한 입력 열 목록입니다. 입력 열을 사용 가능한 대상 열에 끌어 놓아 열을 매핑할 수 있습니다.

**사용 가능한 대상 열**

사용 가능한 대상 열 목록입니다. 대상 열을 사용 가능한 입력 열에 끌어 놓아 열을 매핑할 수 있습니다.

**입력 열**

선택한 입력 열을 표시합니다. 출력에서 열을 제외하는 **< ignore >** 를 선택하여 매핑을 제거할 수 있습니다.

**대상 열**

사용 가능한 모든 대상 열(매핑되거나 매핑되지 않음)을 표시합니다.

> [!NOTE]
>
>지원되지 않는 데이터 형식 열은 경고를 발생하면서 매핑에서 삭제됩니다.

## <a name="oracle-destination-editor-error-output-page"></a>Oracle 대상 편집기(오류 출력 페이지)

Oracle 대상 편집기 대화 상자의 오류 출력 페이지를 사용하여 오류 처리 옵션을 선택할 수 있습니다.

**Oracle 대상 편집기 오류 출력 페이지를 열려면**

- SQL Server Data Tools에서 Oracle 대상이 있는 SSIS(SQL Server Integration Services) 패키지를 엽니다.

- 데이터 흐름 탭에서 Oracle 대상을 두 번 클릭합니다.

- Oracle 대상 편집기에서 오류 출력을 클릭합니다.

### <a name="options"></a>옵션

**오류 동작**

Oracle 원본에서 흐름의 오류를 처리하는 방법을 선택합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.
**관련 섹션**: [데이터 오류 처리](https://docs.microsoft.com/sql/integration-services/data-flow/error-handling-in-data?view=sql-server-2017)

**잘림**

Oracle 원본에서 흐름의 잘림을 처리하는 방법을 선택합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [Oracle 연결 관리자](oracle-connection-manager.md)를 구성합니다.
- [Oracle 원본](oracle-source.md)을 구성합니다.
- [Oracle 대상](oracle-destination.md)을 구성합니다.
- 질문이 있는 경우 [TechCommunity](https://aka.ms/AA5u35j)을 방문하세요.
