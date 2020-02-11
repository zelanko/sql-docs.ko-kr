---
title: 백업 서버 가져오기 & 구성
description: 이 문서에서는 비 어플라이언스 Windows 시스템을 AP (Analytics Platform System) 및 PDW (병렬 데이터 웨어하우스)의 백업 및 복원 기능과 함께 사용할 백업 서버로 구성 하는 방법을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e160c606b19933934ec844b477ffec08475307d8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401491"
---
# <a name="acquire-and-configure-a-backup-server-for-parallel-data-warehouse"></a>병렬 데이터 웨어하우스의 백업 서버 가져오기 및 구성
이 문서에서는 비 어플라이언스 Windows 시스템을 AP (Analytics Platform System) 및 PDW (병렬 데이터 웨어하우스)의 백업 및 복원 기능과 함께 사용할 백업 서버로 구성 하는 방법을 설명 합니다.  
  
  
## <a name="Basics"></a>Backup server 기본 사항  
백업 서버:  
  
-   사용자 고유의 IT 팀에서 제공 하 고 관리 합니다.  
  
-   PDW 관련 소프트웨어나 도구를 요구 하지 않습니다. PDW는 백업 서버에 소프트웨어를 설치 하지 않습니다.  
  
-   은 (는) 사용자 고유의 어플라이언스 랙에 있으며 APS 어플라이언스 내에 배치할 수 없습니다.  
  
-   어플라이언스 InfiniBand 네트워크에 연결할 수 있습니다. InfiniBand 또는 Ethernet을 통해 백업을 수행할 수 있습니다. InfiniBand는 성능상의 이유로 권장 됩니다.  
  
-   는 어플라이언스 도메인이 아니라 자신의 고객 도메인에 있습니다. 고객 도메인과 어플라이언스 도메인 간에 트러스트 관계가 없습니다.  
  
-   SMB (서버 메시지 블록) 응용 프로그램 수준 네트워크 프로토콜을 사용 하는 Windows 파일 공유 인 백업 파일 공유를 호스팅합니다. 백업 파일 공유 권한은 공유에서 백업 및 복원 작업을 수행 하는 기능을 Windows 도메인 사용자 (일반적으로 전용 백업 사용자)에 게 제공 합니다. PDW가 백업 파일 공유에 대 한 백업 및 복원 작업을 수행할 수 있도록 Windows 도메인 사용자의 사용자 이름 및 암호 자격 증명은 PDW에 저장 됩니다.  
  
## <a name="Step1"></a>1 단계: 용량 요구 사항 확인  
백업 서버에 대 한 시스템 요구 사항은 전적으로 자신의 작업에 따라 달라 집니다. 백업 서버를 구매 하거나 프로 비전 하기 전에 용량 요구 사항을 파악 해야 합니다. 백업 서버는 워크 로드의 성능 및 저장소 요구 사항을 처리 하는 한 백업 전용으로 지정할 필요가 없습니다. 여러 서버 중 하나로 각 데이터베이스를 백업 및 복원 하기 위해 여러 백업 서버를 사용할 수도 있습니다.  
  
[백업 서버 용량 계획 워크시트](backup-capacity-planning-worksheet.md) 를 사용 하 여 용량 요구 사항을 결정할 수 있습니다.  
  
## <a name="Step2"></a>2 단계: 백업 서버 가져오기  
이제 용량 요구 사항을 더 잘 이해 했으므로 구매 하거나 프로 비전 하는 데 필요한 서버 및 네트워킹 구성 요소를 계획할 수 있습니다. 다음 요구 사항 목록을 구매 계획에 포함 한 다음 서버를 구입 하거나 기존 서버를 프로 비전 합니다.  
  
### <a name="software-requirements"></a>소프트웨어 요구 사항  
Windows 파일 공유 (SMB) 프로토콜을 사용 하는 파일 서버  
  
다음을 수행 하기 위해 Windows Server 2012 이상을 권장 합니다.  
  
-   SMB를 통한 파일 사전 할당의 성능 혜택을 얻습니다.  
  
-   백업 작업에는 IFI (인스턴트 파일 초기화)를 사용 합니다. IT 팀은 백업 서버에서이 설정을 관리 합니다. PDW Configuration Manager (dwconfig .exe)는 백업 서버에서 IFI를 설정 하거나 제어 하지 않습니다. 이전 버전의 Windows는 IFI를 갖지 않지만 여전히 백업 서버로 사용할 수 있습니다.  
  
