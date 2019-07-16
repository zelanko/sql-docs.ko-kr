---
title: SQL Server 병렬 데이터 웨어하우스-원격 테이블 복사본을 받도록 구성 | Microsoft Docs
description: 원격 테이블 복사본을 받도록 병렬 데이터 웨어하우스에서 외부 SMP SQL Server 인스턴스를 구성 하는 방법에 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3ad1ee005f5d28e7477fab7c1abe7ed4074e233d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961299"
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies---parallel-data-warehouse"></a>병렬 데이터 웨어하우스-원격 테이블 복사본을 받도록 외부 SMP SQL 서버를 구성 합니다.
원격 테이블 복사본을 받도록 병렬 데이터 웨어하우스에서 외부 SQL Server 인스턴스를 구성 하는 방법에 설명 합니다.  

이 항목에서는 원격 테이블 복사본을 구성 하기 위한 구성 단계 중 하나를 설명 합니다. 목록은 모든 구성 단계를 참조 하세요 [원격 테이블 복사](remote-table-copy.md)합니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
외부 SQL Server를 구성 하려면 다음을 수행 해야 합니다.  
  
-   SQL Server 2008 Enterprise Edition 또는 이후 버전을 설치 하거나 이미 설치 되어 준비를 사용 하 여 Windows 시스템을가지고 있습니다. Windows 시스템의 지침에 따라 이미 구성 해야 합니다 [는 외부 Windows 시스템에 수신 원격 테이블 복사를 사용 하 여 InfiniBand 구성](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)합니다.  
  
-   SQL Server 인스턴스 및 Windows 시스템을 구성 하는 기능을 사용 하 여 Windows 관리자 계정입니다.  
  
-   SQL Server 로그인 계정 (SQL Server가 이미 설치 된 경우) 로그인을 만들고 대상 데이터베이스에 대 한 권한을 부여 하는 기능입니다.  
  
## <a name="HowToSQLServer"></a>원격 테이블 복사본을 받도록 외부 SMP SQL 서버 구성  
원격 테이블 복사 기능은 Windows 시스템에서 실행 되는 외부 SMP SQL Server 데이터베이스에 SQL Server PDW appliance에서 테이블을 복사 합니다. 원격 테이블 복사본을 받도록 외부 Windows 시스템을 구성한 후 다음 단계를 설치 하 여 Windows 시스템에 SQL Server 구성입니다.  
  
SQL Server를 구성 하려면 다음 단계를 사용 합니다.  
  
1.  Windows 시스템에서 SQL Server 2008 Enterprise Edition 또는 이후 버전을 설치 합니다. 이 SMP SQL Server 라고 합니다.  
  
2.  고정된 TCP 포트에서 TCP/IP 연결을 허용 하도록 SQL Server를 구성 합니다. 이 구성은 기본적으로 비활성화 되 고 SQL Server PDW SMP SQL Server에 연결할 수 있도록 설정 해야 합니다.  
  
3.  Windows 방화벽을 사용 하지 않도록 설정 하거나 Windows 방화벽이 설정 되어 작동할 수 있도록 SMP SQL Server TCP 포트를 구성 하십시오.  
  
4.  SQL Server 인증 모드를 허용 하도록 SQL Server를 구성 합니다. 병렬 데이터 내보내기 항상 인증에 대 한 SQL Server 계정을 사용 합니다.  
  
5.  인증에 사용할 SMP SQL Server에서 SQL Server 계정을 결정 합니다. 만들기, 삭제 및 병렬 데이터 내보내기 작업에 대 한 대상 데이터베이스에서 테이블 데이터를 삽입할 수 있는 권한을 해당 계정에 부여 합니다.  
  
## <a name="BPSQLConfig"></a>원격 테이블 복사본에 대 한 SMP SQL Server 구성에 대 한 모범 사례  
원격 테이블 복사본을 받도록 SMP SQL Server를 구성할 때 성능을 향상 시키려면 다음 모범 사례를 사용 합니다.  
  
1.  SQL Server 제품 설명서에 설명 된 대로 모범 사례를 따릅니다. 예를 들어, 데이터 암호화를 사용 하도록 설정 합니다. SQL Server 보안 설정에 대 한 자세한 내용은 참조 하세요. [Securing SQL Server](../relational-databases/security/securing-sql-server.md) MSDN에 있습니다.  
  
2.  대량 로그 또는 단순 복구 모델을 사용 합니다.  
  
    내보내기 작업 중 병렬 데이터, 데이터를 대량으로 새로 만든된 대상 테이블에 삽입 합니다. 대량 삽입 하는 동안 최상의 성능을 위해 대상 데이터베이스를 사용 하 여 대량 로그 또는 단순 복구 모델을 설정 합니다.  
  
3.  로그 공간을 확보 하려면 batch_size 옵션을 사용 합니다.  
  
    대량 로그 또는 단순 복구 모델을 사용 하 여 대량 삽입 데이터에 대 한 로깅을 최소화, 하지만 일부 로깅 여전히 발생 합니다. 로그 파일이 너무 많이 늘어나서을 방지 하려면 정기적으로 로그 공간을 확보 하려면 SQL Server batch_size 옵션을 사용 합니다.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
