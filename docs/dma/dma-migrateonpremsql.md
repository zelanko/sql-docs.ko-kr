---
title: Data Migration Assistant를 사용 하 여 SQL Server 업그레이드
description: Data Migration Assistant를 사용 하 여 온-프레미스 SQL Server를 SQL Server의 최신 버전으로 업그레이드 하거나 Azure Vm에서 SQL Server 하는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 05/18/2019
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
ms.author: jtoland
ms.openlocfilehash: fc78354e3b422342e376bd7ebe75233dcd3ffaee
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056530"
---
# <a name="upgrade-sql-server-using-the-data-migration-assistant"></a>Data Migration Assistant를 사용 하 여 SQL Server 업그레이드

Data Migration Assistant은 온-프레미스 SQL Server를 원활 하 게 평가 하 고, 이후 버전의 SQL Server 또는 마이그레이션을 Azure Vm 또는 Azure SQL Database에서 SQL Server로 업그레이드 하는 기능을 제공 합니다.

이 문서에서는 SQL Server 온-프레미스를 SQL Server의 이후 버전으로 업그레이드 하거나 Data Migration Assistant를 사용 하 여 Azure Vm에서 SQL Server 하는 방법에 대 한 단계별 지침을 제공 합니다.

## <a name="create-a-new-migration-project"></a>새 마이그레이션 프로젝트 만들기

1. 왼쪽 창에서 **새로 만들기** (+), **마이그레이션** 프로젝트 형식을 차례로 선택 합니다.

2. 온-프레미스 SQL Server를 온-프레미스 SQL Server 최신 버전으로 업그레이드 하는 경우 원본 및 대상 서버 유형을 **SQL Server** 로 설정 합니다.

3. **만들기**를 선택합니다.

   ![마이그레이션 프로젝트 만들기](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>원본 및 대상 지정

1. 원본에 대해 **원본 서버 정보** 섹션의 **서버 이름** 필드에 SQL Server 인스턴스 이름을 입력 합니다. 

2. 원본 SQL Server 인스턴스에서 지 원하는 **인증 유형을** 선택 합니다.

3. 대상의 경우 **대상 서버 정보** 섹션의 **서버 이름** 필드에 SQL Server 인스턴스 이름을 입력 합니다. 

4. 대상 SQL Server 인스턴스에서 지 원하는 **인증 유형을** 선택 합니다.

5. 연결 **속성** 섹션에서 **연결 암호화** 를 선택 하 여 연결을 암호화 하는 것이 좋습니다.

6. **다음**을 클릭합니다.

   ![원본 및 대상 지정 페이지](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>데이터베이스 추가

1. **데이터베이스 추가** 페이지의 왼쪽 창에서 해당 데이터베이스만 선택 하 여 마이그레이션하려는 특정 데이터베이스를 선택 합니다.

   기본적으로 원본 SQL Server 인스턴스의 모든 사용자 데이터베이스가 마이그레이션하도록 선택 됩니다.

2. 페이지의 오른쪽에 있는 마이그레이션 설정을 사용 하 여 다음을 수행 하 여 데이터베이스에 적용 되는 마이그레이션 옵션을 설정 합니다.

   > [!NOTE]
   > 왼쪽 창에서 서버를 선택 하 여 마이그레이션하는 모든 데이터베이스에 마이그레이션 설정을 적용할 수 있습니다. 또한 왼쪽 창에서 데이터베이스를 선택 하 여 특정 설정을 사용 하 여 개별 데이터베이스를 구성할 수 있습니다.

    a. **백업 작업을 위해 원본 및 대상 SQL server에서 액세스할 수 있는 공유 위치**를 지정 합니다. 원본 SQL Server 인스턴스를 실행 하는 서비스 계정에 공유 위치에 대 한 쓰기 권한이 있고 대상 서비스 계정에 공유 위치에 대 한 읽기 권한이 있는지 확인 하십시오.

    b. 대상 서버에서 데이터 및 트랜잭션 로그 파일을 복원할 위치를 지정 합니다.

    ![데이터베이스 추가 페이지](../dma/media/AddDatabases.png)

3. **공유 위치 옵션** 상자에서 원본 및 대상 SQL Server 인스턴스에서 액세스할 수 있는 공유 위치를 입력 합니다.

4. 원본 및 대상 SQL Server 모두에 액세스할 수 있는 공유 위치를 제공할 수 없는 경우 **대상 서버에서 읽고 복원할 수 있는 다른 위치에 데이터베이스 백업 복사**를 선택 합니다. 그런 다음 **복원에 대 한 백업 위치 옵션** 상자에 값을 입력 합니다. 

   Data Migration Assistant를 실행 하는 사용자 계정에 백업 위치에 대 한 읽기 권한과 대상 서버가 복원 하는 위치에 대 한 쓰기 권한이 있는지 확인 합니다.

   ![데이터베이스 백업을 다른 위치로 복사 하는 옵션](../dma/media/CopyDatabaseDifferentLocation.png)

5. **다음**을 선택합니다.

Data Migration Assistant는 백업 폴더, 데이터 및 로그 파일 위치에 대 한 유효성 검사를 수행 합니다. 유효성 검사에 실패 하면 옵션을 수정 하 고 **다음**을 선택 합니다.

## <a name="select-logins"></a>로그인 선택

1. 마이그레이션의 특정 로그인을 선택 합니다.

   > [!IMPORTANT]
   > 마이그레이션하기 위해 선택한 데이터베이스에서 하나 이상의 사용자에 매핑되는 로그인을 선택 해야 합니다.   

   기본적으로 마이그레이션에 적합 한 모든 SQL Server 및 Windows 로그인은 마이그레이션하도록 선택 됩니다.

2. **마이그레이션 시작**을 선택 합니다.

   ![로그인 선택 및 마이그레이션 시작](../dma/media/SelectLogins.png)

## <a name="view-results"></a>결과 보기

**결과 보기** 페이지에서 마이그레이션 진행률을 모니터링할 수 있습니다.

![결과 보기 페이지](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>마이그레이션 결과 내보내기

1. **결과 보기** 페이지 맨 아래에 있는 **보고서 내보내기** 를 클릭 하 여 마이그레이션 결과를 CSV 파일에 저장 합니다.

2. 저장 된 파일에서 로그인 마이그레이션에 대 한 세부 정보를 검토 한 다음 변경 내용을 확인 합니다.

## <a name="see-also"></a>참고 항목

- [Data Migration Assistant (DMA)](../dma/dma-overview.md)
- [Data Migration Assistant: 구성 설정](../dma/dma-configurationsettings.md)
- [Data Migration Assistant: 모범 사례](../dma/dma-bestpractices.md)
