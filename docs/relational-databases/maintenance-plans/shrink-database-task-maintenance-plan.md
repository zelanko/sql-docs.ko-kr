---
title: 데이터베이스 축소 태스크(유지 관리 계획) | Microsoft 문서
description: 데이터베이스 축소 태스크를 사용하여 선택한 SQL Server 데이터베이스의 크기를 줄이는 태스크를 만드는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- Shrink Database Task
- Shrink Database(s) Task
- sql13.swb.maint.shrink.f1
helpviewer_keywords:
- Shrink Database Task dialog box
ms.assetid: a9874cac-cded-4145-9c38-8aafd267dbee
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8456bacbc10b4b597a33c577ac7df12f0ba392cc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715341"
---
# <a name="shrink-database-task-maintenance-plan"></a>데이터베이스 축소 태스크(유지 관리 계획)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **데이터베이스 축소 태스크** 대화 상자를 사용하여 선택한 데이터베이스의 크기를 줄이는 작업을 만들 수 있습니다. 아래 옵션을 사용하면 데이터베이스를 축소한 후 사용되지 않는 상태로 데이터베이스에 유지할 공간의 양을 결정할 수 있습니다. 이 비율이 커질수록 데이터베이스를 축소할 수 있는 비율이 줄어듭니다. 이 값은 데이터베이스에 있는 실제 데이터의 비율에 따라 결정됩니다. 예를 들어 60MB의 데이터와 40MB의 사용 가능한 공간이 있는 100MB의 데이터베이스에서 사용 가능한 공간의 비율을 50%로 설정하면 60MB의 50%는 30MB이기 때문에 데이터 공간은 60MB가 되고 사용 가능한 공간은 30MB가 됩니다. 데이터베이스에서 남는 공간만 제거됩니다. 유효한 값은 0에서 100까지입니다.  
  
 파일 끝에 있는 데이터 페이지를 파일 앞의 사용되지 않은 공간으로 이동하여 데이터 파일을 축소하면 공간이 복구됩니다. 파일 끝에 사용 가능한 공간을 충분히 확보한 다음 파일 끝에 있는 데이터 페이지를 할당 해제하고 파일 시스템에 반환할 수 있습니다.  
  
> [!WARNING]  
>  파일 축소를 위해 이동되는 데이터는 파일 내의 모든 사용 가능한 위치로 분산될 수 있습니다. 이로 인해 인덱스 조각화가 발생하여 인덱스 범위를 검색하는 쿼리 성능이 저하될 수 있습니다. 조각화를 방지하려면 축소 후 파일에 대한 인덱스를 다시 작성하는 것이 좋습니다.  
  
 이 태스크는 DBCC SHRINKDATABASE 문을 실행합니다.  
  
## <a name="options"></a>옵션  
 **연결**  
 이 태스크를 수행할 때 사용할 서버 연결을 선택합니다.  
  
 **새로 만들기**  
 이 태스크를 수행할 때 사용할 새 서버 연결을 만듭니다. 아래에서는 **새 연결** 대화 상자에 대해 설명합니다.  
  
 **데이터베이스**  
 이 태스크의 영향을 받는 데이터베이스를 지정합니다.  
  
-   **모든 데이터베이스**  
  
     tempdb를 제외한 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대해 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다.  
  
-   **모든 시스템 데이터베이스**  
  
     tempdb를 제외한 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터베이스에 대해 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다. 사용자가 만든 데이터베이스에 대해서는 유지 관리 태스크가 실행되지 않습니다.  
  
-   **모든 사용자 데이터베이스**  
  
     사용자가 만든 모든 데이터베이스에 대해 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터베이스에 대해서는 유지 관리 태스크가 실행되지 않습니다.  
  
-   **다음 데이터베이스**  
  
     선택한 데이터베이스에 대해서만 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다. 이 옵션을 선택한 경우에는 목록에서 하나 이상의 데이터베이스를 선택해야 합니다.  
  
    > [!NOTE]  
    >  유지 관리 계획은 호환성 수준 80 이상으로 설정된 데이터베이스에 대해서만 실행합니다. 호환성 수준 70 이하로 설정된 데이터베이스는 표시되지 않습니다.  
  
 **데이터베이스 크기가 다음을 초과하면 축소**  
 데이터베이스 축소 태스크를 시작하는 기준이 되는 크기(MB)를 지정합니다.  
  
 **축소 후 데이터 공간 유지 비율**  
 데이터베이스 파일의 사용 가능한 공간이 이 크기에 도달하면 축소를 중지합니다.  
  
 **T-SQL 보기**  
 선택한 옵션을 기반으로 서버에 대해 수행한 이 태스크의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 표시합니다.  
  
> [!NOTE]  
>  영향을 받은 개체 수가 많은 경우에는 표시하는 데 시간이 오래 걸릴 수 있습니다.  
  
## <a name="new-connection-dialog-box"></a>새 연결 대화 상자  
 **연결 이름**  
 새 연결의 이름을 입력합니다.  
  
 **서버 이름 선택 또는 입력**  
 이 태스크를 수행할 때 연결할 서버를 선택합니다.  
  
 **새로 고침**  
 사용할 수 있는 서버 목록을 새로 고칩니다.  
  
 **서버 로그온 정보 입력**  
 서버에 대한 인증 방법을 지정합니다.  
  
 **Windows NT 통합 보안 사용**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결합니다.  
  
 **특정 사용자 이름 및 암호 사용**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결합니다. 이 옵션은 사용할 수 없습니다.  
  
 **사용자 이름**  
 인증 시 사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 입력합니다. 이 옵션은 사용할 수 없습니다.  
  
 **암호**  
 인증 시 사용할 암호를 입력합니다. 이 옵션은 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [DBCC SHRINKDATABASE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)  
  
  
