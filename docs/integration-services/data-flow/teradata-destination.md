---
description: Teradata 대상
title: Teradata 대상 | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 158184ea961aa8938bb0eb2b6f94890dd1eddbfa
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489873"
---
# <a name="teradata-destination"></a>Teradata 대상

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Teradata 대상은 데이터를 Teradata 데이터베이스로 대량 로드합니다.

이 대상은 Teradata 연결 관리자를 사용하여 데이터 원본에 연결합니다. 자세한 내용은 [Teradata 연결 관리자](teradata-connection-manager.md)을 참조하세요.

## <a name="load-options"></a>로드 옵션

Teradata 대상은 다음과 같은 두 가지 데이터 로드 모드를 지원합니다.

- **TPT 스트림**: 이 모드는 TPT API 스트림 연산자(Teradata TPump 프로토콜)를 사용합니다.

- **TPT 로드**(빠른 대량 로드): 이 모드는 빠른 대량 로드를 위해 TPT API 로드 연산자(Teradata FastLoad 프로토콜)를 사용합니다.

빠른 로드 모드에는 다음과 같은 제한 사항이 있습니다.

- Teradata 데이터베이스에 대한 세션 제한은 다음 중 먼저 발생한 요소에 따라 결정됩니다.
    - SESSIONS 명령을 사용하여 설정된 세션 제한
    - 한 세션의 AMP당 Teradata 데이터베이스 제한
    - 애플리케이션당 최대 세션 수에 대한 플랫폼 제한: COP(통신 프로세서) 인터페이스 소프트웨어 파일 CLISPB.DAT에서 MaxSess 변수에 의해 정의됩니다. TDP SET MAXSESSIONS 명령을 사용하여 플랫폼 제한을 지정할 수 있습니다. 기본 제한은 서버 MAXSESS와 같습니다.

- 조인 인덱스는 지원되지 않습니다.
- 대상 테이블의 외래 키 참조는 지원되지 않습니다.
- 보조 인덱스를 사용하여 정의된 대상 테이블은 지원되지 않습니다.

Teradata 빠른 로드 제한 사항에 대한 자세한 내용은 Teradata의 빠른 로드 참조를 참조하세요.

