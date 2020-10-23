---
title: SSIS를 사용하여 Linux에서 데이터 추출, 변환 및 로드
description: Linux에서 SSIS(SQL Server Integration Services) 패키지를 실행하는 방법을 알아봅니다. 또한 SSIS 기능에 대한 자세한 정보를 어디에서 찾을 수 있는지 알아봅니다.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: e513f6783e827617a8c0cc4a1fa0ea4644dcb6e7
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115846"
---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>SSIS를 사용하여 Linux에서 데이터 추출, 변환 및 로드

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 Linux에서 SSIS(SQL Server Integration Services) 패키지를 실행하는 방법을 설명합니다. SSIS는 여러 원본 및 형식에서 데이터를 추출하여 변환 및 정리한 다음, 여러 대상으로 데이터를 로드하여 복잡한 데이터 통합 문제를 해결합니다. 

Linux에서 실행되는 SSIS 패키지는 Windows 온-프레미스 또는 클라우드, Linux 또는 Docker에서 실행되는 Microsoft SQL Server에 연결할 수 있습니다. Azure SQL Database, Azure Synapse Analytics, ODBC 데이터 원본, 플랫 파일 및 ADO.NET 원본, XML 파일, OData 서비스를 비롯한 기타 데이터 원본에 연결할 수도 있습니다.

SSIS의 기능에 대한 자세한 내용은 [SQL Server Integration Services](../integration-services/sql-server-integration-services.md)를 참조하세요.

## <a name="prerequisites"></a>전제 조건

Linux 컴퓨터에서 SSIS 패키지를 실행하려면 먼저 SQL Server Integration Services를 설치해야 합니다. SSIS는 Linux 컴퓨터용 SQL Server 설치에 포함되어 있지 않습니다. 설치 지침은 [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)를 참조하세요.

패키지를 만들고 유지 관리하려면 Windows 컴퓨터도 있어야 합니다. SSIS 디자인 및 관리 도구는 현재 Linux 컴퓨터에서 사용할 수 없는 Windows 애플리케이션입니다. 

## <a name="run-an-ssis-package"></a>SSIS 패키지 실행

Linux 컴퓨터에서 SSIS 패키지를 실행하려면 다음 작업을 수행합니다.

1.  Linux 컴퓨터에 SSIS 패키지를 복사합니다.
2.  다음 명령을 실행합니다.
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="run-an-encrypted-password-protected-package"></a>암호화된(암호로 보호된) 패키지 실행
암호를 사용하여 암호화된 SSIS 패키지를 실행하는 방법에는 다음 세 가지가 있습니다.

1.  다음 예제와 같이 `SSIS_PACKAGE_DECRYPT` 환경 변수의 값을 설정합니다.

    ```
    SSIS_PACKAGE_DECRYPT=test /opt/ssis/bin/dtexec /f package.dtsx
    ```

2.  다음 예제와 같이 `/de[crypt]` 옵션을 지정하여 암호를 대화형으로 입력합니다.

    ```
    /opt/ssis/bin/dtexec /f package.dtsx /de
    
    Enter decryption password:
    ```

3.  다음 예제와 같이 `/de` 옵션을 지정하여 명령줄에서 암호를 지정합니다. 이 방법은 명령과 함께 암호 해독 암호를 명령 기록에 저장하기 때문에 사용하지 않는 것이 좋습니다.

    ```
    opt/ssis/bin/dtexec /f package.dtsx /de test
    
    Warning: Using /De[crypt] <password> may store decryption password in command history.
    
    You can use /De[crypt] instead to enter interactive mode,
    or use environment variable SSIS_PACKAGE_DECRYPT to set decryption password.
    ```

## <a name="design-packages"></a>패키지 디자인

**ODBC 데이터 원본에 연결**. Linux CTP 2.1 새로 고침 이상에서 SSIS를 사용하는 경우 SSIS 패키지는 Linux에서 ODBC 연결을 사용할 수 있습니다. 이 기능은 SQL Server 및 MySQL ODBC 드라이버로 테스트되었지만 ODBC 사양을 준수하는 모든 유니코드 ODBC 드라이버에서도 작동할 것으로 예상됩니다. 디자인 타임에 ODBC 데이터에 연결하기 위한 DSN 또는 연결 문자열을 제공할 수 있습니다. Windows 인증을 사용할 수도 있습니다. 자세한 내용은 [Linux의 ODBC 지원을 알리는 블로그 게시물](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)을 참조하세요.

