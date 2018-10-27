---
title: 온-프레미스 SQL Server 또는 SQL Server Azure Vm에서 Azure SQL Database로 마이그레이션 Data Migration Assistant를 사용 하 여 | Microsoft Docs
description: 온-프레미스 SQL Server는 Azure SQL Database로 마이그레이션할 Data Migration Assistant 사용 방법 알아보기
ms.custom: ''
ms.date: 10/20/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: pochiraju
ms.author: rajpo
manager: craigg
ms.openlocfilehash: db4b48d736b46c0381749943916272e763a077c7
ms.sourcegitcommit: 38f35b2f7a226ded447edc6a36665eaa0376e06e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49643851"
---
# <a name="migrate-on-premises-sql-server-or-sql-server-on-azure-vms-to-azure-sql-database-using-the-data-migration-assistant"></a>온-프레미스 SQL Server 또는 Azure Vm에서 SQL Server Data Migration Assistant를 사용 하 여 Azure SQL Database로 마이그레이션

Data Migration Assistant는 Azure Vm 또는 Azure SQL Database에서 SQL Server 온-프레미스 및 이후 버전의 SQL Server로 업그레이드 하거나 SQL Server로의 마이그레이션을 원활 하 게 평가 제공합니다.

이 문서에서는 Data Migration Assistant를 사용 하 여 Azure SQL Database로 마이그레이션 SQL Server 온-프레미스에 대 한 단계별 지침을 제공 합니다.   

## <a name="create-a-new-migration-project"></a>새 마이그레이션 프로젝트 만들기

1. 왼쪽된 창에서 선택 **새로 만들기** (+)를 선택한 후 합니다 **마이그레이션** 프로젝트 형식.

2. 원본 유형으로 설정 **SQL Server** 대상 서버를 입력 하 고 **Azure SQL Database**합니다.

3. **만들기**를 선택합니다.

   ![마이그레이션 프로젝트 만들기](../dma/media/NewCreate1.png)

## <a name="specify-the-source-server-and-database"></a>원본 서버와 데이터베이스를 지정 합니다.

1. 원본에 대 한 아래 **원본 서버에 연결**를 **서버 이름** 텍스트 상자에서 원본 SQL Server 인스턴스의 이름을 입력 합니다.

2. 선택 합니다 **인증 유형** 원본 SQL Server 인스턴스에서 지원 합니다.

   > [!NOTE]
   > Recommedned 선택 하 여 연결을 암호화 하는 것은 **연결 암호화** 아래의 확인란 **연결 poperties**합니다.

    ![원본 서버 선택](../dma/media/select-source-server.png)

3. **연결**을 선택합니다.

4. Azure SQL Database로 마이그레이션할 단일 원본 데이터베이스를 선택 합니다.

   > [!NOTE]
   > 데이터베이스 및 보기를 평가 하 고 적용 하려는 경우 권장 마이그레이션 선택 하기 전에 수정 합니다 **마이그레이션하기 전에 평가 데이터베이스?** 확인란 합니다.

    ![원본 데이터베이스를 선택 합니다.](../dma/media/select-source-database.png)

5. **다음**을 선택합니다.

## <a name="specify-the-target-server-and-database"></a>대상 서버 및 데이터베이스를 지정 합니다.

1. 대상에 대해 아래 **대상 서버에 연결**를 **서버 이름** 텍스트 상자에 Azure SQL Database 인스턴스의 이름을 입력 합니다. 

2. 선택 된 **인증 유형** 대상 Azure SQL Database 인스턴스에서 지원 합니다.

   > [!NOTE]
   > Recommedned 선택 하 여 연결을 암호화 하는 것은 **연결 암호화** 아래의 확인란 **연결 poperties**합니다.

     ![대상 서버 선택](../dma/media/select-target-server.png)

3. **연결**을 선택합니다.

4. 단일 대상 데이터베이스를 마이그레이션할를 선택 합니다.

   > [!NOTE]
   > Windows 사용자 마이그레이션 하려는 경우는 **대상 외부 사용자 도메인 이름** 텍스트 상자,으로 외부 사용자 도메인 이름을 올바르게 지정 되어 있는지 확인 합니다.

    ![대상 데이터베이스를 선택 합니다.](../dma/media/select-target-database.png)

5. **다음**을 선택합니다.

## <a name="select-schema-objects"></a>스키마 개체를 선택 합니다.

1.  Azure SQL Database로 마이그레이션할 원본 데이터베이스에서 스키마 개체를 선택 합니다.

    ![스키마 개체를 선택 합니다.](../dma/media/select-schema-objects.png)

       > [!NOTE]
       > 으로 변환할 수 없는 개체 중 일부를-는 자동 해결 기회를 사용 하 여 표시 됩니다. 왼쪽된 창에서 이러한 개체를 클릭 하면 제안 된 수정 오른쪽 창에서 표시 됩니다. 픽스를 검토 하 고 적용 하거나 개체에서 모든 변경 내용을 무시 하도록 선택 합니다. 해당 적용 또는 하나의 개체에 대 한 모든 변경 내용을 무시 하 고 다른 데이터베이스 개체가 변경 영향을 주지 않습니다. 문은 자동으로 수정 하거나 변환할 수 없는 데이터베이스에서 대상 데이터베이스로 재현를 주석 처리 됩니다.

    ![제안 된 수정](../dma/media/suggested-fix.png)

2. 선택 **일반 SQL 스크립트**합니다.
 
3. 생성된 된 스크립트를 검토 합니다.

    ![생성 된 스크립트](../dma/media/generated-script.png)

## <a name="deploy-schema"></a>스키마 배포

1. 선택 **스키마 배포**합니다.

2. 스키마 배포 결과를 검토 합니다.
 
    ![스키마 배포 결과](../dma/media/schema-deployment-results.png)

3. 선택 **데이터 마이그레이션** 데이터 마이그레이션 프로세스를 시작 합니다.
 
4. 마이그레이션할 데이터를 사용 하 여 테이블을 선택 합니다.

    ![마이그레이션할 테이블 선택](../dma/media/select-tables-to-migrate.png) 

5. 선택 **데이터 마이그레이션 시작**합니다.
 
마지막 화면에는 전반적인 상태를 보여 줍니다.

   ![마이그레이션 상태](../dma/media/migration-status.png) 

## <a name="see-also"></a>참고자료

- [Data Migration Assistant (DMA)](../dma/dma-overview.md)
- [Data Migration Assistant: 구성 설정](../dma/dma-configurationsettings.md)
- [Data Migration Assistant: 모범 사례](../dma/dma-bestpractices.md)