[Teradata 대상 편집기(연결 관리자 페이지)](#teradata-destination-editor-connection-manager-page)에서 모드를 설정할 수 있습니다.

## <a name="error-handling"></a>오류 처리

로드 프로세스 도중 반환되는 오류는 로드 프로세스 도중 잠긴 임시 오류 테이블에 기록됩니다.
고급 편집기의 **최대 오류 수(MaxErrors)** 속성은 이러한 테이블에 기록될 수 있는 최대 오류 수를 설정합니다.

최대 오류 수가 0보다 큰 경우 고유한 이름의 오류 테이블이 생성되고 정보 메시지가 패키지 로그에 출력됩니다. 오류는 표준 SSIS 구성 요소 오류 출력에서 검색할 수 있습니다.

로드 프로세스가 완료되면 임시 테이블은 삭제됩니다. Teradata 대상이 임시 테이블을 읽을 수 없는 경우에는 **항상 오류 테이블 삭제** 속성을 선택한 경우를 제외하고는 테이블이 삭제되지 않습니다.  로드 프로세스가 완료 전에 중지된 경우 필요한 경우 수동으로 이러한 테이블을 삭제해야 합니다. 이러한 테이블은 대상 테이블과 동일한 데이터베이스에 있습니다.

**최대 오류 수** 에 도달하면 대상 테이블 상태는 사용 중인 모드에 따라 달라집니다.

- 빠른 로드 모드에서는 대상 테이블을 사용할 수 없습니다. 다시 실행하려면 대상 테이블을 자르거나 삭제한 후 다시 만들어야 합니다. 롤백은 지원되지 않습니다.
- TPT 스트림 연산자 모드에서 Teradata 대상은 버퍼링된 행 메커니즘을 통해 실행됩니다. 작업이 실패하는 경우 실패 시 완료된 모든 변경 내용(버퍼가 전송됨)은 대상 테이블에서 영구적입니다. 롤백 개념은 없습니다. 오류 테이블은 삭제됩니다.

Teradata 대상에서 오류가 출력됩니다. 자세한 내용은 [Teradata 대상 편집기(오류 출력 페이지)](#teradata-destination-editor-error-output-page)를 참조하세요.

## <a name="parallelism"></a>병렬 처리

빠른 로드 모드에서는 병렬 처리가 제한되며, 여러 개의 독립적인 빠른 로드 작업이 동시에 동일한 테이블에 액세스할 수 없습니다. 또한 동시 빠른 로드 작업 수는 데이터베이스 변수 **MaxLoadTasks** 에 의해 제한됩니다.

TPT 스트림 모드에서는 병렬 처리 제한이 없습니다. 동일한 테이블에 대해 여러 Teradata 대상을 동시에 실행할 수는 있지만 이로 인해 Teradata당 성능이 저하될 수 있습니다. 자세한 내용은 Teradata 설명서를 참조하세요.

## <a name="troubleshooting-the-teradata-destination"></a>Teradata 대상 문제 해결

Teradata 원본이 TPT(Teradata Parallel Transporter) API에 대해 수행하는 호출을 기록할 수 있습니다. 패키지 로깅을 사용하도록 설정하고 패키지 수준에서 **진단** 이벤트를 선택하여 호출을 기록할 수 있습니다.

ODBC 드라이버 관리자 추적을 사용하도록 설정하여 Teradata 원본이 Teradata ODBC 드라이버에 대해 수행하는 ODBC 호출을 기록할 수 있습니다. 자세한 내용은 *ODBC 데이터 원본 관리자를 사용하여 ODBC 추적을 생성하는 방법* 에 대한 Microsoft 설명서를 참조하십시오.

## <a name="teradata-destination-custom-properties"></a>Teradata 대상 사용자 지정 속성

다음 표에서는 Teradata 대상의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.

|속성 이름|데이터 형식|Description|
|:-|:-|:-|
|AlwaysDropErrorTable|부울|기본값은 **False** 입니다. **True** 일 경우 Teradata 대상이 읽기에 실패하더라도 모든 오류 테이블을 삭제합니다.|
|ArraySupport|부울|기본값은 **True** 입니다. **True** 일 경우 DML 그룹이 ArraySupport를 사용합니다. TPT 스트림에만 적용됩니다. 이 속성은 **고급 편집기** 에 있습니다.|
|버퍼|정수|증가시킬 요청 버퍼의 수입니다. 값은 2~64로 설정할 수 있습니다. TPT 스트림에만 적용됩니다. 이 속성은 **고급 편집기** 에 있습니다.|
|BufferMode|부울|기본값은 **True** 입니다. PutBuffer 기능이 사용되는 경우 **True** 이어야 합니다. 이 속성은 **고급 편집기** 에 있습니다.|
|BufferSize|정수|로드 파일 집합을 보내는 데 사용되는 출력 버퍼 크기(KB)입니다. 기본값은 1024입니다. TPT 부하에만 적용됩니다. 이 속성은 **고급 편집기** 에 있습니다.|
|DataEncryption|부울|기본값은 **False** 입니다. **True** 일 경우 전체 보안 암호화가 사용됩니다.|
|DefaultCodePage|정수|데이터 원본에 코드 페이지 정보가 없을 때 사용할 코드 페이지입니다. <br>**참고**: 이 속성은 **고급 편집기** 에 있습니다.|
|DetailedTracingLevel|정수(열거형)|고급 추적에 대해 다음 옵션 중 하나를 선택합니다. <br> **Off**: 고급 로깅을 사용하지 않습니다. <br> **일반**: 드라이버별 작업 일반 추적이 기록됩니다. <br> **CLI**: CLIv2 관련 작업 추적이 기록됩니다. <br> **Notify 메서드**: Notify 기능 관련 작업 추적이 기록됩니다. <br> **공용 라이브러리**: opcommon 라이브러리 작업 추적이 기록됩니다. <br> **모두**: 위의 모든 작업 추적이 기록됩니다. <br> 고급 추적 로그 파일은 **DetailedTracingFile** 속성에 정의되어 있습니다. <br> 이 옵션이 Off가 아닐 경우 **DetailedTracingFile** 속성을 설정해야 합니다. <br> 이 속성은 **고급 편집기** 에 있습니다.|
|DetailedTracingFile|String|**DetailedTracingLevel** 이 **Off** 가 아닐 경우 자동으로 생성되는 로그 파일의 경로입니다. 이 속성은 **고급 편집기** 에 있습니다.|
|DiscardLargeRow|부울|기본값은 **False** 입니다. **True** 일 경우 큰 행(64K 초과)을 삭제합니다.|
|ErrorTableName|String|오류 테이블 이름입니다. 기본값은 대상 테이블 이름입니다.|
|ExtendedStringColumnsAllocation|부울|**True** 일 경우 **최대 전송 문자 할당 인수** 가 사용됩니다. <br> Teradata 데이터베이스 **내보내기 너비 테이블 ID** 속성이 **최대 기본값** 으로 설정된 경우 이 값을 **True** 로 설정해야 합니다. <br> 기본값은 **False** 입니다.|
|FastLoad|부울|**True** 일 경우 빠른 로드가 사용됩니다. 기본 값은 **false** 입니다. [Teradata 대상 편집기(연결 관리자 페이지)](#teradata-destination-editor-connection-manager-page)에서 설정할 수도 있습니다.|
|MaxErrors|정수|데이터 흐름이 중지되기 전에 발생할 수 있는 오류 수입니다. 기본값은 오류 번호 제한이 없음을 의미하는 **0** 입니다.<br> **오류 처리** 페이지에서 **흐름 리디렉션** 을 선택한 경우입니다. 오류 번호 제한에 도달하기 전에 오류 출력에 모든 오류가 반환됩니다. 자세한 내용은 [Teradata 대상 편집기(오류 출력 페이지)](#teradata-destination-editor-error-output-page)를 참조하세요.|
|MaxSessions|정수|로그온된 최대 세션 수입니다. 이 값은 1보다 커야 합니다. 기본값은 사용 가능한 각 AMP마다 1개 세션입니다.|
|MinSessions|정수|로그온된 최소 세션 수입니다. 이 값은 1보다 커야 합니다. 기본값은 사용 가능한 각 AMP마다 1개 세션입니다.|
|Pack|정수|다중 문 요청으로 압축할 문 수입니다. 기본값은 20이고 허용되는 최대 크기는 2400입니다. TPT 스트림에만 적용됩니다. 이 속성은 **고급 편집기** 에 있습니다.|
|PackMaximum|부울|**True** 일 경우 현재 스트림 작업의 최대 팩 인수를 동적으로 결정합니다. TPT 스트림에만 적용됩니다. 이 속성은 **고급 편집기** 에 있습니다.|
|QueryBandSessInfo|Varchar|사용자가 정의한 세션 기반 쿼리 밴드 식으로, 이를 통해 차지백 모니터링 및 거버넌스를 사용할 수 있습니다. 이 속성은 연결 문자열 형식이어야 합니다. 이 속성은 **고급 편집기** 에 있습니다.|
|ReplicationOveride|Integer(열거형)|옵션: <br> **기본값**: SET SESSION OVERRIDE REPLICATION 문이 데이터베이스로 전송되지 않습니다. 데이터베이스 기본 설정이 사용됩니다. <br> **On**: 일반 복제 서비스 컨트롤이 재정의됩니다. <br> **Off**: 일반 복제 서비스 컨트롤이 사용됩니다. <br> 이 속성은 TPT 스트림에만 적용됩니다. <br> 이 속성은 **고급 편집기** 에 있습니다.|
|Robust|부울|**True** 일 경우 복구 및 다시 시작 작업에 강력한 다시 시작 논리가 사용됩니다. 이 속성은 **TPT 스트림** 에만 적용됩니다. 이 속성은 **고급 편집기** 에 있습니다.|
|TableName|String|사용되는 데이터가 포함된 테이블의 이름입니다.|
|TenacityHours|정수|최대 수의 로드/내보내기 작업이 이미 실행 중인 경우 TPT 드라이버가 로그온을 시도하는 시간(시)입니다. 기본값은 4시간입니다. 이 속성은 **고급 편집기** 에 있습니다.|
|TenacitySleep|정수|제한에 도달했을 때 로그온을 시도하기 전에 TPT 드라이버가 일시 중지되는 시간(분)입니다. 제한은 **MaxSessions** 및 **TenacityHours** 속성으로 정의됩니다. 기본값은 6분입니다. 이 속성은 **고급 편집기** 에 있습니다.|
|UnicodePassThrough|부울|Off(기본값): 유니코드 패스 스루를 사용하지 않습니다. <br>On: 유니코드 패스 스루를 사용합니다.|

## <a name="configuring-the-teradata-destination"></a>Teradata 대상 구성

프로그래밍 방식으로 또는 SSIS 디자이너를 사용하여 Teradata 대상을 구성할 수 있습니다.

아래 그림에는 Teradata 대상 편집기가 나와 있습니다. 여기에는 연결 관리자 페이지, 매핑 페이지 및 오류 출력 페이지가 포함되어 있습니다.

자세한 내용은 다음 항목 중 하나를 참조하십시오.

- [Teradata 대상 편집기(연결 관리자 페이지)](#teradata-destination-editor-connection-manager-page)
- [Teradata 대상 편집기(매핑 페이지)](#teradata-destination-editor-mappings-page)
- [Teradata 대상 편집기(오류 출력 페이지)](#teradata-destination-editor-error-output-page)

![대상 편집기](media/teradata-destination.png)

**고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 포함됩니다.
**고급 편집기** 대화 상자를 열려면

- Integration Services 프로젝트의 **데이터 흐름** 화면에서 Teradata 대상을 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시** 를 선택합니다.

고급 편집기 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [Teradata 대상 사용자 지정 속성](#teradata-destination-custom-properties)을 참조하세요.

## <a name="teradata-destination-editor-connection-manager-page"></a>Teradata 대상 편집기(연결 관리자 페이지)

**Teradata 대상 편집기** 대화 상자의 **연결 관리자 페이지** 를 사용하여 대상에 대한 Teradata 연결 관리자를 선택할 수 있습니다. 이 페이지를 사용하면 데이터베이스에서 테이블이나 뷰를 선택할 수도 있습니다.

Teradata 대상 편집기 연결 관리자 페이지를 열려면

- SQL Server Data Tools에서 Teradata 대상이 있는 SSIS(SQL Server Integration Services) 패키지를 엽니다.

- 데이터 흐름 탭에서 Teradata 대상을 두 번 클릭합니다.

- Teradata 대상 편집기에서 연결 관리자를 클릭합니다.

### <a name="options"></a>옵션

**Connection manager**

목록에서 기존 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 Teradata 연결 관리자를 만듭니다.

**새로 만들기**

**새로 만들기** 를 클릭합니다. 새 연결 관리자를 만들 수 있는 **Teradata 연결 관리자 편집기** 대화 상자가 열립니다.

**데이터 액세스 모드**

원본에서 데이터를 선택하는 방법을 선택합니다. 옵션은 다음 표에 표시되어 있습니다.

|옵션|Description|
|:-|:-|
|테이블 이름 - TPT 스트림|TPT 스트림 연산자를 사용하는 증분 모드입니다. <br>**테이블 또는 뷰 이름**: 목록에서 기존 테이블 또는 뷰를 선택합니다. 이 목록에는 처음 1000개 테이블만 표시됩니다. 테이블 이름 접두사를 입력하거나 이름 중 일부에 (*) 와일드카드를 사용하여 사용하려는 테이블을 나열할 수 있습니다.|
|테이블 이름 – TPL 로드|TPT API 로드 연산자(Teradata FastLoad 프로토콜)를 사용하는 빠른(직접 경로) 로드 모드로, 대상 테이블이 비어 있어야 합니다. <br>**테이블 또는 뷰 이름**: 목록에서 기존 테이블 또는 뷰를 선택합니다. 이 목록에는 처음 1000개 테이블만 표시됩니다. 테이블 이름 접두사를 입력하거나 이름 중 일부에 (*) 와일드카드를 사용하여 사용하려는 테이블을 나열할 수 있습니다.|

**데이터 암호화** 데이터 암호화를 사용하도록 설정하기 위한 확인란입니다. 기본적으로 선택되어 있지 않습니다.

**항상 오류 테이블 삭제** 모든 인스턴스에 오류 테이블을 삭제하기 위한 확인란입니다.

**오류 테이블** 오류를 기록하는 테이블의 이름입니다.

**최소 세션 수** 로그온된 최소 세션 수입니다. 기본값은 사용 가능한 각 AMP마다 1개 세션입니다. 이 값은 1보다 커야 합니다.

**최대 세션 수** 로그온된 최대 세션 수입니다. 기본값은 사용 가능한 각 AMP마다 1개 세션입니다. 이 값은 1보다 커야 합니다.

**최대 오류 수** 데이터 흐름을 중지하거나 리디렉션하기 전에 반환될 수 있는 최대 오류 수입니다. 

## <a name="teradata-destination-editor-mappings-page"></a>Teradata 대상 편집기(매핑 페이지)

**Teradata 대상 편집기** 대화 상자의 **매핑** 페이지를 사용하여 입력 열을 대상 열에 매핑할 수 있습니다.

Teradata 대상 편집기 매핑 페이지를 열려면

- SQL Server Data Tools에서 Teradata 대상이 있는 SSIS(SQL Server Integration Services) 패키지를 엽니다.

- 데이터 흐름 탭에서 Teradata 대상을 두 번 클릭합니다.

- Teradata 대상 편집기에서 매핑을 클릭합니다.

### <a name="options"></a>옵션

**사용 가능한 입력 열**

사용 가능한 입력 열 목록입니다. 입력 열을 사용 가능한 대상 열에 끌어 놓아 열을 매핑할 수 있습니다.

**사용 가능한 대상 열**

사용 가능한 대상 열 목록입니다. 대상 열을 사용 가능한 입력 열에 끌어 놓아 열을 매핑할 수 있습니다.

**입력 열**

선택한 입력 열을 표시합니다. 출력에서 열을 제외하는 **< ignore >** 를 선택하여 매핑을 제거할 수 있습니다.

**대상 열**

사용 가능한 모든 대상 열(매핑되거나 매핑되지 않음)을 표시합니다.

>[!NOTE]
>
>지원되지 않는 데이터 형식 열은 경고를 발생하면서 매핑에서 삭제됩니다.

## <a name="teradata-destination-editor-error-output-page"></a>Teradata 대상 편집기(오류 출력 페이지)
Teradata 대상 편집기 대화 상자의 오류 출력 페이지를 사용하여 오류 처리 옵션을 선택할 수 있습니다.

**Teradata 대상 편집기 오류 출력 페이지를 열려면**

- SQL Server Data Tools에서 Teradata 대상이 있는 SSIS(SQL Server Integration Services) 패키지를 엽니다.

- 데이터 흐름 탭에서 Teradata 대상을 두 번 클릭합니다.

- Teradata 대상 편집기에서 오류 출력을 클릭합니다.

### <a name="options"></a>옵션

**오류 동작**

Teradata 대상에서 흐름 오류를 처리하는 방법을 선택합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.

**관련 항목**: [데이터 오류 처리](./error-handling-in-data.md)

**잘림**

Teradata 대상에서 흐름 잘림을 처리하는 방법을 선택합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [Teradata 연결 관리자](teradata-connection-manager.md) 구성
- [Teradata 원본](teradata-source.md) 구성
- [Teradata 대상](teradata-destination.md) 구성
- 질문이 있는 경우 [Tech Community](https://aka.ms/AA6iwdw)를 방문하세요.
