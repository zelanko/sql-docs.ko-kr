---
title: Data Migration Assistant (SQL Server)의 개요 | Microsoft Docs
description: 다른 SQL Server 또는 Azure 데이터베이스에 SQL Server 데이터베이스를 마이그레이션하기 위해 Data Migration Assistant를 사용 하는 방법 알아보기
ms.custom: ''
ms.date: 03/12/2019
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
manager: craigg
ms.openlocfilehash: 0bb91177a204f93bd141d57b90420678dcd0b722
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57973792"
---
# <a name="overview-of-data-migration-assistant"></a>Data Migration Assistant 개요
Data Migration Assistant (DMA)를 사용 하면 새 버전의 SQL Server 또는 Azure SQL Database에서 데이터베이스 기능에 영향을 줄 수 있는 호환성 문제를 감지 하 여 최신 데이터 플랫폼으로 업그레이드 합니다. DMA는 성능 및 안정성 향상 대상 환경에 대 한 권장 하 고 대상 서버에 원본 서버에서 스키마, 데이터 및 포함 되지 않은 개체를 이동할 수 있습니다.

> [!NOTE] 
> 대규모 마이그레이션의 (측면에서 번호 및 데이터베이스의 크기)를 사용 하는 권장 합니다 [Azure Database Migration Service](/azure/dms/dms-overview)는 대규모 데이터베이스를 마이그레이션할 수 있습니다.
  
## <a name="get-data-migration-assistant"></a>Data Migration Assistant 가져오기
DMA를 설치 하려면 최신 버전의 도구를 다운로드 합니다 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53595), 실행 합니다 **DataMigrationAssistant.msi** 파일.

## <a name="capabilities"></a>Capabilities
- Azure SQL database로 마이그레이션하는 온-프레미스 SQL Server 인스턴스를 평가 합니다. 평가 워크플로 사용 하면 Azure SQL database 마이그레이션에 영향을 줄 수 및 해결 하는 방법에 대 한 자세한 지침을 제공 하는 다음 문제를 검색할 수 있습니다.

  - 마이그레이션 차단 문제: Azure SQL database를 온-프레미스 SQL Server 데이터베이스 마이그레이션 차단 하는 호환성 문제를 검색 합니다. DMA는 해당 문제를 해결 하기 위한 권장 사항을 제공 합니다.

  - 부분적으로 지원 되거나 지원 되지 않는 기능은 다음과 같습니다. 현재 원본 SQL Server 인스턴스에 사용 되는 부분적으로 지원 되거나 지원 되지 않는 기능을 검색 합니다. DMA는 마이그레이션 프로젝트에 통합할 수 있습니다 있도록 포괄적인 Azure 및 완화 단계에서 사용 가능한 대체 방법 권장 사항 집합을 제공 합니다.

- 온-프레미스 SQL server 업그레이드에 영향을 줄 수 있는 문제를 검색 합니다. 이러한 호환성 문제를 설명 하 고 다음 범주로 구성 됩니다.

  - 주요 변경 내용
  - 동작 변경 내용
  - 사용되지 않는 기능

- 데이터베이스는 업그레이드 후에 활용할 수 있는 대상 SQL Server 플랫폼의 새로운 기능을 검색 합니다. 이러한 기능 권장 사항으로 설명 하 고 다음 범주로 구성 됩니다.

  - 성능
  - 보안
  - 스토리지

- 최신 SQL Server 호스트 인스턴스가 온-프레미스 또는 온-프레미스 네트워크에서 액세스할 수 있는 Azure 가상 컴퓨터 (VM)에서 온-프레미스 SQL Server 인스턴스를 마이그레이션하십시오. VPN 또는 기타 기술을 사용 하 여 Azure VM은 액세스할 수 있습니다. 마이그레이션 워크플로 사용 하면 다음 구성 요소를 마이그레이션할 수 있습니다.

  - 데이터베이스의 스키마
  - 데이터 및 사용자
  - 서버 역할
  - SQL Server 및 Windows 로그인

- 성공적인 마이그레이션 후 응용 프로그램 수 대상 SQL Server 데이터베이스에 원활 하 게 연결 합니다.

## <a name="prerequisites"></a>사전 요구 사항
평가 실행 하려면 SQL Server의 멤버일 필요가 **sysadmin** 역할입니다.

## <a name="supported-source-and-target-versions"></a>지원 되는 원본 및 대상 버전
DMA는 모든 이전 버전의 SQL Server 업그레이드 관리자를 대체 하 고 대부분의 SQL Server 버전에 대 한 업그레이드에 사용 해야 합니다. 지원 되는 원본 및 대상 버전이 됩니다.

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

## <a name="see-also"></a>참고자료
[SQL Server 마이그레이션 평가](../dma/dma-assesssqlonprem.md)     
[Data Migration Assistant: 구성 설정](../dma/dma-configurationsettings.md)     
[Data Migration Assistant를 사용 하 여 마이그레이션할 온-프레미스 SQL Server](../dma/dma-migrateonpremsql.md)     
[Data Migration Assistant: 모범 사례](../dma/dma-bestpractices.md)     
