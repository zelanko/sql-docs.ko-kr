---
title: 메모리 액세스에 최적화된 테이블 사용을 위한 요구 사항 | Microsoft 문서
ms.custom: ''
ms.date: 11/24/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
caps.latest.revision: 65
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e08c8b1312c5aa9f0dac57195d937b12c94dca92
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="requirements-for-using-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블 사용을 위한 요구 사항
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Azure DB에서 메모리 내 OLTP 사용의 경우 [SQL 데이터베이스에서 메모리 내 시작](http://azure.microsoft.com/documentation/articles/sql-database-in-memory/)을 참조하세요.  
  
 [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md) 외에 메모리 내 OLTP를 사용하기 위한 요구 사항은 다음과 같습니다.  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1(또는 이상), 모든 버전. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 및 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] RTM(SP1 이전)의 경우 Enterprise, Developer 또는 Evaluation 버전이 필요합니다.
    
    > [!NOTE]
    > 메모리 내 OLTP에는 64비트 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 필요합니다.  
  
-   
            [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에는 메모리 최적화 테이블 및 인덱스에 데이터를 저장하기에 충분한 메모리와 온라인 워크로드를 지원하기 위한 추가 메모리가 필요합니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블에 필요한 메모리 예측](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) 을 참조하세요.  

-   VM(가상 머신)에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](을)를 실행하는 경우 메모리 최적화 테이블 및 인덱스에 필요한 메모리를 지원하기에 충분한 메모리가 VM에 할당되었는지 확인합니다. VM 호스트 응용 프로그램에 따라 VM에 대한 메모리 할당을 보장하는 구성 옵션을 메모리 예약 또는 동적 메모리를 사용하는 경우 최소 RAM이라고 할 수 있습니다. 이러한 설정이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 데이터베이스 요구에 충분한지 확인합니다.
  
-   지속형 메모리 최적화 테이블 크기의 2배에 해당하는 여유 디스크 공간  
  
-   메모리 내 OLTP를 사용하려면 프로세서에서 **cmpxchg16b** 명령을 지원해야 합니다. 최신 64비트 프로세서는 **cmpxchg16b**를 지원합니다.  
  
     가상 머신을 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이전 프로세서로 인한 오류가 표시되면 **cmpxchg16b**를 허용하도록 VM 호스트 응용 프로그램의 구성 옵션이 설정되어 있는지 확인합니다. 설정되어 있지 않은 경우 구성 옵션을 설정할 필요 없이 **cmpxchg16b** 를 지원하는 Hyper-V를 사용할 수 있습니다.  
  
-   메모리 내 OLTP는 **데이터베이스 엔진 서비스**의 일부로 설치됩니다.  
  
     보고서 생성([메모리 내 OLTP에 테이블 또는 저장 프로시저를 포팅해야 하는지 확인](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기를 통해 메모리 내 OLTP를 관리하기 위해)를 설치하려면 [SSMS(SQL Server Management Studio)를 다운로드](../../ssms/download-sql-server-management-studio-ssms.md)합니다.   
  
## <a name="important-notes-on-using-includehek2includeshek-2-mdmd"></a>[!INCLUDE[hek_2](../../includes/hek-2-md.md)] 사용에 관한 중요 사항  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상에서는 사용 가능한 메모리 외에 메모리 최적화 테이블의 크기에 대한 제한이 없습니다. 

-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 데이터베이스에 있는 모든 영구 테이블의 총 메모리 내 크기는 250GB를 초과할 수 없습니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블에 필요한 메모리 예측](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)을 참조하세요.  

> [!NOTE]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1부터 Standard 및 Express Edition은 메모리 내 OLTP를 지원하지만 지정된 데이터베이스의 메모리 최적화 테이블에 사용할 수 있는 메모리의 양에 할당량을 적용합니다. Standard edition에서는 데이터베이스당 32GB이고, Express edition에서는 데이터베이스당 352MB입니다. 
  
-   메모리 최적화 테이블로 하나 이상의 데이터베이스를 만들 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 계정에 *SE_MANAGE_VOLUME_NAME* 사용자 권한을 부여하여 인스턴트 파일 초기화(IFI)를 사용해야 합니다. IFI를 사용하지 않을 경우 메모리 최적화 저장소 파일(데이터 및 델타 파일)이 생성될 때 초기화되므로 작업 성능이 저하될 수 있습니다. IFI 및 사용 방법에 대한 자세한 내용은 [데이터베이스 즉시 파일 초기화](../../relational-databases/databases/database-instant-file-initialization.md)를 참조하세요.
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
 [데이터베이스 즉시 파일 초기화](../../relational-databases/databases/database-instant-file-initialization.md)  
 [메모리 아키텍처 가이드](../../relational-databases/memory-management-architecture-guide.md)
  
