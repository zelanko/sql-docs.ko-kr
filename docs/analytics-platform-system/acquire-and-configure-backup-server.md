---
title: 획득 및 병렬 데이터 웨어하우스 백업 서버-구성 | Microsoft Docs
description: 이 문서에서는 Analytics Platform System (APS) 및 병렬 데이터 웨어하우스 (PDW)의 백업 및 복원 기능을 사용 하 여 백업 서버로 비 어플라이언스 Windows 시스템을 구성 하는 방법을 설명 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: cba345eb7a5aec9ef857819a1f0499266649f6e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63040829"
---
# <a name="acquire-and-configure-a-backup-server-for-parallel-data-warehouse"></a>획득 및 Parallel Data Warehouse에 대 한 백업 서버 구성
이 문서에서는 Analytics Platform System (APS) 및 병렬 데이터 웨어하우스 (PDW)의 백업 및 복원 기능을 사용 하 여 백업 서버로 비 어플라이언스 Windows 시스템을 구성 하는 방법을 설명 합니다.  
  
  
## <a name="Basics"></a>백업 서버 기본 사항  
백업 서버:  
  
-   제공 되 고 고유한 IT 팀에서 관리 됩니다.  
  
-   PDW-특정 소프트웨어 또는 도구는 필요 하지 않습니다. PDW 백업 서버에 소프트웨어를 설치 하지 않습니다.  
  
-   사용자 고유의 비 어플라이언스 랙에 있는 및 APS 어플라이언스 안에 사용할 수 없습니다.  
  
-   어플라이언스 InfiniBand 네트워크에 연결할 수 있습니다. 백업은; 이더넷 또는 InfiniBand를 통해 수행할 수 있습니다. 성능상의 이유로 InfiniBand는 사용 하는 것이 좋습니다.  
  
-   어플라이언스 도메인이 아닌 자신의 고객 도메인입니다. 고객 도메인 및 어플라이언스 도메인 간의 트러스트 관계가 없습니다.  
  
-   서버 메시지 블록 (SMB) 응용 프로그램 수준 네트워크 프로토콜을 사용 하는 Windows 파일 공유는 백업 파일 공유를 호스트 합니다. 백업 파일 공유 사용 권한 (일반적으로 전용된 백업 사용자는) Windows 도메인 사용자에 게 백업 및 복원 작업에서 공유 하는 기능입니다. Windows 도메인 사용자의 사용자 이름 및 암호 자격 증명은 PDW에서 백업을 수행 하 고 백업 파일 공유에 대 한 작업을 복원할 수 있도록 PDW에 저장 됩니다.  
  
## <a name="Step1"></a>1 단계: 용량 요구 사항 확인  
Backup server의 시스템 요구 사항을 고유한 워크 로드에 따라 거의 완전히 달라 집니다. 구매 하거나 백업 서버를 프로 비전 하기 전에 용량 요구 사항을 파악 해야 합니다. Backup server 워크 로드의 성능 및 저장소 요구를 처리할 것으로 백업에만 전용 되도록 없습니다. 백업 및 여러 서버 중 하나에 각 데이터베이스를 복원 하기 위해 여러 백업 서버 할 수도 있습니다.  
  
사용 합니다 [백업 서버 용량 계획 워크시트](backup-capacity-planning-worksheet.md) 용량 요구 사항을 확인할 수 있습니다.  
  
## <a name="Step2"></a>2 단계: 백업 서버 획득  
용량 요구 사항을 이해 했으므로 서버 및을 구입 하거나 프로 비전 해야 하는 네트워킹 구성 요소를 계획할 수 있습니다. 다음과 같은 요구 사항 구매 계획을 통합할 서버를 구입 하거나 기존 서버를 프로 비전 합니다.  
  
### <a name="software-requirements"></a>소프트웨어 요구 사항  
Windows 파일 공유 (SMB) 프로토콜을 사용 하는 모든 파일 서버입니다.  
  
Windows Server 2012 권장 또는를 순서 대로 이상:  
  
-   SMB를 통한 사전 할당 파일의 성능 이점을 얻을 수 있습니다.  
  
