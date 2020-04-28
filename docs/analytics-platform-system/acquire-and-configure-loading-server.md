---
title: 서버 로드를 가져오는 & 구성
description: 이 문서에서는 PDW (병렬 데이터 웨어하우스)에 데이터 로드를 전송 하기 위한 비 어플라이언스 Windows 시스템으로 로드 서버를 획득 하 고 구성 하는 방법을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ef49bb86c8e16600f2ff1bf2d1c7a92ecc5af964
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401483"
---
# <a name="acquire-and-configure-a-loading-server-for-parallel-data-warehouse"></a>병렬 데이터 웨어하우스를 위한 로드 서버 획득 및 구성
이 문서에서는 PDW (병렬 데이터 웨어하우스)에 데이터 로드를 전송 하기 위한 비 어플라이언스 Windows 시스템으로 로드 서버를 획득 하 고 구성 하는 방법을 설명 합니다.  
  
## <a name="basics"></a><a name="Basics"></a>기본 사항  
로드 서버:  
  
-   단일 서버가 될 필요는 없습니다. 여러 로드 서버를 사용 하 여 동시에 로드할 수 있습니다.  
  
-   사용자 고유의 IT 팀에서 제공 하 고 관리 합니다. PDW로 데이터를 로드 하는 데 사용할 수 있는 서버 또는 서버가 이미 있을 수 있습니다.  
  
-   은 (는) 사용자 고유의 비 어플라이언스 랙에 있으며 분석 플랫폼 시스템 어플라이언스 내에 배치할 수 없습니다.  
  
-   는 어플라이언스 InfiniBand 네트워크를 통해 또는 이더넷을 통해 어플라이언스에 연결 됩니다. 성능을 위해 InfiniBand을 사용 하는 것이 좋습니다.  
  
-   는 어플라이언스 도메인이 아니라 자신의 고객 도메인에 있습니다. 고객 도메인과 어플라이언스 도메인 간에 트러스트 관계가 없습니다.  
  
## <a name="step-1-determine-capacity-requirements"></a><a name="Step1"></a>1 단계: 용량 요구 사항 확인  
로드 시스템은 동시 로드를 수행 하는 하나 이상의 로드 서버로 설계 될 수 있습니다. 각 로드 서버는 워크 로드의 성능 및 저장소 요구 사항을 처리 하는 한 로드 전용으로 지정할 필요가 없습니다.  
  
로드 서버에 대 한 시스템 요구 사항은 전적으로 자신의 작업에 따라 달라 집니다. [서버 용량 로드 계획 워크시트](loading-server-capacity-planning-worksheet.md) 를 사용 하 여 용량 요구 사항을 확인 합니다.  
  
## <a name="step-2-acquire-the-sserver"></a><a name="Step2"></a>2 단계: sServer 얻기  
이제 용량 요구 사항을 더 잘 이해 했으므로 구매 하거나 프로 비전 하는 데 필요한 서버 및 네트워킹 구성 요소를 계획할 수 있습니다. 다음 요구 사항 목록을 구매 계획에 포함 한 다음 서버를 구입 하거나 기존 서버를 프로 비전 합니다.  
  
### <a name="software-requirements"></a><a name="R"></a>소프트웨어 요구 사항  
지원되는 운영 체제:  
  
-   Windows Server 2012 또는 Windows Server 2012 R2. 이러한 운영 체제에는 FDR 네트워크 어댑터가 필요 합니다.  
  
-   Windows Server 2008 R2. 이 OS에는 DDR 네트워크 어댑터가 필요 합니다.  
  
Dwloader 명령줄 로드 도구를 사용 하려면 서버에서 EN-US 로캘을 사용 해야 합니다. dwloader는 다른 로캘을 지원 하지 않습니다.  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Windows Server 2012 및 Windows Server 2012 r 2에 대 한 네트워킹 요구 사항  
로드에는 필요 하지 않지만 InfiniBand는 서버를 로드 하는 데 권장 되는 연결 형식입니다. 최상의 성능을 위해 Windows Server 2012 또는 Windows Server 2012 R2 및 FDR InfiniBand 네트워크 어댑터를 사용 하 여 로드 하는 서버를 어플라이언스 InfiniBand 네트워크에 연결 합니다.  
  
