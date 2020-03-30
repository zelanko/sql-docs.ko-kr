---
title: 데이터베이스 엔진 업그레이드 완료 | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.technology: install
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 3f08087e-e532-416c-8caa-e0ec88c57596
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 72c5ff1bcb2162bbe3f3584222214ba448b67d68
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68054278"
---
# <a name="complete-the-database-engine-upgrade"></a>데이터베이스 엔진 업그레이드 완료

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 업그레이드가 완료된 후에 추가로 수행해야 할 여러 단계가 있습니다. 여기에는 다음과 같은 옵션이 포함됩니다.  
  
[!INCLUDE[ssDE](../../includes/ssde-md.md)]을 업그레이드한 후에 다음 태스크를 완료하세요.  
  
- **데이터베이스 백업:** 각 데이터베이스의 전체 백업을 수행합니다.  

- **새 기능 사용:** SQL Server 2016 및 SQL Server 2017에서는 데이터베이스에 대한 DATABASE_COMPATIBILITY 수준이 130 이상으로 변경된 경우에만 일부 변경 내용을 사용할 수 있습니다.  자세한 내용 및 권장되는 워크플로는 [데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)을 참조하세요. 데이터베이스에 SQL Server 2014에서 만든 메모리 최적화 테이블이 있는 경우 [메모리 최적화 테이블에 대한 통계](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md)를 검토합니다.
  
- **Integration Services:**  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 형식으로 Integration Services 패키지를 마이그레이션합니다. 자세한 내용은 [Integration Services 패키지 업그레이드](../../integration-services/install-windows/upgrade-integration-services-packages.md) 합니다.  
  
- **Reporting Services:** 새로 설치한 SQL Server를 업그레이드하는 경우 Reporting Services 암호화 키를 복원합니다. 자세한 내용은 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)을 참조하세요.  
  
- **Master Data Services:** MDS 데이터베이스 스키마를 업그레이드하고 SQL Server 2017 웹 애플리케이션을 만듭니다. 자세한 내용은 [Upgrade Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md)를 참조하세요.  
  
- **Data Quality Services:** DQS 데이터베이스 스키마를 업그레이드하고 DQS 데이터베이스 스키마 업그레이드를 확인합니다. 자세한 내용은 [Upgrade Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md)를 참조하세요.  
  
- **전체 텍스트 검색:** 쿼리 결과의 의미 일관성을 유지하기 위해 전체 텍스트 카탈로그를 다시 채웁니다. 자세한 내용은 [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)를 참조하세요.  
  