-   백업 작업에 대 한 인스턴트 파일 초기화 (IFI)를 사용 합니다. IT 팀에는 백업 서버에서이 설정을 관리합니다. PDW 구성 관리자 (dwconfig.exe) 설정 하지 않거나 백업 서버의 IFI를 제어 합니다. 이전 버전 Windows의 IFI를 없지만 백업 서버로 계속 사용할 수 있습니다.  
  
### <a name="networking-requirements"></a>네트워킹 요구 사항  
필요 하지는 않지만 InfiniBand Backup server에 대 한 권장 되는 연결 유형입니다. 로드 서버 어플라이언스의 InfiniBand 네트워크에 연결 하기 위한 준비:  
  
1.  서버 랙 하려면 가까이에 어플라이언스 InfiniBand 전환 어플라이언스에 연결할 수 있도록 합니다. Mellanox 기술에서 대 한 자세한 내용은 InfiniBand 백서를 참조 하세요 [InfiniBand 소개](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf)합니다.  
  
2.  단일 또는 이중 포트 Mellanox connectx-3 FDR InfiniBand 네트워크 어댑터를 구입 합니다. 데이터 전송 중 내결함성에 대 한 두 개의 포트를 사용 하 여 네트워크 어댑터를 구입 하는 것이 좋습니다. 두 포트 네트워크 어댑터는 고가용성을 위해 필요 합니다.  
  
3.  이중 포트 카드에 대 한 FDR InfiniBand 케이블 2 개 또는 단일 포트 카드에 대 한 1 FDR InfiniBand 케이블을 구입 합니다. FDR InfiniBand 케이블 어플라이언스의 InfiniBand 네트워크에 로드 서버를 연결 됩니다. 케이블 길이 사용자 환경에 따라 로드 서버와 어플라이언스 InfiniBand 스위치 간의 거리에 따라 달라 집니다.  
  
## <a name="Step3"></a>3 단계: InfiniBand 네트워크에 서버를 연결 합니다.  
로드 서버 InfiniBand 네트워크를 연결 하려면 다음이 단계를 사용 합니다. 서버 InfiniBand 네트워크에 사용 하지 않는 경우이 단계를 건너뜁니다.  
  
1.  어플라이언스 InfiniBand 네트워크에 연결할 수 있도록 서버 랙 어플라이언스로 닫을 합니다.  
  
2.  서버 로드에 InfiniBand Mellanox connectx-3 FDR InfiniBand 네트워크 어댑터를 설치 합니다.  
  
3.  첫 번째 어플라이언스 랙에 두 InfiniBand 스위치 중 하나에 InfiniBand 네트워크 어댑터를 연결할 FDR 케이블을 사용 합니다.  
  
4.  설치 하 고 InfiniBand 네트워크 어댑터에 대 한 적절 한 Windows 드라이버를 구성 합니다.  
  
    -   Windows에 대 한 infiniband InfiniBand 공급 업체의 업계 컨소시엄 OpenFabrics Alliance에서 개발 됩니다.  올바른 드라이버 InfiniBand 네트워크 어댑터를 사용 하 여 배포 될 수 있습니다. 그렇지 않은 경우 www.openfabrics.org 에서 드라이버를 다운로드할 수 있습니다.  
  
5.  네트워크 어댑터에 대 한 InfiniBand 및 DNS 설정을 구성 합니다. 구성 지침을 참조 하세요 [InfiniBand 네트워크 어댑터 구성](configure-infiniband-network-adapters.md)합니다.  
  
## <a name="Step4"></a>4 단계: 백업 파일 공유를 구성 합니다.  
PDW는 UNC 파일 공유를 통해 백업 서버에 액세스 합니다. 파일 공유를 설정 하려면:  
  
1.  백업을 저장할 백업 서버에서 폴더를 만듭니다.  
  
2.  백업 공유를 백업 폴더 용 라는 파일 공유를 만듭니다.  
  
3.  지정 하거나 백업 및 복원을 수행 하는 용도로 사용 하려는 고객 도메인에 Windows 도메인 계정을 만듭니다. 보안상의 이유로 백업 사용자로 전용된 계정을 사용 하는 것이 적합 합니다.  
  
4.  백업에 대 한 사용 권한 읽기, 신뢰할 수 있는 계정 및 도메인 백업 계정에 액세스할 수 있도록 공유 및 공유 위치에 쓰기를 추가 합니다.  
  