### <a name="networking-requirements"></a>네트워킹 요구 사항  
필수는 아니지만 InfiniBand은 백업 서버에 권장 되는 연결 형식입니다. 기기 InfiniBand 네트워크에 로드 서버를 연결 하기 위해 준비 하려면:  
  
1.  어플라이언스 InfiniBand 스위치에 연결할 수 있도록 서버를 어플라이언스에 충분히 가깝게 랙을 계획 합니다. InfiniBand에 대 한 Mellanox 기술에 대 한 자세한 내용은 [InfiniBand 소개](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf)백서를 참조 하십시오.  
  
2.  Mellanox Connectx-3 FDR InfiniBand 단일 또는 이중 포트 네트워크 어댑터를 구매 합니다. 데이터를 전송 하는 동안 내결함성을 위해 두 개의 포트를 사용 하 여 네트워크 어댑터를 구매 하는 것이 좋습니다. 고가용성을 위해서는 두 개의 포트 네트워크 어댑터가 필요 합니다.  
  
3.  이중 포트 카드의 경우 2 개의 FDR InfiniBand 케이블을 구매 하거나 단일 포트 카드의 경우 1 개의 FDR InfiniBand 케이블을 구매 합니다. FDR InfiniBand 케이블은 로드 서버를 어플라이언스 InfiniBand 네트워크에 연결 합니다. 케이블 길이는 사용자 환경에 따라 로딩 서버와 어플라이언스 InfiniBand 스위치 간의 거리에 따라 달라 집니다.  
  
## <a name="Step3"></a>3 단계: InfiniBand 네트워크에 서버 연결  
다음 단계를 사용 하 여 로딩 서버를 InfiniBand 네트워크에 연결 합니다. 서버에서 InfiniBand 네트워크를 사용 하지 않는 경우이 단계를 건너뜁니다.  
  
1.  기기 InfiniBand 네트워크에 연결할 수 있도록 서버를 어플라이언스에 충분히 가깝게 랙 합니다.  
  
2.  로드 서버에 InfiniBand Mellanox Connectx-3-3 FDR InfiniBand 네트워크 어댑터를 설치 합니다.  
  
3.  FDR 케이블을 사용 하 여 첫 번째 어플라이언스 랙의 두 InfiniBand 스위치 중 하나에 InfiniBand 네트워크 어댑터를 연결 합니다.  
  
4.  InfiniBand 네트워크 어댑터용으로 적절 한 Windows 드라이버를 설치 하 고 구성 합니다.  
  
    -   Windows 용 InfiniBand 드라이버는 InfiniBand 공급 업체의 업계 컨소시엄의 OpenFabrics 동맹에 의해 개발 되었습니다.  올바른 드라이버가 InfiniBand 네트워크 어댑터와 함께 배포 되었을 수 있습니다. 그렇지 않은 경우 www.openfabrics.org에서 드라이버를 다운로드할 수 있습니다.  
  
5.  네트워크 어댑터에 대 한 InfiniBand 및 DNS 설정을 구성 합니다. 구성 지침은 [InfiniBand 네트워크 어댑터 구성](configure-infiniband-network-adapters.md)을 참조 하세요.  
  
## <a name="Step4"></a>4 단계: 백업 파일 공유 구성  
PDW는 UNC 파일 공유를 통해 백업 서버에 액세스 합니다. 파일 공유를 설정 하려면:  
  
1.  백업 서버에 백업을 저장 하기 위한 폴더를 만듭니다.  
  
2.  백업 폴더에 대 한 백업 공유 라는 파일 공유를 만듭니다.  
  
3.  백업 및 복원을 수행 하기 위해 사용 하려는 고객 도메인에 Windows 도메인 계정을 지정 하거나 만듭니다. 보안상의 이유로, 전용 계정을 백업 사용자로 사용 하는 것이 가장 좋습니다.  
  
4.  트러스트 된 계정 및 도메인 백업 계정만 공유 위치에 액세스 하 고 읽고 쓸 수 있도록 백업 공유에 사용 권한을 추가 합니다.  
  
