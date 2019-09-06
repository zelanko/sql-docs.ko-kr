---
title: Data Migration Assistant 개요 (SQL Server) | Microsoft Docs
description: Data Migration Assistant를 사용 하 여 SQL Server 데이터베이스를 다른 SQL Server 또는 Azure 데이터베이스로 마이그레이션하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 08/23/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, overview
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: ac039906bddc700e9e0b2517d0e34274e088ad2e
ms.sourcegitcommit: 0c6c1555543daff23da9c395865dafd5bb996948
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70304704"
---
# <a name="overview-of-data-migration-assistant"></a>Data Migration Assistant 개요
DMA (Data Migration Assistant)는 새 버전의 SQL Server 또는 Azure SQL Database에서 데이터베이스 기능에 영향을 줄 수 있는 호환성 문제를 검색 하 여 최신 데이터 플랫폼으로 업그레이드 하는 데 도움이 됩니다. DMA는 대상 환경에 대 한 성능 및 안정성 향상을 권장 하며 원본 서버에서 대상 서버로 스키마, 데이터 및 포함 되지 않은 개체를 이동할 수 있도록 합니다.

> [!NOTE] 
> 데이터베이스의 수와 크기를 기준으로 대규모 마이그레이션의 경우 대규모로 데이터베이스를 마이그레이션할 수 있는 [Azure Database Migration Service](/azure/dms/dms-overview)를 사용 하는 것이 좋습니다.
  
## <a name="get-data-migration-assistant"></a>Data Migration Assistant 가져오기
DMA를 설치 하려면 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53595)에서 최신 버전의 도구를 다운로드 한 후 **DataMigrationAssistant** 파일을 실행 합니다.

## <a name="capabilities"></a>Capabilities
- Azure SQL database로 마이그레이션하는 온-프레미스 SQL Server 인스턴스를 평가 합니다. 평가 워크플로를 사용 하면 Azure SQL database 마이그레이션에 영향을 줄 수 있는 다음 문제를 검색 하 고 해결 하는 방법에 대 한 자세한 지침을 제공할 수 있습니다.

  - 마이그레이션 차단 문제: 온-프레미스 SQL Server 데이터베이스를 Azure SQL Database으로 마이그레이션하는 것을 차단 하는 호환성 문제를 검색 합니다. DMA는 이러한 문제를 해결 하는 데 도움이 되는 권장 사항을 제공 합니다.

  - 부분적으로 지원 되거나 지원 되지 않는 기능: 원본 SQL Server 인스턴스에서 현재 사용 중인 부분적으로 지원 되거나 지원 되지 않는 기능을 검색 합니다. DMA는 포괄적인 권장 사항 집합, Azure에서 사용할 수 있는 대체 방법 및 마이그레이션 프로젝트에 통합할 수 있도록 완화 단계를 제공 합니다.

- 온-프레미스 SQL Server로 업그레이드에 영향을 줄 수 있는 문제를 검색 합니다. 이러한 항목은 호환성 문제로 설명 되며 다음 범주로 구성 됩니다.

  - 주요 변경 내용
  - 동작 변경
  - 사용되지 않는 기능

- 업그레이드 후 데이터베이스에서 혜택을 받을 수 있는 대상 SQL Server 플랫폼의 새로운 기능을 검색 합니다. 이러한 기능은 기능 권장 사항으로 설명 되며 다음 범주로 구성 됩니다.

  - 성능
  - 보안
  - 스토리지

- 온-프레미스 SQL Server 인스턴스를 온-프레미스 또는 온-프레미스 네트워크에서 액세스할 수 있는 Azure VM (가상 머신)에 호스팅된 최신 SQL Server 인스턴스로 마이그레이션합니다. VPN 또는 기타 기술을 사용 하 여 Azure VM에 액세스할 수 있습니다. 마이그레이션 워크플로는 다음 구성 요소를 마이그레이션하는 데 도움이 됩니다.

  - 데이터베이스 스키마
  - 데이터 및 사용자
  - 서버 역할
  - SQL Server 및 Windows 로그인

- 성공적으로 마이그레이션한 후 응용 프로그램은 대상 SQL Server 데이터베이스에 원활 하 게 연결할 수 있습니다.

- Azure SQL Database 또는 Azure SQL Database 관리 되는 인스턴스로 마이그레이션하는 온-프레미스 SQL Server Integration Services (SSIS) 패키지를 평가 합니다. 평가는 마이그레이션에 영향을 줄 수 있는 문제를 검색 하는 데 도움이 됩니다. 이러한 항목은 호환성 문제로 설명 되며 다음 범주로 구성 됩니다.

  - 마이그레이션 블 로커: 원본 패키지를 Azure로 마이그레이션하는 것을 차단 하는 호환성 문제를 검색 합니다. DMA는 이러한 문제를 해결 하는 데 도움이 되는 권장 사항을 제공 합니다.

  - 정보 문제: 원본 패키지에서 사용 되는 부분적으로 지원 되거나 더 이상 사용 되지 않는 기능을 검색 합니다.

  > [!NOTE]
  > 파일 시스템에서 호스트 되는 패키지의 평가는 지원 됩니다.
  > MSDB, 패키지 저장소 또는 SSISDB에서 호스트 되는 패키지의 평가는 나중에 제공 됩니다.

## <a name="prerequisites"></a>사전 요구 사항
평가를 실행 하려면 SQL Server **sysadmin** 역할의 멤버 여야 합니다.

## <a name="supported-source-and-target-versions"></a>지원 되는 원본 및 대상 버전
DMA는 SQL Server 업그레이드 관리자의 모든 이전 버전을 대체 하며 대부분의 SQL Server 버전의 업그레이드에 사용 되어야 합니다. 지원 되는 원본 및 대상 버전:

**Sources**
- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012 
- SQL Server 2014
- SQL Server 2016
- Windows의 SQL Server 2017

**대상**
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- Windows 및 Linux의 SQL Server 2017
- Azure SQL 데이터베이스
- Azure SQL Database Managed Instance
- Azure 가상 머신에서 실행 중인 SQL server

## <a name="see-also"></a>참조
[SQL Server 마이그레이션 평가](../dma/dma-assesssqlonprem.md)     
[Data Migration Assistant: 구성 설정](../dma/dma-configurationsettings.md)     
[Data Migration Assistant를 사용 하 여 온-프레미스 SQL Server 마이그레이션](../dma/dma-migrateonpremsql.md)     
[Data Migration Assistant: 모범 사례](../dma/dma-bestpractices.md)     
