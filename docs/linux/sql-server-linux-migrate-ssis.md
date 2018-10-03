---
title: 추출, 변환 및 SSIS 사용 하 여 Linux에 데이터 로드 | Microsoft Docs
description: 이 문서에서는 Linux 컴퓨터에 대 한 SQL Server Integration Services (SSIS)를 설명합니다.
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 07072a2c6cc724c26c6ae2f6f7950d199cd57df7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47697571"
---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>추출, 변환 및 SSIS 사용 하 여 Linux에서 데이터를 로드 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux에서 SQL Server Integration Services (SSIS) 패키지를 실행 하는 방법을 설명 합니다. 여러 원본 및 형식에서 데이터를 추출 하 여 복잡 한 데이터 통합 문제를 해결 하는 SSIS 변환 및 데이터를 정리 하 고 여러 대상에 데이터를 로드 합니다. 

Linux에서 실행 되는 SSIS 패키지는 Windows 온-프레미스 또는 클라우드, linux에서 또는 Docker에서 실행 되는 Microsoft SQL Server에 연결할 수 있습니다. 또한 Azure SQL Database, Azure SQL Data Warehouse, ODBC 데이터 원본, 플랫 파일 및 ADO.NET 원본, XML 파일 및 OData 서비스를 비롯 한 다른 데이터 원본에 연결할 수 있습니다.

SSIS의 기능에 대 한 자세한 내용은 참조 하세요. [SQL Server Integration Services](../integration-services/sql-server-integration-services.md)합니다.

## <a name="prerequisites"></a>사전 요구 사항

Linux 컴퓨터에서 SSIS 패키지 실행 하려면 먼저 SQL Server Integration Services를 설치 해야 합니다. SSIS는 Linux 컴퓨터에 대 한 SQL Server의 설치에 포함 되지 않습니다. 설치 지침은 [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)합니다.

Windows 컴퓨터를 만들고 패키지를 유지 관리할 수도 있습니다. SSIS 디자인 및 관리 도구는 Linux 컴퓨터에 대 한 현재 사용할 수 없는 Windows 응용 프로그램입니다. 

## <a name="run-an-ssis-package"></a>SSIS 패키지 실행

Linux 컴퓨터에서 SSIS 패키지를 실행 하려면 다음 작업을 수행 합니다.

1.  Linux 컴퓨터에 SSIS 패키지를 복사 합니다.
2.  다음 명령을 실행합니다.
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="run-an-encrypted-password-protected-package"></a>암호화 (암호 보호) 패키지 실행
암호로 암호화 된 SSIS 패키지를 실행 하는 방법은 세 가지가 있습니다.

1.  환경 변수의 값을 설정할 `SSIS_PACKAGE_DECRYPT`다음 예제에서와 같이:

    ```
    SSIS_PACKAGE_DECRYPT=test /opt/ssis/bin/dtexec /f package.dtsx
    ```

2.  지정 된 `/de[crypt]` 다음 예제 에서처럼 대화형으로 암호를 입력 하는 옵션:

    ```
    /opt/ssis/bin/dtexec /f package.dtsx /de
    
    Enter decryption password:
    ```

3.  지정 된 `/de` 다음 예와에서 같이 명령줄에서 암호를 제공 하는 옵션입니다. 이 메서드는 명령 기록에서 명령 사용 하 여 암호 해독 암호를 저장 하기 때문에 권장 되지 않습니다.

    ```
    opt/ssis/bin/dtexec /f package.dtsx /de test
    
    Warning: Using /De[crypt] <password> may store decryption password in command history.
    
    You can use /De[crypt] instead to enter interactive mode,
    or use environment variable SSIS_PACKAGE_DECRYPT to set decryption password.
    ```

## <a name="design-packages"></a>패키지 디자인

**ODBC 데이터 원본에 연결할**합니다. 이상 Linux CTP 2.1 새로 고침에서 SSIS를 사용 하 여 SSIS 패키지는 Linux에서 ODBC 연결을 사용할 수 있습니다. 이 기능은 SQL Server 및 MySQL ODBC 드라이버를 사용 하 여 테스트 되었습니다 있지만 ODBC 사양을 따르는 모든 유니코드 ODBC 드라이버와 함께 사용 하 합니다. 디자인 타임에 ODBC 데이터에 연결할 DSN 또는 연결 문자열을 제공할 수 있습니다. Windows 인증을 사용할 수도 있습니다. 자세한 내용은 참조는 [블로그 Linux의 ODBC 지원 발표 게시물](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)합니다.

