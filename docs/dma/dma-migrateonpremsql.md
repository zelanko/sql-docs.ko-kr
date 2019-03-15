---
title: 업그레이드 온-프레미스 SQL Server 또는 SQL Server Data Migration Assistant를 사용 하 여 Azure Vm에서 SQL Server | Microsoft Docs
description: Azure Vm의 SQL Server 또는 SQL Server의 이후 버전으로는 온-프레미스 SQL Server를 업그레이드 하려면 Data Migration Assistant를 사용 하는 방법 알아보기
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 6d90a661c160fbbe473e6c30a8e45e9ea4f75056
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57974432"
---
# <a name="upgrade-on-premises-sql-server-to-sql-server-or-sql-server-on-azure-vms-using-the-data-migration-assistant"></a>SQL Server 또는 SQL Server Data Migration Assistant를 사용 하 여 Azure Vm에서 온-프레미스 SQL Server 업그레이드

Data Migration Assistant는 Azure Vm 또는 Azure SQL Database에서 SQL Server 온-프레미스 및 이후 버전의 SQL Server로 업그레이드 하거나 SQL Server로의 마이그레이션을 원활 하 게 평가 제공합니다.

이 문서에서는 Data Migration Assistant를 사용 하 여 온-프레미스 SQL Server Azure Vm의 SQL Server 또는 SQL Server의 최신 버전으로 업그레이드 하는 것에 대 한 단계별 지침을 제공 합니다.   

## <a name="create-a-new-migration-project"></a>새 마이그레이션 프로젝트 만들기

1. 왼쪽된 창에서 선택 **새로 만들기** (+)를 차례로 합니다 **마이그레이션** 프로젝트 형식.

2. 원본 및 대상 서버 유형으로 설정 **SQL Server** 온-프레미스 SQL Server는 온-프레미스 SQL Server의 이후 버전으로 업그레이드 하는 경우.

3. **만들기**를 선택합니다.

   ![마이그레이션 프로젝트 만들기](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>원본 및 대상 지정

1. 원본에 대 한 SQL Server 인스턴스 이름에를 입력 합니다 **서버 이름** 필드를 **서버 세부 정보를 원본** 섹션. 

2. 선택 합니다 **인증 유형** 원본 SQL Server 인스턴스에서 지원 합니다.

3. 대상에 대해 SQL Server 인스턴스 이름에를 입력 합니다 **서버 이름** 필드를 **대상 서버 세부 정보** 섹션입니다. 

4. 선택 된 **인증 유형** 대상 SQL Server 인스턴스에서 지원 합니다.

5. 선택 하 여 연결을 암호화 하는 것이 좋습니다 **연결 암호화** 에 **연결 속성** 섹션입니다.

6. **다음**을 클릭합니다.

   ![원본 및 대상 페이지를 지정 합니다.](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>데이터베이스 추가

1. 만의 왼쪽된 창에서 해당 데이터베이스를 선택 하 여 마이그레이션하려는 특정 데이터베이스를 선택 합니다 **데이터베이스를 추가할** 페이지입니다.

   기본적으로 원본 SQL Server 인스턴스에서 모든 사용자 데이터베이스 마이그레이션에 대 한 선택

2. 페이지의 오른쪽에 마이그레이션 설정을 사용 하 여 다음을 수행 하 여 데이터베이스에 적용 되는 마이그레이션 옵션을 설정 합니다.

   > [!NOTE]
   > 마이그레이션 설정으로 마이그레이션하는 왼쪽된 창에서 서버를 선택 하 여 모든 데이터베이스에 적용할 수 있습니다. 왼쪽된 창에서 데이터베이스를 선택 하 여 특정 설정을 사용 하 여 개별 데이터베이스를 구성할 수 있습니다.

    a. 지정 된 **백업 작업에 대 한 원본 및 대상 SQL 서버에서 액세스할 수 있는 위치를 공유**합니다. 소스를 실행 하는 서비스 계정 SQL Server 인스턴스에 있는 공유 위치에 대 한 권한이 읽고 쓰는 대상 서비스 계정에 공유 위치에 대 한 권한이 있는지 확인 합니다.

    b. 데이터와 대상 서버의 트랜잭션 로그 파일을 복원 하려면 위치를 지정 합니다.

    ![데이터베이스 페이지를 추가 합니다.](../dma/media/AddDatabases.png)

3. 원본 및 대상 SQL Server 인스턴스 액세스에 있는 공유 위치를 입력 합니다 **공유 위치 옵션** 상자입니다.

4. 해당 소스와 대상 SQL 서버를 선택 액세스할 공유 위치를 제공할 수 없으면 **대상 서버 읽고에서 복원할 수 있는 다른 위치로 데이터베이스 백업 복사**합니다. 그런 다음에 대 한 값을 입력 합니다 **복원 옵션에 대 한 백업 위치** 상자입니다. 

   Data Migration Assistant를 실행 하는 사용자 계정에 읽기 권한을 백업 위치에 있는지 확인 하 고 대상 서버는 복원 위치에 쓰기 권한이 있습니다.

   ![데이터베이스 백업을 다른 위치로 복사 하는 옵션](../dma/media/CopyDatabaseDifferentLocation.png)

5. **다음**을 선택합니다.

Data Migration Assistant는 백업 폴더, 데이터 및 로그 파일 위치에서 유효성 검사를 수행합니다. 모든 유효성 검사에 실패 하는 경우 옵션을 수정 하 고 선택한 **다음**합니다.

## <a name="select-logins"></a>로그인 선택

1. 마이그레이션에 대 한 특정 로그인을 선택 합니다.

   > [!IMPORTANT]
   > 마이그레이션을 위해 선택한 데이터베이스에서 하나 이상의 사용자에 매핑되는 로그인을 선택 해야 합니다.   

   기본적으로 마이그레이션에 적합 한 모든 SQL Server 및 Windows 로그인은 마이그레이션에 대 한 선택 됩니다.

2. 선택 **마이그레이션을 시작**합니다.

   ![로그인을 선택 하 고 마이그레이션 시작](../dma/media/SelectLogins.png)

## <a name="view-results"></a>결과 보기

마이그레이션 진행률을 모니터링할 수 있습니다 합니다 **결과 볼** 페이지입니다.

![뷰 결과 페이지](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>마이그레이션 결과 내보내기

1. 클릭 **보고서를 내보낼** 맨 아래에 **결과 볼** 마이그레이션 결과를 CSV 파일로 저장 하려면 페이지입니다.

2. 로그인 마이그레이션에 대 한 세부 정보에 대 한 저장된 된 파일을 검토 하 고 변경 내용을 확인 합니다.

## <a name="see-also"></a>참고자료

- [Data Migration Assistant (DMA)](../dma/dma-overview.md)
- [Data Migration Assistant: 구성 설정](../dma/dma-configurationsettings.md)
- [Data Migration Assistant: 모범 사례](../dma/dma-bestpractices.md)
