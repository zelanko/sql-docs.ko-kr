---
title: "추출, 변환 및 SSIS와 Linux에서 데이터를 로드 | Microsoft Docs"
description: 
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dab69c7-73af-4340-aef0-de057356b791
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d7317cad5aa1e77653431c128ce1549bc4349e18
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>추출, 변환 및 SSIS와 Linux에서 데이터 로드

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

이 항목에서는 Linux에서 SQL Server Integration Services (SSIS) 패키지를 실행 하는 방법에 설명 합니다. SSIS 변환 및 데이터를 정리 및 여러 대상 업데이트 여러 소스 및 형식 중에서 데이터를 로드 하 여 복잡 한 데이터 통합 문제를 해결 합니다. 

Linux에서 실행 되는 SSIS 패키지는 linux 또는 Docker에서 클라우드에서 또는 Windows 온-프레미스에서 실행 중인 Microsoft SQL Server에 연결할 수 있습니다. 또한 Azure SQL 데이터베이스, Azure SQL 데이터 웨어하우스 및 ODBC 데이터 원본에 연결할 수 있습니다.

Windows 컴퓨터를 만들고 패키지를 유지 관리할 때 Linux에서 패키지를 실행 하려면 SSIS를 사용할 수 있습니다. SSIS 디자인 및 관리 도구는 Windows 응용 프로그램. 

## <a name="prerequisites"></a>필수 구성 요소

Linux 컴퓨터에서 SSIS 패키지를 실행 하려면 먼저 SQL Server Integration Services를 설치 해야 합니다. 설치 지침을 참조 하십시오. [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)합니다.

## <a name="run-an-ssis-package"></a>SSIS 패키지를 실행 합니다.

Linux 컴퓨터에서 SSIS 패키지를 실행 하려면 다음 작업을 수행 합니다.

1.  Linux 컴퓨터에 SSIS 패키지를 복사 합니다.
2.  다음 명령을 실행합니다.
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="more-about-ssis-on-linux"></a>SSIS Linux에 대 한 자세한 정보

**ODBC 연결**합니다. 이상 Linux CTP 2.1 새로 고침에서 SSIS, SSIS 패키지는 Linux 기반 ODBC 연결 사용할 수 있습니다. 이 기능은 SQL Server 및 MySQL ODBC 드라이버와 함께 테스트 되었습니다 하지만 또한 ODBC 사양을 따르는 모든 유니코드 ODBC 드라이버와 함께 사용 해야 합니다. 디자인 타임에 ODBC 데이터;에 연결 하는 DSN 또는 연결 문자열 중 하나를 제공할 수 있습니다. 또한 Windows 인증을 사용할 수 있습니다. 자세한 내용은 참조는 [블로그 게시물 Linux ODBC 지원 발표](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)합니다.

**경로**합니다. SSIS Linux에서 Linux 스타일 경로의 지원 하지 않지만 실행 시 Windows 스타일 경로의 Linux 스타일 경로에 매핑합니다. SSIS 패키지에서 Windows 스타일 경로 제공 합니다. 그런 다음, 예를 들어 매핑합니다 Windows 스타일 경로 Linux에서 SSIS `C:\test` Linux 스타일 경로에 `/test`합니다.

**패키지 배포**합니다. 이 릴리스에서 Linux에서 파일 시스템에만 패키지를 저장할 수 있습니다. SSIS 카탈로그 데이터베이스와 레거시 SSIS 서비스 패키지 배포 및 저장을 위해 Linux에서 사용할 수 없는 경우

**패키지 일정 예약**합니다. 이 릴리스에서 패키지 실행을 예약 Linux에서 SQL 에이전트를 사용할 수 없습니다.

**기타 제한 사항 및 알려진된 문제**합니다. Linux에서 SSIS 패키지를 실행할 때이 릴리스에서 다음과 같은 기능이 지원 되지 않습니다.
  - SSIS 카탈로그 데이터베이스
  - SQL 에이전트에서 예약 된 패키지 실행
  - Windows 인증
  - 타사 구성 요소
  - CDC(변경 데이터 캡처)
  - SSIS 규모 확장
  - SSIS 용 azure 기능 팩
  - Hadoop 및 HDFS 지원
  - Microsoft Connector for SAP BW

다른 제한 사항 및 Linux에서 SSIS의 알려진된 문제에 대 한 참조는 [릴리스 정보](sql-server-linux-release-notes.md#ssis)합니다.

Linux에서 SSIS에 대 한 자세한 내용은 다음 블로그 게시물을 참조 합니다.

-   [Linux에서 SSIS는 SQL Server 2017 CTP2.1에서 사용할 수 있는](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [ODBC는 SSIS (SQL Server 2017 CTP 2.1 새로 고침)를 linux에서 지원](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-about-ssis"></a>SSIS에 대 한 자세한 정보

Microsoft SQL Server Integration Services (SSIS)는 추출, 변환 및 로드 (ETL) 패키지의 데이터 웨어하우징를 포함 하 여 고성능 데이터 통합 솔루션을 구축 하기 위한 플랫폼입니다. SSIS에 대한 자세한 내용은 [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services.md)를 참조하세요.

SSIS에는 다음과 같은 기능이 포함 됩니다.
- 그래픽 도구 및 Windows에서 패키지 작성 및 디버깅에 대 한 마법사
- 다양 한 FTP 작업과 같은 워크플로 기능을 수행 하 고 SQL 문을 실행 하며 전자 메일 메시지 보내기 작업
- 다양 한 데이터 원본 및 대상 데이터 추출 및 로드에 대 한
- 다양 한 정리, 집계, 병합 및 데이터 복사를 위한 변환
- 사용자 고유의 사용자 지정 스크립트 및 구성 요소와 SSIS를 확장 하기 위한 응용 프로그래밍 인터페이스 (Api)

SSIS와 시작 하려면 최신 버전의 다운로드 [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)합니다. 다음 자습서를 따라 [ETL 패키지를 만드는 방법을 SSIS](https://msdn.microsoft.com/en-us/library/ms169917.aspx)합니다.

## <a name="see-also"></a>참고 항목
- [SQL Server Integration Services에 대 한 자세한 정보](https://msdn.microsoft.com/en-us/library/ms141026.aspx)
- [SQL Server Integration Services (SSIS) 개발 및 관리 도구](https://msdn.microsoft.com/en-us/library/ms140028.aspx)
- [SQL Server Integration Services 자습서](https://msdn.microsoft.com/en-us/library/jj720568.aspx)

