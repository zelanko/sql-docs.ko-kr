---
title: 원격 테이블 복사본을 받도록 SQL Server 구성
description: 병렬 데이터 웨어하우스에서 원격 테이블 복사본을 받도록 외부 SMP SQL Server 인스턴스를 구성 하는 방법을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3e5475e86582ede2e6fa7ca5a302bba7ee74faa3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401321"
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies---parallel-data-warehouse"></a>외부 SMP SQL Server 구성 하 여 원격 테이블 복사-병렬 데이터 웨어하우스를 수신 합니다.
병렬 데이터 웨어하우스에서 원격 테이블 복사본을 받도록 외부 SQL Server 인스턴스를 구성 하는 방법을 설명 합니다.  

이 항목에서는 원격 테이블 복사를 구성 하는 구성 단계 중 하나에 대해 설명 합니다. 모든 구성 단계 목록은 [원격 테이블 복사](remote-table-copy.md)를 참조 하세요.  
  
## <a name="before-you-begin"></a>시작하기 전에  
외부 SQL Server를 구성 하려면 먼저 다음을 수행 해야 합니다.  
  
-   SQL Server 2008 Enterprise Edition 이상 버전의 Windows 시스템을 설치 하거나 이미 설치할 준비가 되었습니다. Windows 시스템은 [InfiniBand를 사용 하 여 원격 테이블 복사본을 받도록 외부 Windows 시스템 구성](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)의 지침에 따라 이미 구성 되어 있어야 합니다.  
  
-   SQL Server 인스턴스와 Windows 시스템을 구성할 수 있는 Windows 관리자 계정입니다.  
  
-   로그인을 만들고 대상 데이터베이스에 대 한 사용 권한을 부여할 수 있는 기능을 포함 하는 SQL Server 로그인 계정 (SQL Server 이미 설치 된 경우)  
  
## <a name="HowToSQLServer"></a>원격 테이블 복사본을 받도록 외부 SMP SQL Server 구성  
원격 테이블 복사 기능은 SQL Server PDW 어플라이언스의 테이블을 Windows 시스템에서 실행 되는 외부 SMP SQL Server 데이터베이스로 복사 합니다. 원격 테이블 복사본을 받도록 외부 Windows 시스템을 구성한 후 다음 단계는 Windows 시스템에 SQL Server를 설치 하 고 구성 하는 것입니다.  
  
SQL Server를 구성 하려면 다음 단계를 사용 합니다.  
  
1.  Windows 시스템에 SQL Server 2008 Enterprise Edition 이상 버전을 설치 합니다. 이를 SMP SQL Server 라고 합니다.  
  
2.  고정 TCP 포트에서 TCP/IP 연결을 허용 하도록 SQL Server를 구성 합니다. 이 구성은 기본적으로 사용 하지 않도록 설정 되어 SQL Server PDW SMP SQL Server에 연결할 수 있도록 설정 해야 합니다.  
  
3.  Windows 방화벽을 사용 하지 않도록 설정 하거나 windows 방화벽을 사용 하도록 설정 하 여 작동 하도록 SMP SQL Server TCP 포트를 구성 합니다.  
  
4.  SQL Server 인증 모드를 허용 하도록 SQL Server를 구성 합니다. 병렬 데이터 내보내기는 인증을 위해 항상 SQL Server 계정을 사용 합니다.  
  
5.  인증에 사용 될 SMP SQL Server의 SQL Server 계정을 결정 합니다. 병렬 데이터 내보내기 작업을 위해 대상 데이터베이스의 테이블에 데이터를 만들고, 삭제 하 고, 삽입할 권한을 해당 계정에 부여 합니다.  
  
## <a name="BPSQLConfig"></a>원격 테이블 복사에 대 한 SMP SQL Server 구성 모범 사례  
원격 테이블 복사본을 받도록 SMP SQL Server를 구성 하는 경우 다음 모범 사례를 사용 하 여 성능을 향상 시킵니다.  
  
1.  SQL Server 제품 설명서에 설명 된 대로 모범 사례를 따릅니다. 예를 들어 데이터 암호화를 사용 하도록 설정 합니다. SQL Server 보안에 대 한 자세한 내용은 MSDN의 [SQL Server 보안](../relational-databases/security/securing-sql-server.md) 을 참조 하세요.  
  
2.  대량 로그 또는 단순 복구 모델을 사용 합니다.  
  
    병렬 데이터 내보내기 작업 중에는 새로 만든 대상 테이블에 데이터가 대량으로 삽입 됩니다. 대량 삽입 중에 최대 성능을 위해 대량 로그 또는 단순 복구 모델을 사용 하도록 대상 데이터베이스를 설정 합니다.  
  
3.  Batch_size 옵션을 사용 하 여 로그 공간을 회수할 수 있습니다.  
  
    대량 로그 또는 단순 복구 모델은 대량 삽입 된 데이터에 대해 최소 로깅을 사용 하지만 일부 로깅은 여전히 발생 합니다. 로그 파일이 너무 커지지 않도록 하려면 SQL Server batch_size 옵션을 사용 하 여 로그 공간을 정기적으로 회수 합니다.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
