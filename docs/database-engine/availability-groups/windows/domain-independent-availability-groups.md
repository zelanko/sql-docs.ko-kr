---
title: 도메인 독립 가용성 그룹(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], domain independent
ms.assetid: ''
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0024663d9d16d191338abfa2604e6c969f0d58e5
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52415080"
---
# <a name="domain-independent-availability-groups"></a>도메인 독립 가용성 그룹
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Always On AG(가용성 그룹)에는 기본 WSFC(Windows Server 장애 조치 클러스터)가 필요합니다. Windows Server 2012 R2를 통해 WSFC를 배포하는 경우 노드라고도 하는 WSFC에 참여하는 서버가 반드시 동일한 도메인에 가입되어야 합니다. AD DS(Active Directory Domain Services)에 대한 자세한 내용은 [여기](https://technet.microsoft.com/library/cc759073(v=ws.10).aspx)를 참조하세요.

AD DS 및 WSFC 종속성은 DBM(데이터베이스 미러링) 구성으로 이전에 배포된 것보다 더 복잡합니다. 이는 이러한 종속성 없이 인증서를 사용하여 여러 데이터 센터에 DBM을 배포할 수 있기 때문입니다.  둘 이상의 데이터 센터에 걸쳐 있는 기존 가용성 그룹에서는 모든 서버가 동일한 Active Directory 도메인에 가입되어야 하며, 다른 도메인, 심지어 트러스트된 도메인에서는 작동하지 않아야 합니다. 모든 서버는 동일한 WSFC의 노드 여야 합니다. 다음 그림에서는 이 구성을 보여 줍니다. 또한 SQL Server 2016에는 여러 가지 방식으로 이 목표를 달성할 수 있는 분산 가용성 그룹이 있습니다.


![동일한 도메인에 연결된 두 데이터 센터에 걸쳐 있는 WSFC][1]

Windows Server 2012 R2에서는 가용성 그룹과 함께 사용할 수 있는 특수한 형태의 Windows Server 장애 조치 클러스터인 [Active Directory 분리 클러스터](https://technet.microsoft.com/library/dn265970.aspx)를 도입했습니다. 이 유형의 WSFC에서는 노드가 동일한 Active Directory 도메인에 여전히 가입되어야 하지만, 이 경우 WSFC는 도메인이 아니라 DNS를 사용합니다. 도메인이 여전히 관련되어 있으므로 Active Directory 분리 클러스터에서도 도메인이 전혀 필요하지 않은 환경을 제공하지 않습니다.

Windows Server 2016에서는 Active Directory 분리 클러스터(작업 그룹 클러스터)를 기반으로 하여 새로운 종류의 Windows Server 장애 조치 클러스터를 도입했습니다. 작업 그룹 클러스터를 사용하면 SQL Server 2016에서 AD DS가 필요하지 않은 WSFC에 기반하여 가용성 그룹을 배포할 수 있습니다. SQL Server에서는 데이터베이스 미러링 시나리오에서 인증서가 필요한 것처럼 엔드포인트 보안에 인증서를 사용해야 합니다.  이런 유형의 가용성 그룹을 도메인 독립 가용성 그룹이라고 합니다. 기본 작업 그룹 클러스터가 있는 가용성 그룹을 배포하면 WSFC를 구성할 노드에 대해 다음과 같은 조합을 지원할 수 있습니다.
- 노드가 도메인에 가입되어 있지 않습니다.
- 모든 노드가 서로 다른 도메인에 가입되어 있습니다.
- 노드가 도메인 가입 노드와 비도메인 가입 노드의 조합으로 혼합되어 있습니다.

다음 그림에서는 데이터 센터 1의 노드는 도메인에 가입되어 있지만, 데이터 센터 2의 노드는 DNS만 사용하는 도메인 독립 가용성 그룹의 예를 보여 줍니다. 이 경우 WSFC의 노드가 될 모든 서버에서 DNS 접미사를 설정합니다. 가용성 그룹에 액세스하는 모든 응용 프로그램과 서버는 동일한 DNS 정보를 확인해야 합니다.


![도메인에 가입된 두 개의 노드가 있는 작업 그룹 클러스터][2]

도메인 독립 가용성 그룹은 다중 사이트 또는 재해 복구 시나리오에만 사용되지는 않습니다. 단일 데이터 센터에 배포할 수 있으며, [기본 가용성 그룹](basic-availability-groups-always-on-availability-groups.md)(Standard Edition 가용성 그룹이라고도 함)과 함께 사용하여 그림과 같이 인증서로 데이터베이스 미러링을 사용하여 달성한 것과 비슷한 아키텍처를 제공합니다.


![Standard Edition에서 AG의 상위 수준 보기][3]

도메인 독립 가용성 그룹 배포에는 알려진 몇 가지 주의 사항이 있습니다.
- 쿼럼과 함께 사용할 수 있는 유일한 미러링 모니터 서버 유형은 디스크 및 [클라우드](https://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness)이며, 이는 Windows Server 2016의 새로운 기능입니다. 가용성 그룹에서 공유 디스크를 사용할 가능성이 거의 없으므로 디스크에 문제가 있습니다.
- WSFC의 기본 작업 그룹 클러스터 변형은 PowerShell만 사용하여 만들 수 있는 한편, 장애 조치 클러스터 관리자를 사용하여 관리할 수 있습니다.
- Kerberos가 필요한 경우 Active Directory 도메인에 연결된 표준 WSFC를 배포해야 하며 도메인 독립 가용성 그룹은 아마도 옵션이 아닐 수 있습니다.
- 수신기는 구성할 수 있지만, 사용할 수 있도록 하려면 DNS에 등록해야 합니다. 위에서 설명한 대로 수신기에 대한 Kerberos 지원은 없습니다.
- 도메인이 없거나 함께 작동하도록 구성되어 있지 않을 수 있으므로 SQL Server에 연결하는 응용 프로그램은 주로 SQL Server 인증을 사용해야 합니다. 
- 가용성 그룹 구성에는 인증서가 사용됩니다.

## <a name="set-and-verify-the-dns-suffix-on-all-replica-servers"></a>모든 복제본 서버에서 DNS 접미사 설정 및 확인

공통 DNS 접미사는 도메인 독립 가용성 그룹의 작업 그룹 클러스터에 필요합니다. 가용성 그룹에 대한 복제본을 호스팅할 각 Windows Server에서 DNS 접미사를 설정하고 확인하려면 다음 지침을 따릅니다.

1. Windows 키 + X 바로 가기를 사용하여 시스템을 선택합니다.
2. 컴퓨터 이름과 전체 컴퓨터 이름이 같으면 DNS 접미사가 설정되지 않은 것입니다. 예를 들어 컴퓨터 이름이 ALLAN인 경우 전체 컴퓨터 이름의 값은 ALLAN이 아니어야 합니다. ALLAN.SQLHA.LAB과 같아야 합니다. SQLHA.LAB는 DNS 접미사입니다. 작업 그룹의 값은 WORKGROUP입니다. DNS 접미사를 설정해야 하는 경우 [설정 변경]을 선택합니다.
3. [시스템 속성] 대화 상자의 [컴퓨터 이름] 탭에서 [변경]을 클릭합니다.
4. [컴퓨터 이름/도메인 변경] 대화 상자에서 [자세히]를 클릭합니다.
5. [DNS 접미사 및 NetBIOS 컴퓨터 이름] 대화 상자에서 [기본 DNS] 접미사로 공통 DNS 접미사를 입력합니다. 
6. [확인]을 클릭하여 [DNS 접미사 및 NetBIOS 컴퓨터 이름] 대화 상자를 닫습니다.
7. [확인]을 클릭하여 [컴퓨터 이름/도메인 변경] 대화 상자를 닫습니다.
8. 변경 내용을 적용하려면 서버를 다시 시작하라는 메시지가 표시됩니다. [확인]을 클릭하여 [컴퓨터 이름/도메인 변경] 대화 상자를 닫습니다.
9. [닫기]를 클릭하여 [시스템 속성] 대화 상자를 닫습니다.
10. 다시 시작하라는 메시지가 표시됩니다. 즉시 다시 시작하지 않으려면 [나중에 다시 시작]을 클릭하고, 그렇지 않으면 [지금 다시 시작]을 클릭합니다.
11. 서버가 다시 부팅된 후 [시스템]을 다시 살펴보고 공통 DNS 접미사가 구성되었는지 확인합니다.


![DNS 접미사의 성공적인 구성][4]

## <a name="create-a-domain-independent-availability-group"></a>도메인 독립 가용성 그룹 만들기

도메인 독립 가용성 그룹은 현재 SQL Server Management Studio를 사용하여 만들 수는 없습니다. 도메인 독립 가용성 그룹을 만드는 것은 기본적으로 일반적인 가용성 그룹을 만드는 것과 동일하지만 인증서 생성과 같은 특정 측면은 Transact-SQL에서만 가능합니다. 아래 예제에서는 두 개의 복제본, 즉 주 복제본 하나와 보조 복제본 하나가 있는 가용성 그룹 구성을 가정하고 있습니다. 

1. [이 링크에 있는 지침을 사용](https://blogs.msdn.microsoft.com/clustering/2015/08/17/workgroup-and-multi-domain-clusters-in-windows-server-2016/)하여 가용성 그룹에 참여할 모든 서버로 구성된 작업 그룹 클러스터를 배포합니다. 작업 그룹 클러스터를 구성하기 전에 공통 DNS 접미사가 이미 구성되어 있는지 확인합니다.
2. 가용성 그룹에 참여할 각 인스턴스에서 [Always On 가용성 그룹 기능을 사용하도록 설정합니다](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server). 이렇게 하려면 각각의 SQL Server 인스턴스를 다시 시작해야 합니다.
3. 주 복제본을 호스팅할 각 인스턴스에는 데이터베이스 마스터 키가 필요합니다. 마스터 키가 아직 없으면 다음 명령을 실행합니다.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Strong Password';
   GO
   ```

4. 주 복제본이 될 인스턴스에서 보조 복제본을 인바운드 연결하고 주 복제본의 엔드포인트를 보호하는 데 사용할 인증서를 만듭니다.

   ```sql
   CREATE CERTIFICATE InstanceA_Cert 
   WITH SUBJECT = 'InstanceA Certificate';
   GO
   ``` 

5. 인증서를 백업합니다. 원하는 경우 개인 키를 사용하여 보안을 강화할 수도 있습니다. 이 예제에서는 개인 키를 사용하지 않습니다.

   ```sql
   BACKUP CERTIFICATE InstanceA_Cert 
   TO FILE = 'Backup_path\InstanceA_Cert.cer';
   GO
   ```

6. InstanceB_Cert와 같은 인증서에 대해 적절한 이름을 사용하여 4단계와 5단계를 반복하여 각 보조 복제본에 대한 인증서를 만들고 백업합니다.
7. 주 복제본에서 가용성 그룹의 각 보조 복제본에 대한 로그인을 만들어야 합니다. 이 로그인에는 도메인 독립 가용성 그룹에서 사용하는 엔드포인트에 연결할 수 있는 권한이 부여됩니다. 예를 들어 InstanceB라는 복제본의 경우 다음과 같습니다.

   ```sql
   CREATE LOGIN InstanceB_Login WITH PASSWORD = 'Strong Password';
   GO
   ```

8. 각 보조 복제본에서 주 복제본에 대한 로그인을 만듭니다. 이 로그인에는 엔드포인트에 연결할 수 있는 권한이 부여됩니다. 예를 들어 InstanceB라는 복제본의 경우 다음과 같습니다.

   ```sql
   CREATE LOGIN InstanceA_Login WITH PASSWORD = 'Strong Password';
   GO
   ```

9. 모든 인스턴스에서 만든 각 로그인에 대한 사용자를 만듭니다. 이 인증서는 인증서를 복원할 때 사용됩니다. 예를 들어 주 복제본에 대한 사용자를 생성하려면 다음과 같습니다.

   ```sql
   CREATE USER InstanceA_User FOR LOGIN InstanceA_Login;
   GO
   ```

10. 주 복제본일 수 있는 모든 복제본에 대해 모든 관련 보조 복제본에 로그인 및 사용자를 만듭니다.
11. 각 인스턴스에서 로그인 및 사용자가 작성된 다른 인스턴스의 인증서를 복원합니다. 주 복제본에서 모든 보조 복제본 인증서를 복원합니다. 각 보조 복제본에서 주 복제본의 인증서를 복원하고 주 복제본이 될 수 있는 다른 모든 복제본에서도 복원합니다. 예를 들어 다음과 같이 사용할 수 있습니다.

   ```sql
   CREATE CERTIFICATE [InstanceB_Cert]
   AUTHORIZATION InstanceB_User
   FROM FILE = 'Restore_path\InstanceB_Cert.cer'
   ```

12. 복제본이 될 각 인스턴스에서 가용성 그룹이 사용할 엔드포인트를 만듭니다. 가용성 그룹의 경우 엔드포인트의 유형은 DATABASE_MIRRORING이어야 합니다. 엔드포인트는 인증을 위해 해당 인스턴스에 대해 4단계에서 만든 인증서를 사용합니다. 인증서를 사용하여 엔드포인트를 만드는 예제 구문은 다음과 같습니다. 사용자 환경과 관련된 적절한 암호화 방법 및 다른 옵션을 사용합니다. 사용 가능한 옵션에 대한 자세한 내용은 [CREATE ENDPOINT(Transact-SQL)](../../../t-sql/statements/create-endpoint-transact-sql.md)를 참조하세요.

   ```sql
   CREATE ENDPOINT DIAG_EP
   STATE = STARTED
   AS TCP (   
    LISTENER_PORT = 5022,
    LISTENER_IP = ALL
         )
   FOR DATABASE_MIRRORING (
    AUTHENTICATION = CERTIFICATE InstanceX_Cert,
    ROLE = ALL
         )
   ```

13. 9단계에서 해당 인스턴스에 만든 각 사용자에게 권한을 할당하여 엔드포인트에 연결할 수 있습니다. 

   ```sql
   GRANT CONNECT ON ENDPOINT::DIAG_EP TO [InstanceX_User];
   GO
   ```

14. 기본 인증서와 엔드포인트 보안이 구성되었으면 기본 설정 방법을 사용하여 가용성 그룹을 만듭니다. 보조 복제본을 초기화하는 데 사용된 백업을 수동으로 백업, 복사 및 복원하거나 [자동 시드](automatically-initialize-always-on-availability-group.md)를 사용하는 것이 좋습니다. 마법사를 사용하여 보조 복제본을 초기화하면, 비도메인 가입 작업 그룹 클러스터를 사용할 때 작동하지 않을 수 있는 SMB(서버 메시지 블록) 파일이 사용됩니다.
15. 수신기를 만드는 경우 이름과 IP 주소가 모두 DNS에 등록되어 있는지 확인합니다.

### <a name="next-steps"></a>다음 단계 

- [가용성 그룹 마법사 사용(SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)

- [새 가용성 그룹 대화 상자 사용(SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)
 
- [Transact-SQL을 사용하여 가용성 그룹 만들기](create-an-availability-group-transact-sql.md)

<!--Image references-->
[1]: ./media/diag-wsfc-two-data-centers-same-domain.png
[2]: ./media/diag-workgroup-cluster-two-nodes-joined.png
[3]: ./media/diag-high-level-view-ag-standard-edition.png
[4]: ./media/diag-successful-dns-suffix.png
