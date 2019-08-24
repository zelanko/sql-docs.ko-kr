---
title: SQL Server Integration Service 마이그레이션 평가 (Data Migration Assistant)를 수행 합니다. Microsoft Docs
description: Data Migration Assistant를 사용 하 여 관리 되는 인스턴스로 Azure SQL Database Azure SQL Database 마이그레이션하기 전에 온-프레미스 SQL Server Integration Services를 평가 하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 08/23/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 14e53b3820e784916484cbe6a15ba82cd2ed5c8e
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70001375"
---
# <a name="perform-a-sql-server-integration-service-migration-assessment-with-data-migration-assistant"></a>Data Migration Assistant를 사용 하 여 SQL Server Integration Service 마이그레이션 평가 수행

다음 단계별 지침은 Data Migration Assistant를 사용 하 여 SSIS (SQL Server Integration Services) 패키지를 Azure SQL Database 또는 Azure SQL Database 관리 되는 인스턴스로 마이그레이션하기 위한 첫 번째 평가를 수행 하는 데 도움이 됩니다.

## <a name="create-an-assessment"></a>평가 만들기

1. **새로 만들기** (+) 아이콘을 선택 하 고 **평가** 프로젝트 형식을 **Integration Service**로 선택 합니다.

1. 원본 및 대상 서버 유형을 설정 합니다.

    **SQL Server**로 원본을 선택 하 고 대상 서버 유형을 **Azure SQL Database** 또는 **Azure SQL Database 관리 되는 인스턴스로**설정 합니다.

1. **만들기**를 클릭합니다.

    ![평가 만들기](media/dma-assess-ssis/dma-assess-ssis-create.png)

## <a name="add-sources-to-assess"></a>평가할 소스 추가

1. 기본 옵션을 따르고 **원본 선택**에서 **다음** 을 클릭 합니다.

1. SQL server 인스턴스 이름을 입력 하 고 인증 유형을 선택한 후 올바른 연결 속성을 설정 합니다.
1. SSIS 패키지를 포함 하는 폴더 경로를 입력 하십시오.
1. 패키지 암호화 암호 (해당 하는 경우)를 입력 한 다음 **연결**합니다.
1. 평가할 파일 시스템을 선택한 다음 **추가**를 선택 합니다.
  ![소스 추가](media/dma-assess-ssis/dma-assess-ssis-addsource.png)
1. 여러 폴더를 평가 해야 하는 경우 **원본 추가** 를 선택 하 여 연결 플라이 아웃 메뉴를 엽니다.
1. **평가 시작**을 클릭 합니다.
  ![평가 시작](media/dma-assess-ssis/dma-assess-ssis-assess.png)

## <a name="view-results"></a>결과 보기

호환성 문제 범주는 온-프레미스 SSIS 패키지를 Azure SSIS Integration Runtime로 마이그레이션하는 것을 차단 하는 부분적으로 지원 되거나 지원 되지 않는 기능을 제공 합니다. 그런 다음 해당 문제를 해결 하는 데 도움이 되는 권장 사항을 제공 합니다.

![결과 보기](media/dma-assess-ssis/dma-assess-ssis-result.png)

## <a name="next-steps"></a>다음 단계

- [Azure SQL Database 관리 되는 인스턴스로 SQL Server Integration Services 패키지 마이그레이션](https://docs.microsoft.com/en-us/azure/dms/how-to-migrate-ssis-packages-managed-instance)
- [SQL Server Integration Services 패키지를 Azure SQL Database에 다시 배포](https://docs.microsoft.com/en-us/azure/dms/how-to-migrate-ssis-packages)
