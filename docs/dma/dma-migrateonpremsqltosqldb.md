---
title: Data Migration Assistant를 사용 하 여 Azure SQL Database SQL Server 마이그레이션
description: Data Migration Assistant를 사용 하 여 온-프레미스 SQL Server를로 마이그레이션하는 방법에 대해 알아봅니다 Azure SQL Database
ms.date: 06/29/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: ec6b5ad0ab2047e72a1f3e3e5dfcd9fc49b954d9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749782"
---
# <a name="migrate-on-premises-sql-server-or-sql-server-on-azure-vms-to-azure-sql-database-using-the-data-migration-assistant"></a>Azure Vm에서 온-프레미스 SQL Server 또는 SQL Server를 마이그레이션하여 Data Migration Assistant를 사용 하 여 Azure SQL Database

Data Migration Assistant은 온-프레미스 SQL Server를 원활 하 게 평가 하 고, 이후 버전의 SQL Server 또는 마이그레이션을 Azure Vm 또는 Azure SQL Database에서 SQL Server로 업그레이드 하는 기능을 제공 합니다.

이 문서에서는 Data Migration Assistant를 사용 하 여 온-프레미스에서 Azure SQL Database로 SQL Server 마이그레이션하기 위한 단계별 지침을 제공 합니다.

## <a name="create-a-new-migration-project"></a>새 마이그레이션 프로젝트 만들기

1. 왼쪽 창에서 **새로 만들기** (+)를 선택 하 고 **마이그레이션** 프로젝트 유형을 선택 합니다.

2. 원본 유형을 **SQL Server** 로 설정 하 고 대상 서버 유형을 **Azure SQL Database**로 설정 합니다.

3. **만들기**를 선택합니다.

   ![마이그레이션 프로젝트 만들기](../dma/media/NewCreate1.png)

## <a name="specify-the-source-server-and-database"></a>원본 서버 및 데이터베이스 지정

1. 원본에 대해 원본 **서버에 연결**의 **서버 이름** 텍스트 상자에 원본 SQL Server 인스턴스 이름을 입력 합니다.

2. 원본 SQL Server 인스턴스에서 지원하는 **인증 형식**을 선택합니다.

   > [!NOTE]
   > 연결 **암호화** 확인란을 선택 하 여 연결 상태에서 연결을 암호화 하는 것이 **좋습니다.**

    ![원본 서버 선택](../dma/media/select-source-server.png)

3. **연결**을 선택합니다.

4. Azure SQL Database 마이그레이션할 단일 원본 데이터베이스를 선택 합니다.

   > [!NOTE]
   > 마이그레이션을 수행 하기 전에 데이터베이스를 평가 하 여 권장 해결 방법을 확인 하 고 적용 하려면 **마이그레이션 전에 데이터베이스 평가** 확인란을 선택 합니다.

    ![원본 데이터베이스 선택](../dma/media/select-source-database.png)

5. **다음**을 선택합니다.

## <a name="specify-the-target-server-and-database"></a>대상 서버 및 데이터베이스 지정

1. 대상의 경우 **대상 서버에 연결**의 **서버 이름** 텍스트 상자에 Azure SQL Database 인스턴스의 이름을 입력 합니다. 

2. 대상 Azure SQL Database 인스턴스에서 지 원하는 **인증 유형을** 선택 합니다.

   > [!NOTE]
   > 연결 **암호화** 확인란을 선택 하 여 연결 상태에서 연결을 암호화 하는 것이 **좋습니다.**

     ![대상 서버 선택](../dma/media/select-target-server.png)

3. **연결**을 선택합니다.

4. 원본 데이터베이스를 마이그레이션할 단일 대상 데이터베이스를 선택합니다.

   > [!NOTE]
   > Windows 사용자를 마이그레이션하려면 대상 외부 **사용자 도메인 이름** 텍스트 상자에서 대상 외부 사용자 도메인 이름이 올바르게 지정 되어 있는지 확인 합니다.

    ![대상 데이터베이스 선택](../dma/media/select-target-database.png)

5. **다음**을 선택합니다.

## <a name="select-schema-objects"></a>스키마 개체 선택

1. Azure SQL Database로 마이그레이션할 원본 데이터베이스에서 스키마 개체를 선택합니다.

    ![스키마 개체 선택](../dma/media/select-schema-objects.png)

    > [!NOTE]
    > 그대로 변환할 수 없는 일부 개체의 경우 자동 수정 옵션이 제공됩니다. 왼쪽 창에서 이러한 개체를 클릭하면 오른쪽 창에 수정 제안 사항이 표시됩니다. 해당 수정 내용을 검토하고 개체별로 모든 변경 내용을 적용하거나 무시하도록 선택합니다. 개체 하나에 대해 모든 변경을 적용하거나 무시해도 다른 데이터베이스 개체의 변경 내용에는 영향을 주지 않습니다. 변환하거나 자동으로 수정할 수 없는 문은 대상 데이터베이스로 재현되어 주석 처리됩니다.

    ![제안 된 수정](../dma/media/suggested-fix.png)

2. **일반 SQL 스크립트**를 선택 합니다.

3. 생성 된 스크립트를 검토 합니다.

    ![생성 된 스크립트](../dma/media/generated-script.png)

## <a name="deploy-schema"></a>스키마 배포

1. **스키마 배포**를 선택 합니다.

2. 스키마 배포 결과를 검토합니다.

    ![스키마 배포 결과](../dma/media/schema-deployment-results.png)

3. 데이터 **마이그레이션을 선택 하** 여 데이터 마이그레이션 프로세스를 시작 합니다.

4. 마이그레이션할 데이터가 포함된 테이블을 선택합니다.

    ![마이그레이션할 테이블 선택](../dma/media/select-tables-to-migrate.png) 

5. **데이터 마이그레이션 시작**을 선택 합니다.

마지막 화면에 전체 상태가 표시됩니다.

   ![마이그레이션 상태](../dma/media/migration-status.png) 

## <a name="see-also"></a>참고 항목

* [Data Migration Assistant(DMA)](../dma/dma-overview.md)
* [Data Migration Assistant: 구성 설정](../dma/dma-configurationsettings.md)
* [Data Migration Assistant: 모범 사례](../dma/dma-bestpractices.md)
