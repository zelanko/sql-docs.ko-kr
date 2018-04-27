---
title: 데이터 마이그레이션 길잡이 (SQL Server)의 새로운 기능 | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2018
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, new features
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0004406d86da4174898141d1f75c72186921b8d3
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="whats-new-in-data-migration-assistant"></a>데이터 마이그레이션 길잡이의 새로운 기능

이 항목에서는 각 릴리스에 추가 데이터 마이그레이션 길잡이 (DMA)의 오류가 나열 됩니다.

## <a name="dma-v34"></a>DMA v3.4
DMA v3.4 출시에 다음과 같은 추가 기능에 포함 됩니다.
- Azure SQL 데이터베이스의 마이그레이션 위한 원본으로 SQL Server 2017 지원 합니다.
- 안정성, 성능 및 평가 규칙 정확성 향상.

## <a name="dma-v33"></a>DMA v3.3
DMA의 v3.3 릴리스를 통해 온-프레미스 SQL Server 인스턴스를 사용 하 여 새 버전의 Windows와 Linux 모두에서 SQL Server 2017를 마이그레이션이 가능 합니다. Windows 및 Linux에 대 한 전체 마이그레이션 워크플로 동일 이지만, Linux에 대 한 SQL Server 2017로 이동 하는 몇 가지 추가 고려 사항 필요 합니다.

### <a name="specifying-the-back-up-path"></a>백업 경로 지정합니다.
Linux 및 Windows에는 다른 경로 형식을 사용합니다. 결과적으로, SQL Server 2017 linux로 마이그레이션에서는 사용자 Windows와 Linux 버전의 물리적 파일의 위치 경로를 제공 해야 합니다. 이 물리적 파일의 위치에 따라 다른 방법으로 수행 됩니다.
물리적 백업 파일이 실행 하는 컴퓨터에 있으면:
- Linux를 사용 하 여 'samba' 파일을 공유할 네트워크 상의 다른 컴퓨터와 공유 합니다.
-   Windows에서는 'mnt' 명령의 사용 하 여 Linux를 실행 하는 컴퓨터에 공유를 탑재 합니다.

> [!NOTE]
> 'Samba' 공유 또는 'mnt' 명령을 사용 하 여 세부 정보는이 문서의 범위입니다.

### <a name="migrating-windows-logins"></a>마이그레이션 Windows 로그인
Active Directory (AD) 로그인 마이그레이션의 SQL Server 2017 linux에서 공식적으로 지원 되지만, 제대로 작동 하려면 추가 구성이 필요 합니다. 항목을 참조 [Linux에서 SQL Server와 Active Directory 인증](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-active-directory-authentication) SQL Server 2017 linux에서 Active Directory 로그인을 설정 하는 방법에 대 한 자세한 정보에 대 한 합니다. 그 후 설치가 완료 되 면 평소와 같이 Active Directory 로그인을 마이그레이션할 수 있습니다. 표준 SQL 인증에는 모든 추가 설치 없이 예상 대로 작동 합니다.

## <a name="dma-v32"></a>DMA v3.2
DMA의 경우 v3.2 릴리스는 다음과 같은 추가 기능에 포함 됩니다.

- 스키마 및 데이터 마이그레이션 새 마이그레이션 워크플로를 온-프레미스 SQL Server 데이터베이스에서 Azure SQL 데이터베이스에 활성화 됩니다.

- Azure SQL 데이터베이스에 스키마 마이그레이션 중 DMA 원본 데이터베이스 개체 스크립팅, 잠재적인 호환성 문제를 해결 하는 방법에 지침을 제공 및 다음 스키마를 Azure에 배포 합니다.

## <a name="dma-v31"></a>DMA v3.1
V 3.1 릴리스의 DMA 다음과 같은 추가 기능에 포함 됩니다.

- 지원 되지 않는 시스템 저장 프로시저 및 CLR 개체를 활용 하는 데이터베이스 데이터 정렬 기준으로 Azure SQL 데이터베이스에 대 한 개선 된 평가 권장 합니다.

- 호환성 수준 130, 120, 110 및 Azure SQL 데이터베이스를 마이그레이션하는 경우 100에 대 한 지침을 평가 합니다.

## <a name="dma-v30"></a>DMA v3.0
DMA v3.0 릴리스의 Azure SQL 데이터베이스 평가 관련 된 문제 해결에 도움이 되도록 포괄적인 권장 사항을 제공할 것을 확장 합니다.

- 마이그레이션 차단 문제입니다.

- 부분적으로 또는 특징과 기능을 지원 되지 않습니다.

## <a name="dma-v21"></a>DMA v2.1
DMA (v2.1) 릴리스의 다음과 같은 추가 기능에 포함 됩니다.
- 최대 규모로 평가 실행 하는 데 도움이 무인된 모드에서 평가 실행 하기 위한 명령줄 지원 합니다. 추가 세부 정보에 대 한 항목을 참조 [실행 데이터 마이그레이션 길잡이 명령줄에서](dma-commandline.md)합니다.

- 사용자가 시작 하 고 DMA를 닫으면 성능 향상입니다.

- SQL 연결 제한 시간을 구성할 수 있습니다. 추가 세부 정보에 대 한 항목을 참조 [데이터 마이그레이션 길잡이 대 한 구성 설정을](dma-configurationsettings.md)합니다.

## <a name="dma-v20"></a>DMA v2.0
DMA v2.0 릴리스의 향상 된 스트레치 데이터베이스 기능 권장 사항이 저장 공간 절약 효과 최대화 하는 적절 한 우선 순위가 지정 된 테이블에 포함 됩니다.

## <a name="dma-v10"></a>DMA v1.0
DMA의 v1.0 릴리스는 초기 릴리스 및에 대 한 제공:
- SQL Server의 온-프레미스 버전으로 업그레이드에 영향을 줄 수 있는 문제의 검색입니다. 모든 결과 호환성 문제로를 다음과 같은 영역으로 분류 됩니다.
    -   주요 변경 내용
    - 동작 변경 내용
    - 사용 되지 않는 기능

- 데이터베이스 업그레이드를 활용할 수 있는 대상 SQL Server 플랫폼의 새로운 기능의 검색입니다. 모든 결과 기능 권장 사항을로 다음과 같은 영역으로 분류 됩니다.
    - 성능
    - 보안
    - 저장소

-   평가 수행 하려면 최신 사용자 경험 합니다.

## <a name="see-also"></a>참고 항목

[데이터 마이그레이션 길잡이 개요](../dma/dma-overview.md)