**경로**합니다. SSIS 패키지에서 Windows 스타일 경로 제공 합니다. Linux의 SSIS Linux 스타일 경로 지원 하지 않지만 런타임에 Windows 스타일 경로 스타일 Linux 경로에 매핑합니다. Linux의 SSIS Windows 스타일 경로 매핑합니다 예를 들어, 한 다음, `C:\test` Linux 스타일 경로로 `/test`합니다.

## <a name="deploy-packages"></a>패키지 배포
이 릴리스에서 linux 파일 시스템에만 패키지를 저장할 수 있습니다. SSIS 카탈로그 데이터베이스와 레거시 SSIS 서비스 패키지 배포 및 저장을 위해 Linux에서 사용할 수 없는 경우

## <a name="schedule-packages"></a>패키지 예약
일정 도구와 같은 Linux 시스템을 사용 하면 `cron` 패키지를 예약 합니다. 이 릴리스에서 패키지 실행을 예약 하려면 Linux에서 SQL 에이전트를 사용할 수 없습니다. 자세한 내용은 참조 하세요. [cron 사용 하 여 Linux에서 일정 SSIS 패키지](sql-server-linux-schedule-ssis-packages.md)합니다.

## <a name="limitations-and-known-issues"></a>제한 사항 및 알려진 문제

제한 사항 및 Linux에서 SSIS의 알려진된 문제에 대 한 자세한 내용은 참조 하세요. [제한 사항 및 Linux에서 SSIS에 대 한 알려진된 문제](sql-server-linux-ssis-known-issues.md)합니다.

## <a name="more-info-about-ssis-on-linux"></a>Linux에서 SSIS에 대 한 자세한 정보

Linux에서 SSIS에 대 한 자세한 내용은 다음 블로그 게시물을 참조 하세요.

-   [Linux에서 SSIS는 SQL Server CTP2.1에서 사용할 수 있습니다.](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [ODBC는 SSIS (SQL Server CTP 2.1 새로 고침) linux에서 지원](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-info-about-ssis"></a>SSIS에 대 한 자세한 정보

Microsoft SQL Server Integration Services (SSIS)는 추출, 변환 및 데이터 웨어하우징용 로드 (ETL) 패키지를 포함 하 여 고성능 데이터 통합 솔루션을 빌드하기 위한 플랫폼입니다. SSIS에 대한 자세한 내용은 [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services)를 참조하세요.

SSIS에는 다음 기능이 포함 됩니다.
- 그래픽 도구 및 Windows에서 패키지 작성 및 디버깅에 대 한 마법사
- 다양 한 SQL 문 실행 및 전자 메일 메시지 보내기, FTP 작업과 같은 워크플로 함수를 수행할 작업
- 다양 한 데이터 원본 및 데이터 추출 및 로드에 대 한 대상
- 다양 한 정리, 집계, 병합 및 데이터를 복사 하는 것에 대 한 변환
- 사용자 고유의 사용자 지정 스크립트 및 구성 요소를 사용 하 여 SSIS를 확장 하기 위한 응용 프로그래밍 인터페이스 (Api)

SSIS를 사용 하 여 시작 하려면 최신 버전의 다운로드 [SQL Server Data Tools (SSDT)](../integration-services/ssis-how-to-create-an-etl-package.md)합니다.

SSIS에 대 한 자세한 내용은 다음 문서를 참조 하세요.
- [SQL Server Integration Services에 자세히 알아보기](../integration-services/sql-server-integration-services.md)
- [SQL Server Integration Services (SSIS) 개발 및 관리 도구](../integration-services/integration-services-ssis-development-and-management-tools.md)
- [SQL Server Integration Services 자습서](../integration-services/integration-services-tutorials.md)

## <a name="related-content-about-ssis-on-linux"></a>Linux에서 SSIS에 대 한 관련된 콘텐츠
-   [Linux의 SQL Server Integration Services (SSIS)를 설치 합니다.](sql-server-linux-setup-ssis.md)
-   [Conf ssis를 사용 하 여 Linux에서 SQL Server Integration Services 구성](sql-server-linux-configure-ssis.md)
-   [제한 사항 및 Linux에서 SSIS에 대 한 알려진된 문제](sql-server-linux-ssis-known-issues.md)
-   [일정 SQL Server Integration Services 패키지 cron 사용 하 여 Linux에서 실행](sql-server-linux-schedule-ssis-packages.md)
