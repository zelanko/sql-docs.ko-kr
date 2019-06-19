---
title: Azure에 배포된 SSIS 패키지 유효성 검사 | Microsoft Docs
description: SSIS 패키지 배포 마법사가 예상대로 패키지가 Azure에서 실행되는 것을 방해할 수 있는 알려진 문제의 패키지를 확인하는 방법에 대해 알아봅니다.
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
manager: craigg
ms.openlocfilehash: a323ebdaa6e9fd8b1ce09acc3f8354d536df9701
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014956"
---
# <a name="validate-sql-server-integration-services-ssis-packages-deployed-to-azure"></a>Azure에 배포된 SSIS(SQL Server Integration Services) 패키지 유효성 검사

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Azure 서버의 SSIS 카탈로그(SSISDB)에 SQL Server Integration Services(SSIS) 프로젝트를 배포하면 패키지 배포 마법사는 **검토** 페이지 이후에 추가 유효성 검사 단계를 추가합니다. 이 유효성 검사 단계에서는 Azure SSIS Integration Runtime에서 패키지가 예상대로 실행되지 않을 수 있는 알려진 문제점을 프로젝트의 패키지에서 확인합니다. 그런 다음 마법사는 **유효성 검사** 페이지에서 적용 가능한 경고를 표시합니다.

> [!IMPORTANT]
> 이 문서에서 설명하는 유효성 검사는 SQL Server 데이터 도구(SSDT) 버전 17.4 이상을 사용하여 프로젝트를 배포할 때 발생합니다. SSDT의 최신 버전을 얻으려면 [SQL Server Data Tools(SSDT) 다운로드](../../ssdt/download-sql-server-data-tools-ssdt.md)를 참조하세요.

패키지 배포 마법사에 대한 자세한 내용은 [통합 서비스(SSIS) 프로젝트 및 패키지 배포](../packages/deploy-integration-services-ssis-projects-and-packages.md)를 참조하세요.

## <a name="validate-connection-managers"></a>연결 관리자 유효성 검사

마법사는 특정 연결 관리자가 다음 문제를 검사하여 연결이 실패할 수 있음을 나타냅니다.
- **Windows 인증**. 연결 문자열에 Windows 인증이 사용되면 유효성 검사에서 경고를 표시합니다. Windows 인증을 위해서는 추가 구성 단계가 필요합니다. 자세한 정보는 [Windows 인증으로 데이터 및 파일 공유에 연결](ssis-azure-connect-with-windows-auth.md)을 참조합니다.
- **파일 경로**. 연결 문자열에 `C:\\...`과 같이 하드 코딩된 로컬 파일 경로가 있으면 유효성 검사에서 경고를 표시합니다. 절대 경로를 포함하는 패키지가 실패할 수 있습니다.
- **UNC 경로**. 연결 문자열에 UNC 경로가 포함되어 있으면 연결 문자열에 UNC 경로가 포함되어 있으면 유효성 검사에서 경고를 표시합니다. 일반적으로 UNC 경로에 액세스하려면 Windows 인증이 필요하기 때문에 UNC 경로가 포함된 패키지가 실패할 수 있습니다.
- **호스트 이름**. 서버 속성에 IP 주소 대신 호스트 이름이 포함되어 있으면 유효성 검사에서 경고를 표시합니다. 호스트 이름을 포함하는 패키지는 일반적으로 Azure 가상 네트워크가 DNS 이름 확인을 지원하기 위해 올바른 DNS 구성이 필요하기 때문에 실패할 수 있습니다.
- **공급자 또는 드라이버**. 공급자 또는 드라이버가 지원되지 않으면 유효성 검사에서 경고를 표시합니다. 현재는 소수의 내장 공급자 및 드라이버만 지원됩니다.

마법사는 목록의 연결 관리자에 대해 다음과 같은 유효성 검사를 수행합니다.

| 연결 관리자 | Windows 인증 | 파일 경로 | UNC 경로 | 호스트 이름 | 공급자 또는 드라이버 |
|--------------------|----------|-----------|-----|-----------|-------------------|
| Ado                | âœ“        |           |     | âœ“         | âœ“                 |
| AdoNet             | âœ“        |           |     | âœ“         | âœ“                 |
| Cache              |          | âœ“         | âœ“   |           |                   |
| 내보내기              |          | âœ“         | âœ“   |           |                   |
| 파일               |          | âœ“         | âœ“   |           |                   |
| FlatFile           |          | âœ“         | âœ“   |           |                   |
| Ftp                |          |           |     | âœ“         |                   |
| MsOLAP100          |          |           |     | âœ“         | âœ“                 |
| MultiFile          |          | âœ“         | âœ“   |           |                   |
| MultiFlatFile      |          | âœ“         | âœ“   |           |                   |
| OData              | âœ“        |           |     | âœ“         |                   |
| Odbc               | âœ“        |           |     | âœ“         | âœ“                 |
| OleDb              | âœ“        |           |     | âœ“         | âœ“                 |
| SmoServer          | âœ“        |           |     | âœ“         |                   |
| Smtp               | âœ“        |           |     | âœ“         |                   |
| SqlMobile          |          | âœ“         | âœ“   |           |                   |
| Wmi                | âœ“        |           |     |           |                   |
|||||||

## <a name="validate-sources-and-destinations"></a>원본 및 대상 유효성 검사
다음 타사 원본 및 대상은 지원되지 않습니다.

-   Attunity에 의한 Oracle 원본 및 대상
-   Attunity에 의한 Teradata 원본 및 대상
-   SAP BI 원본 및 대상

## <a name="validate-tasks-and-components"></a>작업 및 구성 요소 유효성 검사

### <a name="execute-process-task"></a>프로세스 실행 태스크

명령이 절대 경로가 있는 로컬 파일 또는 UNC 경로가 있는 파일을 가리키는 경우 유효성 검사에서 경고를 표시합니다. 이러한 경로로 인해 Azure에서 실행이 실패할 수 있습니다.

### <a name="script-task-and-script-component"></a>스크립트 태스크 및 스크립트 구성 요소

패키지에 스크립트 태스크 또는 지원되지 않는 어셈블리를 참조하거나 호출할 수 있는 스크립트 구성 요소가 패키지에 포함되어 있으면 유효성 검사에서 경고를 표시합니다. 이러한 참조 또는 호출로 인해 실행이 실패할 수 있습니다.

### <a name="other-components"></a>기타 구성 요소

Orc 형식은 HDFS 대상 및 Azure Data Lake Store 대상에서 지원되지 않습니다.

## <a name="next-steps"></a>다음 단계
Azure에서 패키지 실행을 예약하는 방법에 대해 알아보려면 [Azure에서 SSIS 패키지 예약](ssis-azure-schedule-packages.md)을 참조하세요.
