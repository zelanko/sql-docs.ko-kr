---
title: 온-프레미스 SQL Server (데이터 마이그레이션 길잡이)를 마이그레이션 | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: b535e41b93d337fc2cc1ae3f12699dd841bf91b9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="migrate-on-premises-sql-server-using-data-migration-assistant"></a>데이터 마이그레이션 길잡이 사용 하 여 온-프레미스 SQL Server로 마이그레이션

이 문서에서는 데이터 Migration Assistant를 사용 하 여 SQL 서버를 마이그레이션하는 단계별 지침을 제공 합니다.

데이터 마이그레이션 길잡이 원활 하 게 평가 및 최신 온-프레미스 SQL Server 및 SQL Azure VM 데이터 플랫폼의 마이그레이션을 제공합니다.  

마이그레이션을 수행 하려면 다음 작업을 완료 합니다.

- [새 마이그레이션 프로젝트 만들기](#create-a-new-migration-project)
- [원본 및 대상 지정](#specify-source-and-target)
- [데이터베이스를 추가 합니다.](#add-databases)
- [로그인을 선택 합니다.](#select-logins)

## <a name="create-a-new-migration-project"></a>새 마이그레이션 프로젝트 만들기

1. 클릭 **새로** (+)의 왼쪽된 창에 선택 된 **마이그레이션** 프로젝트 형식을 합니다.

1. 원본 및 대상 서버 유형으로 설정 **SQL Server** 는 온-프레미스 SQL Server를 업그레이드 하는 경우는 최신 온-프레미스 SQL Server.

1. **만들기**를 클릭합니다.

   ![마이그레이션 프로젝트 만들기](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>원본 및 대상 지정

1. SQL Server 인스턴스 이름을 입력 원본에 대 한는 **서버 이름** 필드에 **서버 세부 정보를 원본** 섹션. 

1. 선택 된 **인증 유형** 원본 SQL Server 인스턴스에서 지 원하는 합니다.

1. 대상에 대해에 SQL Server 인스턴스 이름을 입력 된 **서버 이름** 필드에 **대상 서버 세부 정보** 섹션. 

1. 선택 된 **인증 유형** 대상 SQL Server 인스턴스에서 지 원하는 합니다.

1. 선택 하 여 연결을 암호화 하는 것이 좋습니다. **연결 암호화** 에 **연결 속성** 섹션.

1. **다음**을 클릭합니다.

   ![원본 및 대상 페이지를 지정 합니다.](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>데이터베이스를 추가 합니다.

1. 만의 왼쪽된 창에서 해당 데이터베이스를 선택 하 여 마이그레이션할 특정 데이터베이스를 선택는 **데이터베이스를 추가할** 페이지.

   기본적으로 원본 SQL Server 인스턴스에서 모든 사용자 데이터베이스 마이그레이션에 대 한 선택

1. 페이지의 오른쪽에 마이그레이션 설정을 사용 하 여 다음을 수행 하 여 데이터베이스에 적용 되는 마이그레이션 옵션을 설정 합니다.

   > [!NOTE]
   > 왼쪽된 창에서 서버를 선택 하 여 마이그레이션하는 모든 데이터베이스에 마이그레이션 설정을 적용할 수 있습니다. 왼쪽된 창에서 데이터베이스를 선택 하 여 특정 설정을 사용 하 여 개별 데이터베이스를 구성할 수 있습니다.


 1. 지정 된 **백업 작업에 대 한 소스 및 대상 SQL server에서 액세스할 수 있는 위치를 공유**합니다. 소스를 실행 하는 서비스 계정 SQL Server 인스턴스에 쓰기 공유 위치에 대 한 권한이 있고 대상 서비스 계정에 읽기 공유 위치에 대 한 권한이 있는지 확인 합니다.

 1. 데이터와 대상 서버에 트랜잭션 로그 파일을 복원 하려면 위치를 지정 합니다.

    ![데이터베이스 페이지를 추가 합니다.](../dma/media/AddDatabases.png)

1. 원본 및 대상 SQL Server 인스턴스가에 액세스할 수 있는 공유 위치를 입력의 **위치 옵션을 공유** 상자입니다.

1. 해당 소스와 대상 SQL Server 선택에 권한이 있는 공유 위치를 제공할 수 없는 경우 **데이터베이스 백업을 대상 서버 읽고에서 복원할 수 있는 다른 위치로 복사**합니다. 그런 다음에 대 한 값을 입력에서 **복원 옵션에 대 한 백업에 대 한 위치** 상자입니다. 

   데이터 마이그레이션 길잡이 실행 하는 사용자 계정에 읽기 권한을 백업 위치에 있는지 확인 하 고 대상 서버를 복원 하는 위치에 쓰기 권한을 합니다.

   ![데이터베이스 백업을 다른 위치로 복사 하는 옵션](../dma/media/CopyDatabaseDifferentLocation.png)

1. **다음**을 클릭합니다.

데이터 마이그레이션 길잡이 유효성 검사를 수행 데이터 및 로그 파일 위치는 백업 폴더에 있습니다. 모든 유효성 검사에 실패할 경우 उ प क 옵션과 클릭 **다음**합니다.

## <a name="select-logins"></a>로그인을 선택 합니다.

1. 마이그레이션에 대 한 특정 로그인을 선택 합니다.

   > [!IMPORTANT]
   > 마이그레이션을 위해 선택한 데이터베이스에 하나 이상의 사용자에 매핑되는 로그인을 선택 해야 합니다.   

   기본적으로 마이그레이션에 대 한 포함 될 수 있는 모든 SQL Server 및 Windows 로그인은 마이그레이션에 대 한 선택 됩니다.

1. 클릭 **마이그레이션을 시작**합니다.

   ![로그인을 선택 하 고 마이그레이션을 시작합니다](../dma/media/SelectLogins.png)

## <a name="view-results"></a>결과 보기

마이그레이션 진행률을 모니터링할 수 있습니다는 **결과 볼** 페이지.

![보기 결과 페이지](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>마이그레이션 결과 내보내기

1. 클릭 **보고서 내보내기** 맨 아래에 **결과 볼** 마이그레이션 결과를 CSV 파일로 저장 하는 페이지입니다.

1. 로그인 마이그레이션에 대 한 세부 정보에 대 한 저장된 된 파일을 검토 하 고 변경 내용을 확인 합니다.

## <a name="see-also"></a>참고 항목

[데이터 마이그레이션 길잡이 (DMA)](../dma/dma-overview.md)

[데이터 마이그레이션 길잡이: 구성 설정](../dma/dma-configurationsettings.md)

[데이터 마이그레이션 길잡이:에 대 한 유용한 정보](../dma/dma-bestpractices.md)