5.  PDW에 백업 도메인 계정 자격 증명을 추가 합니다.  
  
    다음은 그 예입니다.  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    자세한 내용은 다음 저장 프로시저를 참조 하세요.  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="Step5"></a>5 단계: 데이터 백업 시작  
이제 백업 서버에 데이터를 백업 하는 작업을 시작할 준비가 되었습니다.  
  
데이터를 백업 하려면 쿼리 클라이언트를 사용 하 SQL Server PDW에 연결한 다음 백업 데이터베이스를 제출 하거나 데이터베이스 명령을 복원 합니다. DISK = 절을 사용 하 여 백업 서버와 백업 위치를 지정 합니다.  
  
> [!IMPORTANT]  
> 백업 서버의 InfiniBand IP 주소를 사용 해야 합니다. 그렇지 않으면 데이터가 InfiniBand 대신 이더넷을 통해 복사 됩니다.  
  
다음은 그 예입니다.  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full';  
  
RESTORE DATABASE Invoices2013Full  
FROM DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full'  
```  
  
자세한 내용은 다음을 참조하세요. 
  
-   [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)   
  
-   [RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
## <a name="Security"></a>보안 알림  
백업 서버가 어플라이언스의 개인 도메인에 가입 되어 있지 않습니다. 사용자의 네트워크에 있으며 사용자의 도메인과 개인 어플라이언스 도메인 간에 트러스트 관계가 없습니다.  
  
PDW 백업은 어플라이언스에 저장 되지 않으므로 IT 팀은 백업 보안의 모든 측면을 관리 하는 일을 담당 합니다. 예를 들어 여기에는 백업 데이터의 보안, 백업을 저장 하는 데 사용 되는 서버의 보안 및 백업 서버를 APS 어플라이언스에 연결 하는 네트워킹 인프라의 보안 관리가 포함 됩니다.  
  
### <a name="manage-network-credentials"></a>네트워크 자격 증명 관리  
  
백업 디렉터리에 대한 네트워크 액세스는 표준 Windows 파일 공유 보안을 기반으로 합니다. 백업을 수행 하기 전에 백업 디렉터리에 대해 PDW를 인증 하는 데 사용할 Windows 계정을 만들거나 지정 해야 합니다. 이 Windows 계정에는 백업 디렉토리에 액세스, 작성 및 쓰기할 수 있는 권한이 있어야 합니다.  
  
> [!IMPORTANT]  
> 데이터의 보안 위험을 줄이려면 Windows 계정 하나를 전적으로 백업 및 복원 작업을 수행할 목적으로 지정하는 것이 좋습니다. 이 계정에 전적으로 백업 위치에 대해서만 권한을 갖도록 허용합니다.  
  
PDW에 사용자 이름과 암호를 저장 하려면 [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 저장 프로시저를 사용 합니다. PDW는 Windows 자격 증명 관리자를 사용 하 여 사용자 이름 및 암호를 제어 노드와 계산 노드에 저장 하 고 암호화 합니다. 자격 증명은 BACKUP DATABASE 명령으로 백업되지 않습니다.  
  
PDW에서 네트워크 자격 증명을 제거 하려면 [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md) 저장 프로시저를 사용 합니다.  
  
SQL Server PDW에 저장 된 모든 네트워크 자격 증명을 나열 하려면 [dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) 동적 관리 뷰를 사용 합니다.  
  
### <a name="secure-communications"></a>보안 통신  
  
로드 서버에 대 한 작업은 UNC 경로를 사용 하 여 신뢰할 수 있는 내부 네트워크 외부에서 데이터를 가져올 수 있습니다. 네트워크 상의 공격자 또는 이름 확인에 영향을 주는 기능으로 PDW로 전송 된 데이터를 가로채 거 나 수정할 수 있습니다. 이로 인해 변조 및 정보 유출 위험이 발생 합니다. 변조 위험을 완화 하기 위해 다음을 수행 합니다.

- 연결에 대 한 서명이 필요 합니다. 
- 로드 서버에서 보안 설정 \ 로컬 정책 \ 보안 옵션: Microsoft 네트워크 클라이언트: 디지털 서명 통신 (항상): 사용에 다음 그룹 정책 옵션을 설정 합니다.  
  
## <a name="see-also"></a>참고 항목  
[백업 및 복원](backup-and-restore-overview.md)  
  