Windows Server 2012 또는 Windows Server 2012 R2 InfiniBand 연결을 준비 하려면 다음을 수행 합니다.  
  
1.  어플라이언스 InfiniBand 스위치에 연결할 수 있도록 서버를 어플라이언스에 충분히 가깝게 랙을 계획 합니다. InfiniBand에 대 한 Mellanox 기술에 대 한 자세한 내용은 [InfiniBand 소개](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf)백서를 참조 하십시오.  
  
2.  Mellanox Connectx-3 FDR InfiniBand 단일 또는 이중 포트 네트워크 어댑터를 구매 합니다. 데이터를 전송 하는 동안 내결함성을 위해 두 개의 포트를 사용 하 여 네트워크 어댑터를 구매 하는 것이 좋습니다. 고가용성을 위해서는 두 개의 포트 네트워크 어댑터가 필요 합니다.  
  
3.  이중 포트 카드의 경우 2 개의 FDR InfiniBand 케이블을 구매 하거나 단일 포트 카드의 경우 1 개의 FDR InfiniBand 케이블을 구매 합니다. FDR InfiniBand 케이블은 로드 서버를 어플라이언스 InfiniBand 네트워크에 연결 합니다. 케이블 길이는 사용자 환경에 따라 로딩 서버와 어플라이언스 InfiniBand 스위치 간의 거리에 따라 달라 집니다.  
  
## <a name="step-3-connect-the-server-to-the-infiniband-networks"></a><a name="Step3"></a>3 단계: InfiniBand 네트워크에 서버 연결  
다음 단계를 사용 하 여 로딩 서버를 InfiniBand 네트워크에 연결 합니다. 서버에서 InfiniBand 네트워크를 사용 하지 않는 경우이 단계를 건너뜁니다.  
  
1.  기기 InfiniBand 네트워크에 연결할 수 있도록 서버를 어플라이언스에 충분히 가깝게 랙 합니다.  
  
2.  로드 서버에 InfiniBand Mellanox Connectx-3-3 FDR InfiniBand 네트워크 어댑터를 설치 합니다.  
  
3.  FDR 케이블을 사용 하 여 첫 번째 어플라이언스 랙의 두 InfiniBand 스위치 중 하나에 InfiniBand 네트워크 어댑터를 연결 합니다.  
  
4.  InfiniBand 네트워크 어댑터용으로 적절 한 Windows 드라이버를 설치 하 고 구성 합니다.  
  
    -   Windows 용 InfiniBand 드라이버는 InfiniBand 공급 업체의 업계 컨소시엄의 OpenFabrics 동맹에 의해 개발 되었습니다.  올바른 드라이버가 InfiniBand 네트워크 어댑터와 함께 배포 되었을 수 있습니다. 그렇지 않은 경우 www.openfabrics.org에서 드라이버를 다운로드할 수 있습니다.  
  
5.  네트워크 어댑터에 대 한 InfiniBand 및 DNS 설정을 구성 합니다. 구성 지침은 [InfiniBand 네트워크 어댑터 구성](configure-infiniband-network-adapters.md)을 참조 하세요.  
  
## <a name="step-4-install-the-loading-tools"></a><a name="Step4"></a>4 단계: 로드 도구 설치  
클라이언트 도구는 Microsoft 다운로드 센터에서 다운로드할 수 있습니다. 

Dwloader를 설치 하려면 클라이언트 도구에서 dwloader 설치를 실행 합니다.
  
