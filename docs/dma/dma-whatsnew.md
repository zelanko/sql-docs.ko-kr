---
title: Data Migration Assistant (SQL Server)의 새로운 기능 | Microsoft Docs
ms.custom: ''
ms.date: 07/15/2019
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
ms.openlocfilehash: 4bce2ed84dbaac8d6ec95bbcf34827a8113c1f54
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262269"
---
# <a name="whats-new-in-data-migration-assistant"></a>Data Migration Assistant의 새로운 기능
이 문서는 각 릴리스에 추가의 도우미 DMA (Data Migration)를 나열합니다.

## <a name="dma-v44"></a>DMA v4.4

DMA v4.4 릴리스의 Azure Migrate 평가 업로드에 대 한 지원을 제공 합니다.

## <a name="dma-v43"></a>DMA v4.3

DMA v4.3 릴리스는에 대 한 지원을 제공합니다.

* Azure SQL Database에 대 한 SKU 권장 워크 로드 평가에 따라 인스턴스를 관리 합니다.
* SQL Server 평가 대 한 원본으로 RDS입니다.
* Azure SQL Database에 대 한 에이전트 작업 평가 인스턴스를 관리 되는 대상으로 합니다.
* 특정 평가 규칙을 무시 하는 기능 DMA에서 구성 된 'ignoreErrorCodes' 속성에 지정 된 오류 코드 목록을 DMA 평가 결과에 표시 되지 않습니다.
* 작업 작업 단계 및 적절 한 권장 사항을 제공 하는 T-SQL 쿼리 평가
* 확장된 이벤트 (공개 미리 보기)를 평가 합니다.

또한이 릴리스의 DMA에는 많은 관련 버그 수정 뿐만 아니라 데이터베이스의 스키마 개체를 처리 하기 위한 향상 된 성능을 제공:

* 경우에 따라 네이티브 컴파일을 사용 하 여 컴파일된 절차입니다.
* 복잡 한 데이터베이스 스키마입니다.

## <a name="dma-v42"></a>DMA v4.2

DMA v4.2 릴리스 관리 되는 인스턴스를 온-프레미스 SQL Server에서 Azure SQL Database로 마이그레이션 하는 경우 하나 이상의 서버 인스턴스에 대 한 대상 준비 상태 평가 대 한 명령줄 지원을 제공 합니다. 이제 고객은 DMA 명령줄을 사용 하 여 해당 데이터베이스 스키마에 대 한 메타 데이터를 수집 하려면 블 로커를 검색 하 고 Azure SQL Database 관리 되는 인스턴스로 마이그레이션에 영향을 주는 부분적으로 지원 되거나 지원 되지 않는 기능에 대해 알아봅니다 수 있습니다. 제공 된 Power BI 템플릿을 사용 하 여 결과 렌더링할 수 있습니다.

## <a name="dma-v41"></a>DMA v4.1

DMA v4.1 릴리스의 종합적인 평가의 온-프레미스 SQL Server 데이터베이스를 Azure SQL Database Managed Instance로 마이그레이션에 대 한 지원을 소개 합니다.

평가 워크플로 사용 하면 Azure SQL Database Managed Instance로 마이그레이션에 영향을 줄 수 있는 다음 문제를 감지 합니다.

* **지원 되지 않는 또는 부분적으로 지원 되는 기능**합니다. DMA 사용에서 중이거나 부분적으로 지원 되는 대상 Azure SQL Database Managed Instance에 지원 되지 않는 기능에 대 한 원본 SQL Server 데이터베이스를 평가 합니다. 이 도구는 포괄적인 마이그레이션 프로젝트를 계획 하는 경우 고객 계정에이 정보를 취할 수 있도록 단계를 완화 하 고 Azure에서의 사용 가능한 대체 방법 권장 사항 집합이 제공 합니다.

* **호환성 문제**합니다. DMA는 또한 다음과 같은 영역에 관련 된 호환성 문제를 식별 합니다.

  * 주요 변경 내용:  데이터베이스에서 대상 데이터베이스로 마이그레이션 기능을 손상 시킬 수 있는 특정 스키마 개체입니다.  데이터베이스 마이그레이션 후 이러한 스키마 개체를 수정 하는 것이 좋습니다.
  * 동작 변경 내용: 보고 스키마 개체가 계속 작동 하지만 성능 저하 예를 들어 다른 동작을 그러지 않을 것입니다.
  * 정보 제공 용 이므로 문제:  이러한 개체는 마이그레이션에 영향을 주지 않습니다 하지만 SQL Server를 해제 하는 기능에서 사용 되지 않을 수 있습니다.

