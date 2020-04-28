---
title: Data Migration Assistant (SQL Server)의 새로운 기능 | Microsoft Docs
description: SQL Server 및 Azure SQL Database에 대 한 Data Migration Assistant의 각 릴리스에 대 한 새로운 기능에 대해 알아봅니다.
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, new features
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: b5caa8b63175447daa04198768a67e7fe5e59c81
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78896801"
---
# <a name="whats-new-in-data-migration-assistant"></a>Data Migration Assistant의 새로운 기능

이 문서에서는 Data Migration Assistant의 각 릴리스에 추가 된 기능을 나열 합니다.

## <a name="data-migration-assistant-v-50"></a>Data Migration Assistant v 5.0

Data Migration Assistant의 v 5.0 릴리스는 다음에 대 한 지원을 제공 합니다.

- 평가 및 업그레이드를 위한 대상으로 Windows 용 SQL Server 2019 및 Linux 용 SQL Server 2019
- 이전 버전의 Data Migration Assistant에서 만든 평가를 저장 하 고 로드 하는 기능을 포함 하 여 평가를 저장 하 고 로드 합니다.
- SSISDB에서 호스트 되는 SSIS (SQL Server Integration Services) 프로젝트 및 패키지 저장소에서 호스트 되는 SSIS 패키지를 평가 합니다. 데이터베이스 Migration Assistant는 지원 되지 않거나 부분적으로 지원 되거나 지원 되지 않는 기능 및 원본 패키지에서 사용 되는 호환성 문제를 검색 하 고 이러한 문제를 해결 하는 데 도움이 되는 권장 사항을 제공 합니다
- 외부 응용 프로그램의 SQL 쿼리 (예: c # 소스 코드의 SQL 쿼리)를 평가 합니다. 사용자는 데이터 액세스 마이그레이션 도구 키트를 사용 하 여 c # 소스 코드에서 사용 되는 SQL 쿼리에 대 한 전체 JSON 보고서를 생성 한 다음 Data Migration Assistant에 업로드할 수 있습니다.

또한이 Data Migration Assistant 릴리스에서는 향상 된 추가 및 버그 수정이 제공 되며이 도구는 .Net 4.7.2 업데이트 되었습니다.

## <a name="data-migration-assistant-v45"></a>Data Migration Assistant v 4.5

Data Migration Assistant의 v 4.5 릴리스는 파일 시스템에서 호스트 되는 SSIS (SQL Server Integration Services) 패키지를 Azure SQL Database 또는 Azure SQL Database 관리 되는 인스턴스로 마이그레이션하기 위한 평가를 지원 합니다.

## <a name="data-migration-assistant-v44"></a>Data Migration Assistant v 4.4

Data Migration Assistant의 v 4.4 릴리스는 Azure Migrate에 대 한 평가를 업로드 하기 위한 지원을 제공 합니다.

## <a name="data-migration-assistant-v43"></a>Data Migration Assistant v 4.3

Data Migration Assistant의 v 4.3 릴리스는 다음에 대 한 지원을 제공 합니다.

- 작업 평가를 기반으로 Azure SQL Database 관리 되는 인스턴스에 대 한 SKU 권장 사항입니다.
- RDS SQL Server 평가의 원본으로 사용할 경우
- 대상으로 Azure SQL Database 관리 되는 인스턴스에 대 한 에이전트 작업 평가입니다.
- 특정 평가 규칙을 무시할 수 있습니다. DMA에서 구성 된 ' ignoreErrorCodes ' 속성에 지정 된 오류 코드 목록이 DMA 평가 결과에 표시 되지 않습니다.
- 작업 활동 단계에서 T-sql 쿼리를 평가 하 고 적절 한 권장 사항을 제공 합니다.
- 확장 이벤트 평가 (공개 미리 보기).

또한이 DMA 릴리스는 데이터베이스에서 많은 수의 스키마 개체를 처리 하는 데 향상 된 성능을 제공 하 고와 관련 된 버그 수정도 제공 합니다.

- 네이티브 컴파일을 사용 하 여 컴파일된 프로시저 (경우에 따라)
- 복잡 한 데이터베이스 스키마.

## <a name="data-migration-assistant-v42"></a>Data Migration Assistant v 4.2

Data Migration Assistant의 v 4.2 릴리스는 온-프레미스 SQL Server에서 Azure SQL Database 관리 되는 인스턴스로 마이그레이션할 때 하나 이상의 서버 인스턴스에 대 한 대상 준비 평가를 위한 명령줄 지원을 제공 합니다. 이제 고객은 Data Migration Assistant 명령줄을 사용 하 여 데이터베이스 스키마에 대 한 메타 데이터를 수집 하 고, 차단을 검색 하 고, Azure SQL Database 관리 되는 인스턴스로 마이그레이션에 영향을 주는 부분적으로 지원 되거나 지원 되지 않는 기능에 대해 알아볼 수 있습니다 그런 다음 제공 된 Power BI 템플릿을 사용 하 여 결과를 렌더링할 수 있습니다.

## <a name="data-migration-assistant-v41"></a>Data Migration Assistant v 4.1

Data Migration Assistant의 v 4.1 릴리스에는 Azure SQL Database 관리 되는 인스턴스로 마이그레이션하는 온-프레미스 SQL Server 데이터베이스의 포괄적인 평가 지원이 도입 되었습니다.

평가 워크플로를 사용 하면 Azure SQL Database 관리 되는 인스턴스로 마이그레이션하는 데 영향을 줄 수 있는 다음 문제를 검색할 수 있습니다.

- **지원 되지 않거나 부분적으로 지원 되는 기능**입니다. Data Migration Assistant는 대상 Azure SQL Database Managed Instance에서 부분적으로 지원 되거나 지원 되지 않는 사용 중인 기능에 대 한 원본 SQL Server 데이터베이스를 평가 합니다. 그런 다음이 도구는 포괄적인 권장 사항 집합, Azure에서 사용할 수 있는 대체 방법 및 완화 단계를 제공 하므로 고객이 마이그레이션 프로젝트를 계획할 때이 정보를 고려할 수 있습니다.

- **호환성 문제** 또한 Data Migration Assistant는 다음 영역과 관련 된 호환성 문제를 식별 합니다.

  - 주요 변경 내용: 대상 데이터베이스로 마이그레이션하는 기능을 손상 시킬 수 있는 특정 스키마 개체입니다.  데이터베이스 마이그레이션 후에 이러한 스키마 개체를 수정 하는 것이 좋습니다.
  - 동작 변경: 보고 된 스키마 개체는 계속 작동할 수 있지만 성능 저하와 같은 다른 동작을 나타낼 수 있습니다.
  - 정보 문제: 이러한 개체는 마이그레이션에 영향을 주지 않지만 기능 SQL Server 릴리스에서는 사용 되지 않을 수 있습니다.

평가가 완료 되 면 [Azure Database Migration Service](https://azure.microsoft.com/services/database-migration/) (DMS)를 사용 하 여 SQL Server 데이터베이스의 마이그레이션을 수행 하 Azure SQL Database Managed Instance 합니다.  DMS는 Azure SQL Database Managed Instance에 대 한 [오프 라인](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance) (일회성) 및 [온라인](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online) (최소 가동 중지 시간) 데이터베이스 마이그레이션을 모두 지원 합니다.

## <a name="data-migration-assistant-v40"></a>Data Migration Assistant v 4.0

Data Migration Assistant의 v 4.0 릴리스에는 사용자가 데이터베이스를 호스트 하는 컴퓨터에서 수집 된 성능 카운터를 기반으로 권장 되는 최소 Azure SQL Database SKU를 식별할 수 있도록 하는 Azure SQL Database SKU 권장 사항 기능이 도입 되었습니다. 이 기능은 가격 책정 계층, 계산 수준 및 최대 데이터 크기와 관련 된 권장 사항 뿐만 아니라 월별 예상 비용을 제공 합니다. 또한 Azure에 모든 데이터베이스를 대량으로 프로 비전 하는 기능을 제공 합니다.

> [!NOTE]
> 이 기능은 현재 CLI (명령줄 인터페이스)를 통해서만 사용할 수 있습니다.

추가 세부 정보는 [온-프레미스 데이터베이스에 적합 한 AZURE SQL DATABASE SKU 식별](dma-sku-recommend-sql-db.md)문서를 참조 하세요.

## <a name="data-migration-assistant-v36"></a>Data Migration Assistant v 3.6

Data Migration Assistant의 v 3.6 릴리스에는 가장 일반적인 마이그레이션 차단기의 영향을 받는 스키마 개체에 대 한 "자동 수정"이 도입 되었습니다.

이 릴리스에서는 다음과 같은 마이그레이션 차단과 동작 변경 문제에 대 한 autofix를 제공 합니다.

- 정규화 되지 않은 Join 구문을 사용 하는 스키마 개체입니다.
- 레거시 RAISEERROR 문을 사용 하는 스키마 개체입니다.
- Order By 정수 리터럴을 사용 하는 SQL 문입니다.

Data Migration Assistant는 나열 된 문제의 영향을 받는 개체에 대해 자동 스키마 변환을 수행 하 고 스키마 변환을 계속 하기 전에 사용자에 게 확인 메시지를 표시 합니다. 사용자는 제안 된 코드 변경 내용을 검토 한 다음 지정 된 데이터베이스 개체에 대 한 모든 변환을 허용 하거나 거부할 수 있습니다.

Data Migration Assistant Microsoft 프로그램 합성 (PROSE) 기술을 사용 하 여 코드 수정을 제안 합니다. [PROSE](https://microsoft.github.io/prose/)에 대해 자세히 알아보세요.

## <a name="data-migration-assistant-v35"></a>Data Migration Assistant v 3.5

Data Migration Assistant v 3.5 릴리스에는 다음과 같은 추가 내용이 포함 되어 있습니다.

- Azure SQL Database로 마이그레이션하기 위한 상당한 성능 향상 (벤치 마크 테스트는 이전 버전의 Data Migration Assistant) 보다 프로세스가 4 배 더 빠른 것을 의미 합니다.
- 메모리 사용 공간은 마이그레이션 워크플로의 안정성을 향상 시키기 위해 추가로 최적화 됩니다.
- 스키마 및 데이터 마이그레이션을 수행 하는 동안 평가를 건너뛰는 기능 (마이그레이션 전에 이미 평가를 수행 하 고 모든 주요 스키마 개체를 해결 한 경우).
- 이전 버전의 SQL Server 온-프레미스를 최신 버전으로 업그레이드 하거나 Azure Vm에서 SQL Server 하는 경우 백업 파일에 대해 잘못 된 네트워크 공유 경로가 제공 되는 경우 도구와 관련 된 문제를 해결 하는 수정 프로그램이 충돌 합니다.

## <a name="data-migration-assistant-v34"></a>Data Migration Assistant v 3.4

Data Migration Assistant의 v 3.4 릴리스에는 다음과 같은 추가 내용이 포함 되어 있습니다.

- Azure SQL Database에 대 한 마이그레이션의 소스로 SQL Server 2017를 지원 합니다.
- 안정성, 성능 및 평가 규칙 정확성 향상.

## <a name="ddata-migration-assistant-v33"></a>3.3 데이터 Migration Assistant v 3.3

Data Migration Assistant의 v 3.3 릴리스를 사용 하면 Windows 및 Linux 모두에서 온-프레미스 SQL Server 인스턴스를 SQL Server 2017의 새 버전으로 마이그레이션할 수 있습니다. Windows 및 Linux에 대 한 전체 마이그레이션 워크플로는 동일 하지만 Linux 용 SQL Server 2017로 이동 하려면 몇 가지 추가 고려 사항이 필요 합니다.

### <a name="specifying-the-back-up-path"></a>백업 경로 지정

Linux 및 Windows는 서로 다른 경로 형식을 사용 합니다. 따라서 Linux에서 SQL Server 2017로 마이그레이션하려면 사용자가 Windows 및 Linux 버전의 경로를 물리적 파일의 위치에 모두 제공 해야 합니다. 물리적 파일의 위치에 따라 두 버전의 경로를 서로 다른 방식으로 제공할 수 있습니다.
물리적 백업 파일이 다음을 실행 하는 컴퓨터에 있는 경우:

- Linux에서 ' samba ' 공유를 사용 하 여 네트워크에 있는 다른 컴퓨터와 파일을 공유 합니다.
- Windows에서 ' mnt ' 명령을 사용 하 여 Linux를 실행 하는 컴퓨터에 공유를 탑재 합니다.

> [!NOTE]
> ' Samba ' 공유 또는 ' mnt ' 명령의 사용에 대 한 자세한 내용은이 문서의 범위를 벗어나는 것입니다.

### <a name="migrating-windows-logins"></a>Windows 로그인 마이그레이션

AD (Active Directory) 로그인의 마이그레이션은 Linux의 SQL Server 2017에서 공식적으로 지원 되지만 성공적으로 작동 하려면 추가 구성이 필요 합니다. Linux에서 SQL Server 2017에 Active Directory 로그인을 설정 하는 방법에 대 한 자세한 내용은 [SQL Server on Linux 인증 Active Directory](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-authentication) 문서를 참조 하세요. 필요한 구성을 수행한 후에는 설치가 완료 되 고 평소와 같이 Active Directory 로그인을 마이그레이션할 수 있습니다. 표준 SQL 인증은 추가 설정 없이 정상적으로 작동 합니다.

## <a name="data-migration-assistant-v32"></a>Data Migration Assistant v 3.2

Data Migration Assistant v 3.2 릴리스에는 다음과 같은 추가 내용이 포함 되어 있습니다.

- 스키마 및 데이터 마이그레이션은 온-프레미스 SQL Server 데이터베이스에서 새 마이그레이션 워크플로를 사용 하 여 Azure SQL Database 하는 데 사용 됩니다.
- Azure SQL Database에 대 한 스키마 마이그레이션을 수행 하는 동안 DMA 스크립트 원본 데이터베이스 개체는 잠재적 호환성 문제를 해결 하는 방법에 대 한 지침을 제공 하 고 Azure에 스키마를 배포 합니다.

## <a name="data-migration-assistant-v31"></a>Data Migration Assistant v 3.1

Data Migration Assistant의 v 3.1 릴리스에는 다음과 같은 추가 내용이 포함 되어 있습니다.

- 데이터베이스 데이터 정렬, 지원 되지 않는 시스템 저장 프로시저 및 CLR 개체 사용에 대 한 Azure SQL Database에 대 한 평가 권장 사항을 개선 했습니다.
- Azure SQL Database로 마이그레이션할 때 호환성 수준 130, 120, 110 및 100에 대 한 평가 지침.

## <a name="data-migration-assistant-v30"></a>Data Migration Assistant v 3.0

Data Migration Assistant의 v 3.0 릴리스는 Azure SQL Database 평가를 확장 하 여와 관련 된 문제를 해결 하는 데 도움이 되는 포괄적인 권장 사항을 제공 합니다.

- 마이그레이션 차단 문제
- 부분적으로 지원 되거나 지원 되지 않는 기능 및 함수입니다.

## <a name="data-migration-assistant-v21"></a>Data Migration Assistant v 2.1

Data Migration Assistant의 v 2.1 릴리스에는 다음과 같은 추가 내용이 포함 되어 있습니다.

- 무인 모드에서 평가를 실행 하기 위한 명령줄 지원 .이를 통해 대규모 평가를 실행할 수 있습니다. 자세한 내용은 [명령줄에서 Data Migration Assistant 실행](dma-commandline.md)문서를 참조 하세요.
- 사용자가 DMA를 시작 하 고 닫을 때 성능이 향상 되었습니다.
- SQL 연결 제한 시간을 구성할 수 있습니다. 자세한 내용은 [Data Migration Assistant에 대 한 구성 설정](dma-configurationsettings.md)문서를 참조 하세요.

## <a name="data-migration-assistant-v20"></a>Data Migration Assistant v2.0

Data Migration Assistant v2.0 릴리스는 향상 된 스트레치 데이터베이스 기능 권장 사항을 포함 하 여 저장소 절감 효과를 최대화 하는 적절 한 우선 순위를 제공 합니다.

## <a name="data-migration-assistant-v10"></a>Data Migration Assistant v1.0

Data Migration Assistant의 v1.0 릴리스는 초기 릴리스 이며 다음을 제공 합니다.

- SQL Server 온-프레미스 버전으로의 업그레이드에 영향을 줄 수 있는 문제 검색. 모든 결과는 호환성 문제로 설명 되며 다음 영역으로 분류 됩니다.
  - 호환성이 손상되는 변경
  - 동작 변경
  - 사용되지 않는 기능
- 업그레이드 후 데이터베이스에서 혜택을 받을 수 있는 대상 SQL Server 플랫폼의 새로운 기능에 대 한 검색입니다. 모든 결과는 기능 권장 사항으로 설명 되며 다음 영역으로 분류 됩니다.
  - 성능
  - 보안
  - 스토리지
- 평가를 수행 하기 위한 최신 사용자 환경입니다.

## <a name="see-also"></a>참고 항목

[Data Migration Assistant 개요](../dma/dma-overview.md)