5.  PDW에 백업 도메인 계정 자격 증명을 추가 합니다.  
  
    이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    자세한 내용은 이러한 저장된 프로시저를 참조 하세요.  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="Step5"></a>5 단계: 데이터 백업 시작  
이제 백업 서버로 데이터를 백업 시작할 준비가 되었습니다.  
  
백업 데이터, 쿼리 클라이언트를 사용 하 여 SQL Server PDW에 연결한 후 백업 또는 복원할 데이터베이스를 제출 하는 명령입니다. 디스크를 사용 하 여 백업 서버 및 백업 위치를 지정 하는 절 =.  
  
> [!IMPORTANT]  
> Backup server의 InfiniBand IP 주소를 사용 해야 합니다. 그렇지 않으면 데이터 InfiniBand 대신 이더넷을 통해 복사 됩니다.  
  
이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full';  
  
RESTORE DATABASE Invoices2013Full  
FROM DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full'  
```  
  
참조 항목: 
  
-   [데이터베이스 백업](../t-sql/statements/backup-database-parallel-data-warehouse.md)   
  
-   [데이터베이스 복원](../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
## <a name="Security"></a>보안 알림  
백업 서버 어플라이언스에 대 한 개인 도메인에 연결 되지 않았습니다. 사용자 고유의 네트워크에서 이므로 고유한 도메인 및 개인 기기 도메인 간에 트러스트 관계가 없습니다.  
  
PDW 백업이 어플라이언스에 저장 되어 있지 하므로 IT 팀은 백업 보안의 모든 측면을 관리 하는 일을 담당 합니다. 예를 들어, 백업 데이터, 백업을 저장 하는 데 서버의 보안 및 APS 어플라이언스로 백업 서버를 연결 하는 네트워킹 인프라의 보안의 보안을 관리 하는 것이 여기 있습니다.  
  
### <a name="manage-network-credentials"></a>네트워크 자격 증명 관리  
  
백업 디렉터리에 대한 네트워크 액세스는 표준 Windows 파일 공유 보안을 기반으로 합니다. 백업을 수행 하기 전에 백업 디렉터리에 PDW를 인증 하기 위해 사용할 Windows 계정을 만들거나 지정 해야 합니다. 이 Windows 계정에는 백업 디렉토리에 액세스, 작성 및 쓰기할 수 있는 권한이 있어야 합니다.  
  
> [!IMPORTANT]  
> 데이터의 보안 위험을 줄이려면 Windows 계정 하나를 전적으로 백업 및 복원 작업을 수행할 목적으로 지정하는 것이 좋습니다. 이 계정에 전적으로 백업 위치에 대해서만 권한을 갖도록 허용합니다.  
  
PDW에 사용자 이름 및 암호를 저장 하려면 사용 합니다 [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 저장 프로시저입니다. PDW는 Windows 자격 증명 관리자를 사용 하 여 저장 및 제어 노드에 사용자 이름 및 암호를 암호화 하 고 계산 노드. 자격 증명은 BACKUP DATABASE 명령으로 백업되지 않습니다.  
  
PDW에서 네트워크 자격 증명을 제거 하려면 사용 합니다 [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md) 저장 프로시저입니다.  
  
모든 SQL Server PDW에 저장 된 네트워크 자격 증명을 나열 하려면 사용 합니다 [sys.dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) 동적 관리 뷰.  
  
### <a name="secure-communications"></a>보안 통신  
  
로드 서버에서 작업에는 신뢰할 수 있는 내부 네트워크 외부 데이터를 UNC 경로 사용 수 있습니다. 공격자가 네트워크 또는 이름 확인에 영향을 줄 수 있는 기능을 사용 하 여 가로채 거 나 PDW로 전송 된 데이터를 수정할 수 있습니다. 이 변조 및 정보 공개 위험을 표시합니다. 변조 위험을 완화 하려면:

- 연결에 서명 해야 합니다. 
- 로드 서버에서 보안 설정 \ 로컬 정책 \ 보안 옵션에 다음 그룹 정책 옵션을 설정 합니다.  Microsoft 네트워크 클라이언트: 디지털 서명 통신 (항상): 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
[백업 및 복원](backup-and-restore-overview.md)  
  
