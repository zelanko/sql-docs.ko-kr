---
title: SQL Server 2019 릴리스 정보 | Microsoft Docs
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: c8a69dc4aa074c7e2d8575f7d8543ee75f577e1e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532916"
---
# <a name="includesql-server-2019includessssqlv15-mdmd-release-notes"></a>[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 릴리스 정보
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]의 관련 제한 사항 및 알려진 문제에 대해 설명합니다. 관련 내용은 다음을 참조하세요.

> [[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)

## [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]는 [!INCLUDE[SQL Server 2019](../includes/ssnoversion-md.md)]의 최신 공개 릴리스입니다.

라이선싱에 대한 전체 세부 정보는 설치 미디어의 `License Terms` 폴더에 있습니다.

## <a name="documentation"></a>설명서

- **문제 및 고객에게 미치는 영향**: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설명서는 버전별로 필터링할 수 있습니다. 각 설명서 페이지의 왼쪽 맨 위에 있는 컨트롤을 사용하여 요구 사항에 맞게 필터링합니다.

## <a name="build-number"></a>빌드 번호

SQL Server 2019의 RTM 빌드 번호는 `15.0.2000.5`입니다.

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="sql-server-installation-may-fail-if-ssms-18x-is-installed"></a>SSMS 18.x가 설치된 경우 SQL Server 설치가 실패할 수 있음

- **문제 및 고객에게 미치는 영향**: 다음과 같은 조건에서는 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 설치가 실패합니다.
  1. SSMS(SQL Server Management Studio) 버전 18.0, 18.1, 18.2 또는 18.3이 서버에 설치되어 있습니다.
  1. 이동식 미디어에서 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 설치를 시도합니다. 예를 들어 설치 미디어가 DVD입니다.

- **해결 방법**:
  1. SSMS 18.3.1보다 이전 버전의 SSMS를 제거합니다.
  1. 최신 버전의 SSMS(18.3.1 이상)를 설치합니다. 최신 버전은 [SSMS 다운로드](../ssms/download-sql-server-management-studio-ssms.md)를 참조하세요.
  1. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]를 정상적으로 설치합니다.

  > [!NOTE]
  > 제거가 필요합니다.

- **적용 대상**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]

## <a name="utf-8-collations"></a>UTF-8 데이터 정렬

- **문제 및 고객에게 미치는 영향**: UTF-8 사용 데이터 정렬은 다음 기능과 함께 사용할 수 없습니다.
  - [메모리 내 OLTP 테이블](../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md)
  - [보안 Enclaves를 사용한 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)(보안 Enclaves를 사용하지 않는 경우 [Always Encrypted](../relational-databases/security/encryption/always-encrypted-database-engine.md)는 UTF-8을 사용할 수 있음)

  > [!WARNING]
  > 4000바이트를 초과하여 사용하는 [CHAR 또는 VARCHAR](../t-sql/data-types/char-and-varchar-transact-sql.md)로 정의된 테이블 열을 포함하는 데이터베이스의 [bacpac](../relational-databases/data-tier-applications/data-tier-applications.md#bacpac)를 만드는 것은 실패합니다.
  
  > [!NOTE]
  > 현재 Azure Data Studio 또는 SSDT(SQL Server Data Tools)에서 UTF-8 사용 데이터 정렬을 선택하도록 UI를 지원하지 않습니다. 최신 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)](SSMS) 버전 18은 UI의 다양한 UTF-8 사용 데이터 정렬 선택을 지원합니다.

- **적용 대상**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RTM

## <a name="master-data-service-notification-email-contains-broken-link"></a>Master Data Service 알림 메일에 끊어진 링크가 포함됨

- **문제 및 고객에게 미치는 영향**: MDS(Master Data Services)의 알림 메일에 끊어진 링크가 있습니다. 링크를 클릭하면 다음 메시지와 같은 오류를 반환하는 페이지로 이동됩니다.

   `The view 'Index' or its master was not found or no view engine supports the searched locations.`

- **해결 방법**: MDS 포털을 열고 리소스로 직접 이동합니다.

- **적용 대상**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RTM

## <a name="see-also"></a>관련 항목:

- [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-ver15.md)

## <a name="machine-learning-services"></a>Machine Learning Services

SQL Server Machine Learning Services의 문제는 [SQL Server Machine Learning Services의 알려진 문제](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)를 참조하세요.

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]
