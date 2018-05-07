---
title: 데이터 마이그레이션 길잡이 (SQL Server)의 개요 | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, overview
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 16550b6c195f426d914f5a4b4d521cbd739765ee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="overview-of-data-migration-assistant"></a>데이터 마이그레이션 길잡이 개요

데이터 마이그레이션 길잡이 (DMA)를 사용 하면 새 버전 SQL Server 및 Azure SQL 데이터베이스에서에서 데이터베이스 기능에 영향을 줄 수 있는 호환성 문제를 감지 하 여 최신 데이터 플랫폼으로 업그레이드할 수 있습니다. DMA 성능 및 안정성 개선 대상 환경에 권장 하 고 대상 서버에 원본 서버에서 스키마, 데이터 및 포함 되지 않은 개체를 이동할 수 있습니다.

> [!NOTE] 
> 에 대 한 (측면에서 데이터베이스의 크기 및 번호가) 큰 마이그레이션 것이 좋습니다 사용 하는 [Azure 데이터베이스 마이그레이션 서비스](https://docs.microsoft.com/en-us/azure/dms/dms-overview), 규모에 데이터베이스를 마이그레이션할 수 있는 합니다.
  
## <a name="capabilities"></a>Capabilities

- Azure SQL 데이터베이스를 마이그레이션하는 온-프레미스 SQL Server 인스턴스를 평가 합니다. 평가 워크플로 사용 하면 Azure SQL 데이터베이스 마이그레이션에 영향을 줄 수 및이 문제를 해결 하는 방법에 대 한 자세한 지침을 제공 하는 다음 문제를 검색할 수 있습니다.

  - 마이그레이션 차단 문제: 호환성 문제는 블록 마이그레이션 온-프레미스 SQL Server 데이터베이스 s Azure SQL 데이터베이스를 검색 합니다. DMA 그러한 문제를 해결 하기 위한 권장 사항을 제공 합니다.

  - 지원 되지 않는 기능 또는 부분적으로 지원: 현재 사용 중인 원본 SQL Server 인스턴스에서 부분적으로 지원 되거나 지원 되지 않는 기능을 검색 합니다. DMA는 포괄적인 집합 권장 사항, Azure 및 완화 단계에서 사용할 수 있는 방법이 마이그레이션 프로젝트에 통합할 수 있도록 제공 합니다.

- 온-프레미스 SQL Server로의 업그레이드에 영향을 줄 수 있는 문제를 검색 합니다. 이러한 호환성 문제 설명 및 다음 범주로 구성 됩니다.

  - 주요 변경 내용
  - 동작 변경 내용
  - 사용 되지 않는 기능

- 업그레이드 후 데이터베이스 활용할 수 있는 대상 SQL Server 플랫폼의 새로운 기능을 검색 합니다. 이러한 기능은 권장 사항으로 설명 및 다음 범주로 구성 됩니다.

  - 성능
  - 보안
  - 저장소

- 온-프레미스 SQL Server 인스턴스를 온-프레미스 또는 온-프레미스 네트워크에서 액세스할 수 있는 Azure 가상 컴퓨터 (VM)에서 호스트 되는 최신 SQL Server 인스턴스로 마이그레이션하십시오. Azure VM의 VPN 또는 기타 기술을 사용 하 여 액세스할 수 있습니다. 마이그레이션 워크플로 사용 하면 다음과 같은 구성 요소를 마이그레이션할 수 있습니다.

  - 데이터베이스의 스키마
  - 데이터 및 사용자
  - 서버 역할
  - SQL Server 및 Windows 로그인

- 성공적인 마이그레이션 후 응용 프로그램에 연결할 수는 대상 SQL server 데이터베이스 원활 하 게 합니다.

## <a name="supported-source-and-target-versions"></a>지원 되는 소스 및 대상 버전

DMA 모든 이전 버전의 SQL Server 업그레이드 관리자를 대체 하며 대부분의 SQL Server 버전 업그레이드에 사용 해야 합니다. 지원 되는 소스 및 대상 버전에 따라합니다.

**원본**
- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012 
- SQL Server 2014
- SQL Server 2016
- Windows에서 SQL Server 2017

**대상**
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- Windows 및 Linux에서 SQL Server 2017
- Azure SQL Database

> [!NOTE] 
> DMA 현재 없으므로 Azure SQL 데이터베이스 관리 되는 인스턴스를 대상으로 합니다.

## <a name="installation"></a>설치

DMA를 설치 하려면 최신 버전의 도구를 다운로드는 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53595), 다음 실행 하 고는 **DataMigrationAssistant.msi** 파일입니다.

## <a name="see-also"></a>참고 항목

[SQL Server 마이그레이션 평가](../dma/dma-assesssqlonprem.md)

[데이터 마이그레이션 길잡이: 구성 설정](../dma/dma-configurationsettings.md)

[데이터 마이그레이션 길잡이 사용 하 여 마이그레이션 온-프레미스 SQL Server](../dma/dma-migrateonpremsql.md)

[데이터 마이그레이션 길잡이:에 대 한 유용한 정보](../dma/dma-bestpractices.md)



