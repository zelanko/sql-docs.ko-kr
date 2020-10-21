---
title: Azure로 SQL Server Integration Services 마이그레이션 개요 | Microsoft Docs
description: 이 문서에서는 SQL Server Integration Services를 Azure로 마이그레이션하는 프로세스와 도구를 중심으로 설명합니다.
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6fe5435882a55b8e8fcc56dff5d65f957fc6f8c4
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192513"
---
# <a name="migrate-on-premises-ssis-workloads-to-ssis-in-adf"></a>온-프레미스 SSIS 워크로드를 ADF의 SSIS로 마이그레이션

이 문서에는 SSIS(SQL Server Integration Services) 워크로드를 ADF의 SSIS로 마이그레이션하는 데 유용한 프로세스와 도구가 나와 있습니다.

[마이그레이션 개요](/azure/data-factory/scenario-ssis-migration-overview)에서는 ETL 워크로드를 온-프레미스 SSIS에서 ADF의 SSIS로 마이그레이션하는 전체 프로세스를 중심으로 설명합니다.

마이그레이션 프로세스는 [평가](/azure/data-factory/scenario-ssis-migration-overview#assessment) 및 [마이그레이션](/azure/data-factory/scenario-ssis-migration-overview#migration)의 두 단계로 구성됩니다.

## <a name="assessment"></a>평가

DMA(Data Migration Assistant)는 이 목적을 위해 로컬에서 설치 및 실행할 수 있는 무료 다운로드 가능 도구입니다. SSIS 패키지를 일괄 처리로 평가하고 호환성 문제를 확인하기 위해 Integration Services 유형의 DMA 평가 프로젝트를 만들 수 있습니다.

[Database Migration Assistant](../../dma/dma-overview.md)를 가져와 [패키지 평가를 수행](../../dma/dma-assess-ssis.md)합니다.

## <a name="migration"></a>마이그레이션

원본 SSIS 패키지의 스토리지 유형과 데이터베이스 워크로드의 마이그레이션 대상에 따라 SSIS 패키지를 마이그레이션하는 단계와 SSIS 패키지 실행을 예약하는 SQL Server 에이전트 작업이 다를 수 있습니다. 자세한 내용은 [이 페이지](/azure/data-factory/scenario-ssis-migration-overview#migration)를 참조하세요.

## <a name="next-steps"></a>다음 단계

- [SSIS 패키지를 Azure SQL Managed Instance로 마이그레이션](/azure/dms/how-to-migrate-ssis-packages-managed-instance).
- [SSMS(SQL Server Management Studio)를 사용하여 SSIS 작업을 ADF(Azure Data Factory)로 마이그레이션](/azure/data-factory/how-to-migrate-ssis-job-ssms)