**경로**. SSIS 패키지에 Windows 스타일 경로를 제공합니다. Linux SSIS는 Linux 스타일 경로를 지원하지 않고 런타임에 Windows 스타일 경로를 Linux 스타일 경로에 매핑합니다. 예를 들어 Linux SSIS는 Windows 스타일 경로 `C:\test`를 Linux 스타일 경로 `/test`에 매핑합니다.

## <a name="deploy-packages"></a>패키지 배포
이 릴리스에서는 Linux 파일 시스템에만 패키지를 저장할 수 있습니다. SSIS 카탈로그 데이터베이스 및 레거시 SSIS 서비스는 Linux에서 패키지 배포 및 스토리지에 사용할 수 없습니다.

## <a name="schedule-packages"></a>패키지 예약
`cron`과 같은 Linux 시스템 일정 도구를 사용하여 패키지를 예약할 수 있습니다. 이 릴리스에서는 Linux SQL 에이전트를 사용하여 패키지 실행을 예약할 수 없습니다. 자세한 내용은 [cron을 사용하여 Linux에서 SSIS 패키지 예약](sql-server-linux-schedule-ssis-packages.md)을 참조하세요.

## <a name="limitations-and-known-issues"></a>제한 사항 및 알려진 문제

Linux SSIS의 제한 사항 및 알려진 문제에 대한 자세한 내용은 [Linux SSIS의 제한 사항 및 알려진 문제](sql-server-linux-ssis-known-issues.md)를 참조하세요.

## <a name="more-info-about-ssis-on-linux"></a>Linux SSIS에 대한 자세한 정보

Linux SSIS에 대한 자세한 내용은 다음 블로그 게시물을 참조하세요.

-   [SSIS on Linux is available in SQL Server CTP2.1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)(SQL Server CTP 2.1에서 Linux SSIS를 사용할 수 있음)
-   [ODBC is supported in SSIS on Linux (SQL Server CTP 2.1 refresh)](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)(Linux SSIS에서 ODBC가 지원됨(SQL Server CTP 2.1 새로 고침))

## <a name="more-info-about-ssis"></a>SSIS에 대한 자세한 정보

Microsoft SSIS(SQL Server Integration Services)는 데이터 웨어하우징용 ETL(추출, 변환 및 로드) 패키지를 포함하여 고성능 데이터 통합 솔루션을 빌드하기 위한 플랫폼입니다. SSIS에 대한 자세한 내용은 [SQL Server Integration Services](../integration-services/sql-server-integration-services.md)를 참조하세요.

SSIS에는 다음과 같은 기능이 포함되어 있습니다.
- Windows에서 패키지를 빌드하고 디버깅하기 위한 그래픽 도구 및 마법사
- FTP 작업과 같은 워크플로 기능 수행, SQL 문 실행, 메일 메시지 전송을 위한 다양한 태스크
- 데이터를 추출하고 로드하기 위한 다양한 데이터 원본 및 대상
- 데이터를 정리, 집계, 병합 및 복사하기 위한 다양한 변환
- 사용자 지정 스크립트 및 구성 요소를 사용하여 SSIS를 확장하기 위한 API(애플리케이션 프로그래밍 인터페이스)

SSIS를 시작하려면 최신 버전의 [SSDT(SQL Server Data Tools)](../integration-services/ssis-how-to-create-an-etl-package.md)를 다운로드합니다.

SSIS에 대한 자세한 내용은 다음 문서를 참조하세요.
- [SQL Server Integration Services에 대한 자세한 정보](../integration-services/sql-server-integration-services.md)
- [SSIS(SQL Server Integration Services) 개발 및 관리 도구](../integration-services/integration-services-ssis-development-and-management-tools.md)
- [SQL Server Integration Services 자습서](../integration-services/integration-services-tutorials.md)

## <a name="related-content-about-ssis-on-linux"></a>Linux SSIS에 대한 관련 콘텐츠
-   [Linux에서 SSIS(SQL Server Integration Services) 설치](sql-server-linux-setup-ssis.md)
-   [ssis-conf를 사용하여 Linux에서 SQL Server Integration Services 구성](sql-server-linux-configure-ssis.md)
-   [Linux SSIS의 제한 사항 및 알려진 문제](sql-server-linux-ssis-known-issues.md)
-   [cron을 사용하여 Linux에서 SQL Server Integration Services 패키지 실행 예약](sql-server-linux-schedule-ssis-packages.md)