사용 하 여 평가 완료 한 후 우리 [Azure Database Migration Service](https://azure.microsoft.com/services/database-migration/) Azure SQL Database Managed Instance로 SQL Server 데이터베이스의 마이그레이션을 수행 하려면 (DMS).  DMS 둘 다를 지 원하는 [오프 라인](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance) (1 회) 및 [online](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online) Azure SQL Database Managed Instance로 마이그레이션 (최소한의 가동 중지 시간) 데이터베이스입니다.

## <a name="dma-v40"></a>DMA v4.0

DMA v4.0 릴리스의 데이터베이스를 호스팅하는 컴퓨터에서 수집 된 성능 카운터에 따라 Azure SQL 데이터베이스 SKU를 권장 되는 최소를 식별할 수 있는 Azure SQL 데이터베이스 SKU 권장 사항 기능을 소개 합니다. 이 기능은 월별 예상된 비용 뿐만 아니라 계층, 계산 수준 및 최대 데이터 크기, 가격 책정에 관련 된 권장 사항을 제공 합니다. 또한 대량에서 Azure에 모든 데이터베이스를 프로 비전 하는 기능을 제공 합니다.

> [!NOTE]
> 이 기능은 현재 명령줄 인터페이스 (CLI)를 통해서만 사용할 수 있습니다.

추가 세부 정보에 대 한 문서를 참조 [온-프레미스 데이터베이스에 대 한 올바른 Azure SQL 데이터베이스 SKU 확인](dma-sku-recommend-sql-db.md)합니다.

## <a name="dma-v36"></a>DMA v3.6

DMA v3.6 릴리스의에서는 가장 일반적인 마이그레이션 블 로커의 영향을 받는 스키마 개체에 대 한 "자동 수정"을 소개 합니다.

이 릴리스에서 다음 마이그레이션 차단에 대 한 자동 복구를 제공 하 고 동작 문제를 변경 합니다.

* 정규화 되지 않은 조인 구문을 사용 하는 스키마 개체입니다.
* 레거시 RAISEERROR 문을 사용 하는 스키마 개체입니다.
* 정수 리터럴 여 순서를 사용 하는 SQL 문입니다.

DMA는 나열 된 문제로 인해 영향을 받는 개체에 대 한 자동 스키마 변환을 수행 하 고 스키마 변환 사용 하 여 계속 진행 하기 전에 확인 하 라는 합니다. 사용자 제안 되는 코드 변경 내용을 검토 하 고 중 하나 수락 하거나 거부할 수 지정 된 데이터베이스 개체에 대 한 모든 변환을 합니다.

DMA는 Microsoft 프로그램 합성 (PROSE) 기술을 사용 하 여 코드를 수정 하는 것이 좋습니다. 에 대해 자세히 알아보세요 [PROSE](https://microsoft.github.io/prose/)합니다.

## <a name="dma-v35"></a>DMA v3.5

다음 추가 포함 하는 DMA v3.5 릴리스:

* (벤치 마크 테스트 프로세스는 4 배 더 빠르게 보다 이전 버전의 DMA 사용 하 여 표시 하는 데 사용) Azure SQL Database로 마이그레이션에 대 한 상당한 성능 향상.
* 마이그레이션 워크플로의 안정성을 개선 하기 위해 메모리 사용 공간 더욱 최적화 되었습니다.
* (이미 평가 수행 하 고 마이그레이션 전에 모든 주요 스키마 개체를 처리 한) 경우 스키마 및 데이터 마이그레이션 시 평가 건너뛸 수 있습니다.
* 주소에 대 한 수정은 잘못 된 네트워크 공유 경로 제공 하는 경우 백업 파일에 대 한 레거시 버전의 SQL Server의 업그레이드를 수행 하는 경우 충돌 하는 도구를 사용 하 여 문제가 온-프레미스 또는 Azure Vm에서 SQL Server 이후 버전으로 합니다.

## <a name="dma-v34"></a>DMA v3.4

다음 추가 포함 하는 DMA v3.4의 경우 릴리스:

* Azure SQL Database로 마이그레이션 위한 원본으로 SQL Server 2017을 지원 합니다.
* 안정성, 성능 및 평가 규칙 정확성 향상.

## <a name="dma-v33"></a>DMA v3.3

DMA v3.3 릴리스의 Windows와 Linux 모두에서 SQL Server 2017의 새 버전으로 온-프레미스 SQL Server 인스턴스는 마이그레이션을 가능 하 게 합니다. Windows 및 Linux에 대 한 전체 마이그레이션 워크플로 동일 하지만 Linux for SQL Server 2017로 이동 하는 몇 가지 추가 고려 사항에 필요 합니다.

### <a name="specifying-the-back-up-path"></a>백업 경로 지정합니다.

Linux 및 Windows에는 다른 경로 형식을 사용 합니다. 결과적으로, Linux의 SQL Server 2017로 마이그레이션 사용자의 물리적 파일의 위치 경로 Windows 및 Linux 버전을 제공 해야 합니다. 실제 파일의 위치에 따라 다른 방법으로 두 버전의 경로 제공할 수 있습니다.
물리적 백업 파일을 실행 하는 컴퓨터의 경우:

* Linux에서 사용 하 여 'samba' 파일을 공유할 네트워크 상의 다른 컴퓨터와 공유 합니다.
* Windows, Linux를 실행 하는 컴퓨터에 공유를 탑재 하려면 'mnt' 명령을 사용 하 여 합니다.

> [!NOTE]
> 'Samba' 공유 나 'mnt' 명령을 사용 하 여 세부 정보는이 문서의 범위를 벗어납니다.

### <a name="migrating-windows-logins"></a>마이그레이션 Windows 로그인

Active Directory (AD) 로그인 마이그레이션 Linux의 SQL Server 2017에서 공식적으로 지원 되지만, 성공적으로 작동 하려면 추가 구성이 필요 합니다. 문서를 참조 [Linux의 SQL Server를 사용 하 여 Active Directory 인증](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-authentication) Linux의 SQL Server 2017에서 Active Directory 로그인을 설정 하는 방법에 대 한 자세한 내용은 합니다. 필요한 구성의 수행한 후 설치가 완료 되 고 일반적으로 Active Directory 로그인을 마이그레이션할 수 있습니다. 표준 SQL 인증이 추가 설정 없이 예상 대로 작동 합니다.

## <a name="dma-v32"></a>DMA v3.2

다음 추가 포함 하는 DMA v3.2 릴리스:

* 스키마 및 데이터 마이그레이션은 새 마이그레이션 워크플로 사용 하 여 Azure SQL Database로 온-프레미스 SQL Server 데이터베이스에서 활성화 됩니다.
* Azure SQL Database로 스키마 마이그레이션 중 DMA 원본 데이터베이스 개체 스크립팅 모든 잠재적인 호환성 문제를 해결 하는 방법에 대 한 지침을 제공 하며 다음 스키마를 Azure에 배포 합니다.

## <a name="dma-v31"></a>DMA v3.1

다음 추가 포함 하는 DMA v3.1 릴리스:

* 데이터베이스 데이터 정렬 기준으로 Azure SQL Database에 대 한 향상 된 평가 권장 사항을 지원 되지 않는 시스템 저장 프로시저 및 CLR 개체를 사용 합니다.
* 호환성 수준 130, 120, 110 및 Azure SQL Database로 마이그레이션할 때 100에 대 한 지침을 평가 합니다.

## <a name="dma-v30"></a>DMA v3.0

DMA v3.0 릴리스의 관련 된 문제를 해결 하는 데 도움이 되는 포괄적인 권장 사항을 제공 하는 Azure SQL 데이터베이스 평가 확장 합니다.

* 마이그레이션 차단 문제입니다.
* 부분적으로 지원 되지 않는 기능 및 함수 또는 합니다.

## <a name="dma-v21"></a>DMA v2.1

다음 추가 포함 하는 DMA v2.1 릴리스:

* 평가 대규모로 평가 실행 하는 데 도움이 되는 무인 모드로 실행 하기 위한 명령줄 지원 합니다. 추가 세부 정보에 대 한 문서를 참조 [실행 Data Migration Assistant 명령줄에서](dma-commandline.md)합니다.
* 사용자가 시작 하 고 DMA를 닫을 때 성능 향상입니다.
* SQL 연결 제한 시간을 구성할 수 있습니다. 추가 세부 정보에 대 한 문서를 참조 [Data Migration Assistant에 대 한 구성 설정을](dma-configurationsettings.md)합니다.

## <a name="dma-v20"></a>DMA v2.0

DMA v2.0 릴리스의 향상 된 스트레치 데이터베이스 기능 권장 사항이 절약 된 저장소를 최대화 하는 적절 한 우선 순위가 지정 된 테이블을 포함 합니다.

## <a name="dma-v10"></a>DMA v1.0

DMA v1.0 릴리스를 출시 한 이며 제공:

* 문제는 온-프레미스 버전의 SQL Server로의 업그레이드에 영향을 줄 수를 검색 합니다. 모든 결과 호환성 문제로를 다음과 같은 영역으로 분류 하 고 있습니다.
  * 주요 변경 내용
  * 동작 변경 내용
  * 사용되지 않는 기능
* 데이터베이스는 업그레이드 후에 활용할 수 있는 대상 SQL Server 플랫폼의 새로운 기능을 검색 합니다. 모든 결과 기능 권장 사항으로 설명 하 고 다음과 같은 영역으로 범주별로 분류 하:
  * 성능
  * 보안
  * 스토리지
* 최신 사용자 환경을 평가 수행 합니다.

## <a name="see-also"></a>참고자료

[Data Migration Assistant 개요](../dma/dma-overview.md)
