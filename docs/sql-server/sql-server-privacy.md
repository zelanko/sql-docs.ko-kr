---
title: SQL Server 개인 정보 제공 | Microsoft Docs
ms.date: 4/24/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords: ''
helpviewer_keywords: ''
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 4842d7749f41864697e0a6a24f522f1f8e9ca4f8
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
---
# <a name="sql-server-privacy-supplement"></a>SQL Server 개인 정보 제공
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서서는 SQL Server 내에서 사용되는 다양한 데이터 개체의 동작 및 개인적 또는 기밀 방식으로 정보를 전달하는 데 개체를 사용하는 방법을 요약합니다. 이 문서는 전반적인 [Microsoft 개인정보처리방침](https://go.microsoft.com/fwlink/?LinkId=521839)에 대한 추록입니다. 이 문서에서 데이터 분류는 SQL Server 온-프레미스 제품의 버전에만 적용됩니다. 항목에 적용되지 않습니다.

- Azure SQL 데이터베이스
- SSMS(SQL Server Management Studio)
- SQL  Server  Data  Tools(SSDT)
- SQL Operations Studio
- Data Migration Assistant
- SQL Server 마이그레이션 길잡이
- MS-SQL 확장

*허용된 사용 시나리오*의 정의입니다. Microsoft는 이 문서의 컨텍스트에서 Microsoft에서 시작된 작업이나 작업으로 "허용된 사용 시나리오"를 정의합니다.

## <a name="access-control"></a>액세스 제어

SQL Server 설치 내에서 로그인, 사용자 또는 계정을 보호하는 데 사용되는 자격 증명 관련 정보입니다.

### <a name="examples-of-access-control"></a>액세스 제어의 예제

- 암호
- 인증서

### <a name="permitted-usage-scenarios"></a>허용된 사용 시나리오

|시나리오  |액세스 제한  |보존 요구 사항 |
|---------|---------|---------|
|이러한 자격 증명은 사용 피드백을 통해 사용자 컴퓨터를 벗어나지 않습니다.     |-         |-         |
|크래시 덤프는 액세스 제어 데이터를 포함할 수 있습니다.     |-         |크래시 덤프: 최대 30일입니다.         |
|고객이 수동으로 삽입하지 않으면 이러한 자격 증명은 사용자 피드백을 통해 사용자 컴퓨터를 벗어나지 않습니다.    |타사 액세스 권한 없이 Microsoft 내부 사용량을 제한합니다.         |사용자 피드백: 최대 1년         |
 |
## <a name="customer-content"></a>고객 콘텐츠

고객 콘텐츠는 직접 또는 간접적으로 사용자 테이블 내에 저장된 데이터로 정의됩니다. 데이터에는 사용자 테이블 내에 저장될 수 있는 쿼리 텍스트 내의 통계 또는 사용자 리터럴이 포함됩니다.

### <a name="examples-of-customer-content"></a>고객 콘텐츠의 예제

- 사용자 테이블의 행 내에 저장된 데이터 값입니다.
- 사용자 테이블의 행 내에서 값의 복사본을 포함하는 통계 개체입니다.
- 리터럴 값이 포함된 텍스트를 쿼리합니다.

### <a name="permitted-usage-scenarios"></a>허용된 사용 시나리오
|시나리오  |액세스 제한  |보존 요구 사항 |
|---------|---------|---------|
|이 데이터는 사용 피드백을 통해 사용자 컴퓨터를 벗어나지 않습니다. |- |- |
|크래시 덤프에는 고객 콘텐츠가 포함되고 Microsoft로 내보내집니다. |- |크래시 덤프: 최대 30일입니다. |
|동의하는 고객은 Microsoft에 고객 콘텐츠를 포함하는 사용자 피드백을 보낼 수 있습니다. |타사 액세스 권한 없이 Microsoft 내부를 제한합니다. Microsoft에서는 원래 고객에게 데이터를 노출할 수 있습니다. |사용자 피드백: 최대 1년 |

## <a name="end-user-identifiable-information-euii"></a>EUII(최종 사용자 식별 가능 정보)

사용자로부터 받거나 제품을 사용하여 생성된 데이터입니다.
- 개별 사용자에게 연결 가능합니다.
- 콘텐츠를 포함하지 않습니다.

### <a name="examples-of-end-user-identifiable-information"></a>예제 최종 사용자 식별 가능 정보의 예

- 인터페이스 식별 전체 IP 주소
- 컴퓨터 이름
- 로그인/사용자 이름
- 이메일 주소의 로컬 부분(joe@contoso.com)
- 위치 정보
- 고객 ID

### <a name="permitted-usage-scenarios"></a>허용된 사용 시나리오

|시나리오  |액세스 제한  |보존 요구 사항|
|---------|---------|---------|
|이 데이터는 사용 피드백을 통해 사용자 컴퓨터를 벗어나지 않습니다. |- |- |
|크래시 덤프에는 EUII가 포함되고 Microsoft로 내보내집니다. |- |크래시 덤프: 최대 30일 |
|고객 식별 ID를 Microsoft에 내보내서 사용자가 구독하는 새로운 하이브리드 및 클라우드 기능을 제공할 수 있습니다. |- |현재 이러한 하이브리드 또는 클라우드 기능이 존재하지 않습니다.|
|동의하는 고객은 Microsoft에 고객 콘텐츠를 포함하는 사용자 피드백을 보낼 수 있습니다.|타사 액세스 권한 없이 Microsoft 내부 사용량을 제한합니다. Microsoft에서는 원래 고객에게 데이터를 노출할 수 있습니다. |사용자 피드백: 최대 1년 |

## <a name="internet-based-services-data"></a>인터넷 기반 서비스 데이터

SQL Server EULA당 인터넷 기반 서비스를 제공하는 데 필요한 데이터입니다.

### <a name="examples-of-internet-based-services-data"></a>인터넷 기반 서비스 데이터의 예제

- 컴퓨터 사양 정보
- 브라우저 이름/버전
- SQL Server 버전
- 언어 코드
- 특정 옥텟이 제거된 IP 주소
- 맵 데이터

### <a name="permitted-usage-scenarios"></a>허용된 사용 시나리오

|시나리오  |액세스 제한  |보존 요구 사항|
|---------|---------|---------| 
|현재 기능에서 기능 개선 및/또는 버그 수정을 수행하기 위해 Microsoft에서 사용할 수 있습니다. |타사 액세스 권한 없이 Microsoft 내부 사용량을 제한합니다. Microsoft에서는 원래 고객에게 데이터를 노출할 수 있습니다.  예: 대시보드 |최소 90일 - 최대 3년 |
|동의하는 고객은 Microsoft에 고객 콘텐츠를 포함하는 사용자 피드백을 보낼 수 있습니다. |타사 액세스 권한 없이 Microsoft 내부 사용량을 제한합니다. |동의하는 고객은 Microsoft에 고객 콘텐츠를 포함하는 사용자 피드백을 보낼 수 있습니다. |
|파워 뷰 및 SQL Reporting Services Map 항목은 Bing Maps를 사용하기 위해 데이터를 전송할 수 있습니다. |세션 데이터에 대한 제한 사항 |- |

## <a name="system-metadata"></a>시스템 메타데이터

서버를 실행하는 과정에서 생성된 데이터입니다.  데이터에는 고객 콘텐츠가 포함되지 않습니다.

### <a name="examples-of-system-metadata"></a>시스템 메타데이터의 예제

다음은 고객 콘텐츠, 고객 액세스 제어 또는 EUII가 포함되지 않는 경우 시스템 메타데이터를 사용합니다.

- 데이터베이스 GUID
- 컴퓨터 이름 해시
- 인스턴스 이름 해시
- 응용 프로그램 이름
- 동작/사용량 데이터
- SQLCEIP(SQL 사용자 환경 개선 프로그램 데이터)
- 서버 구성 데이터(예: sp_configure)
- 기능 구성 데이터
- 이벤트 이름 및 오류 코드

Microsoft는 SQL Server를 사용하는 다른 프로그램에서 설정한 응용 프로그램 이름 값을 검사합니다. (예: Sharepoint 또는 타사 패키지 프로그램 및 사용량 데이터가 활성화되면 Microsoft에 전송되는 시스템 메타데이터에 이 정보가 포함됩니다.) 고객은 시스템 메타데이터 필드에서 최종 사용자 식별 가능 정보와 같은 개인 데이터를 배치하거나 이러한 필드에서 개인 데이터를 저장하도록 디자인된 응용 프로그램을 만들지 않아야 합니다. 

### <a name="permitted-usage-scenarios"></a>허용된 사용 시나리오

|시나리오  |액세스 제한  |보존 요구 사항|
|---------|---------|---------|
|현재 기능에서 기능 개선 및/또는 버그 수정을 수행하기 위해 Microsoft에서 사용할 수 있습니다.|타사 액세스 권한 없이 Microsoft 내부 사용량을 제한합니다. |최소 90일 - 최대 3년 |
|고객에게 제안하는 데 사용할 수 있습니다.  예를 들어 "제품의 사용량에 따라 성능이 향상되기 때문에 기능 *X*를 사용하는 것이 좋습니다." |Microsoft에서는 원래 고객에게 데이터를 노출할 수 있습니다(예: 대시보드를 통해). |고객 데이터 보안 로그: 최소 3년 - 최대 6년 |
향후 제품 계획을 위해 Microsoft에서 사용할 수 있습니다. |Microsoft는 해당 제품이 Microsoft 소프트웨어로 실행되는 방법을 개선하기 위해 다른 하드웨어 및 소프트웨어 공급 업체와 이 정보를 공유할 수 있습니다. |최소 90일 - 최대 3년|
|내보낸 사용량 피드백에 따라 클라우드 기반 서비스를 제공하기 위해 Microsoft에서 사용할 수 있습니다. 예를 들어 고객 대시보드는 조직에서 설치된 모든 SQL Server에 대한 기능 사용량을 표시합니다. |Microsoft에서는 원래 고객에게 데이터를 노출할 수 있습니다(예: 대시보드를 통해). |최소 90일 - 최대 3년 |
|동의하는 고객은 Microsoft에 고객 콘텐츠를 포함하는 사용자 피드백을 보낼 수 있습니다. |타사 액세스 권한 없이 Microsoft 내부를 제한합니다. Microsoft에서는 원래 고객에게 데이터를 노출할 수 있습니다. |사용자 피드백: 최대 1년 |
|데이터베이스 이름과 응용 프로그램 이름을 사용하여 데이터베이스와 응용 프로그램을 알려진 범주(예: Microsoft 또는 다른 회사에서 제공하는 소프트웨어를 실행하는 범주)로 분류할 수 있습니다.|타사 액세스 권한 없이 Microsoft 내부를 제한합니다.|최소 90일 - 최대 3년 |

## <a name="object-metadata"></a>개체 메타데이터

서버, 데이터베이스, 테이블 및 기타 리소스를 구성하는 방법을 설명하고 사용되는 데이터입니다.  개체 메타데이터에는 데이터베이스 테이블 및 열 이름이 포함되지만 데이터베이스 행의 콘텐츠 또는 기타 고객 콘텐츠를 포함하지 않습니다. 고객은 개체 메타데이터 필드에서 최종 사용자 식별 가능 정보와 같은 개인 데이터를 배치하거나 이러한 필드에서 개인 데이터를 저장하도록 디자인된 응용 프로그램을 만들지 않아야 합니다. 아래 허용된 사용 시나리오의 경우 제품 개선을 위한 사용 패턴을 판단할 때 해시 양식만 사용됩니다. 

### <a name="examples-of-object-metadata"></a>개체 메타데이터의 예제

- SQL Server 데이터베이스 이름
- 테이블 이름 및 열 이름
- 통계 이름

### <a name="permitted-usage-scenarios"></a>허용된 사용 시나리오

|시나리오  |액세스 제한  |보존 요구 사항|
|---------|---------|---------|
|현재 기능에서 기능 개선 및/또는 버그 수정을 수행하기 위해 Microsoft에서 사용할 수 있습니다. |타사 액세스 권한 없이 Microsoft 내부 사용량을 제한합니다. |최소 90일 - 최대 3년|

## <a name="telemetry-controls"></a>원격 분석 컨트롤

제품에서 원격 분석을 켜고 끄는 방법에 대한 지침은 https://support.microsoft.com/en-us/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft의 내용을 참조하세요.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