Integration Services를 로드 하는 데 사용할 계획인 경우 Integration Services 및 Integration Services 대상 어댑터를 설치 해야 합니다. 어댑터는 클라이언트 도구에서 사용할 수 있습니다.

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="step-5-start-loading"></a><a name="Step5"></a>5 단계: 로드 시작  
이제 데이터 로드를 시작할 준비가 되었습니다. 자세한 내용은 다음을 참조하세요.  
  
1.  [dwloader 명령줄 로드 도구](dwloader.md)  
  
2.  [로드 개요](load-overview.md)  
  
## <a name="performance"></a>성능  
Windows Server 2012 이상에서 최적의 로드 성능을 위해 데이터를 덮어쓸 때 운영 체제가 기존 데이터를 0으로 덮어쓰지 않도록 즉시 파일 초기화를 설정 합니다. 이전 데이터가 디스크에 존재 하기 때문에 보안상 위험할 수 있는 경우 즉시 파일 초기화를 해제 해야 합니다.  
  
## <a name="security-notices"></a><a name="Security"></a>보안 알림  
로드할 데이터가 어플라이언스에 저장 되지 않으므로 IT 팀은 데이터를 로드 하기 위한 보안의 모든 측면을 관리 하는 일을 담당 합니다. 예를 들어 로드할 데이터의 보안, 로드를 저장 하는 데 사용 되는 서버의 보안 및 로드 서버를 SQL Server PDW 어플라이언스에 연결 하는 네트워킹 인프라의 보안을 관리 하는 작업이 포함 됩니다.  
  
> [!IMPORTANT]  
> Dwloader 명령줄 로드 도구를 사용 하는 각 로드 서버를 보호 하는 것이 특히 중요 합니다. Dwloader는 데이터를 로드할 때 먼저 Control 노드를 사용 하 여 인증 한 후 인증에 성공 하면 데이터를 로드 하는 서버에서 데이터 채널을 통해 계산 노드로 직접 이동 합니다. 각 로딩 서버와 각 계산 노드 간의 손을 흔들기 중에는 인증서 유효성 검사가 수행 되지 않습니다. 이를 통해 계산 노드는 로드 하는 동안 각 데이터 채널에 대 한 잠재적 메시지 가로채기 (man-in-the-middle) 공격에 노출 됩니다. 이러한 공격으로 인해 데이터가 손상 되거나 정보가 공개 될 수 있습니다.  
  
데이터의 보안 위험을 줄이려면 다음을 권장 합니다.  
  
-   PDW로 데이터를 로드 하는 용도로만 사용 되는 Windows 계정을 하나 지정 합니다. 이 계정에 로드 위치에 대 한 사용 권한을 부여 하 고 다른 곳에서는 사용 하지 않습니다.  
  
-   데이터를 로드할 수 있는 권한이 있는 하나의 PDW 사용자를 지정 합니다. 보안 요구 사항에 따라 데이터베이스당 하나의 특정 사용자가 있을 수 있습니다.  
  
-   로드 서버에 대 한 작업은 신뢰할 수 있는 내부 네트워크 외부에서 데이터를 끌어오는 UNC 경로를 사용할 수 있습니다. 그리고 네트워크 상의 공격자 또는 이름 확인에 영향을 주는 기능으로 인해 SQL Server PDW 전송 된 데이터를 가로채 거 나 수정할 수 있습니다. 이로 인해 변조 및 정보 유출 위험이 발생 합니다. 연결에 대 한 로그인을 요구 하 여 변조를 완화 해야 합니다. 이러한 위험을 완화 하려면 로드 서버에서 보안 설정 \ 로컬 정책 \ **보안 옵션** 의 다음 그룹 정책 옵션을 설정 합니다. **Microsoft 네트워크 클라이언트: 디지털 서명 통신 (항상): 사용**  
  
-   Windows Server 2012 이상에서 즉시 파일 초기화를 해제 합니다. 성능 섹션에 명시 된 대로 성능 및 보안 간의 균형을 유지 하는 것입니다. 보안 요구 사항에 따라 가장 적합 한 항목을 결정 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
[백업 및 복원 개요](backup-and-restore-overview.md)  
  
