---
title: SMB 파일 공유 저장소를 사용하여 SQL Server 설치 | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8b7810b2-637e-46a3-9fe1-d055898ba639
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 5f167c8789a1aea41a0d6c900f38462be8cb873d
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40410385"
---
# <a name="install-sql-server-with-smb-fileshare-storage"></a>SMB 파일 공유 저장소를 사용하여 SQL Server 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 시작해서 시스템 데이터베이스(Master, Model, MSDB 및 TempDB) 및 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 사용자 데이터베이스를 SMB(서버 메시지 블록) 파일 서버와 함께 저장소 옵션으로 설치할 수 있습니다. 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 독립 실행형 설치와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] FCI(장애 조치(Failover) 클러스터 설치) 모두에 적용됩니다.  
  
> [!NOTE]  
>  Filestream이 현재 SMB 파일 공유에서 지원되지 않습니다.  
  
## <a name="installation-considerations"></a>설치 고려 사항  
  
### <a name="smb-fileshare-formats"></a>SMB 파일 공유 형식:  
 SMB 파일 공유를 지정할 때 독립 실행형 및 FCI 데이터베이스에 대해 지원되는 UNC(Universal Naming Convention) 경로 형식은 다음과 같습니다.  
  
-   \\\ServerName\ShareName\  
  
-   \\\ServerName\ShareName  
  
 범용 명명 규칙에 대한 자세한 내용은 [UNC](http://msdn.microsoft.com/library/gg465305.aspx)를 참조하세요.  
  
 루프백 UNC 경로(서버 이름이 localhost, 127.0.0.1또는 로컬 컴퓨터 이름인 UNC 경로)는 지원되지 않습니다. 특별한 경우이기는 하지만 같은 노드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 호스팅되는 파일 서버 클러스터를 사용한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행도 지원되지 않습니다. 이러한 상황이 발생하지 않게 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 파일 서버 클러스터를 별도의 Windows 클러스터에 만드는 것이 좋습니다.  
  
 아래 UNC 경로 형식은 지원되지 않습니다.  
  
-   루프백 경로( \\\localhost\\..\ 또는 \\\127.0.0.1\\...\)  
  
-   관리 공유(예: \\\servername\x$)  
  
-   \\\\?\x:\ 등의 기타 UNC 경로  
  
-   매핑된 네트워크 드라이브  
  
### <a name="supported-data-definition-language-ddl-statements"></a>지원되는 DDL(데이터 정의 언어) 문  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 문과 데이터베이스 엔진 저장 프로시저는 SMB 파일 공유를 지원합니다.  
  
1.  [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
2.  [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
3.  [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
4.  [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)  
  
### <a name="installation-options"></a>설치 옵션  
  
-   설치 UI "데이터베이스 엔진 구성" 페이지의 "데이터 디렉터리" 탭에서 "데이터 루트 디렉터리" 매개 변수를 "\\\fileserver1\share1\"로 설정합니다.  
  
-   명령 프롬프트 설치에서 "/INSTALLSQLDATADIR"을 "\\\fileserver1\share1\"로 지정합니다.  
  
     다음은 SMB 파일 공유 옵션을 사용하여 독립 실행형 서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치하는 예제 구문입니다.  
  
    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="<StrongPassword>" /INSTALLSQLDATADIR="\\FileServer\Share1\" /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 와 함께 기본 인스턴스로 단일 노드 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]장애 조치(Failover) 클러스터 인스턴스를 설치합니다.  
  
    ```  
    setup.exe /q /ACTION=InstallFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'" /FAILOVERCLUSTERNETWORKNAME="<Insert Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /Features=AS,SQL /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /INSTALLSQLDATADIR="\\FileServer\Share1\" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /SQLSYSADMINACCOUNTS="<DomainName\UserName> /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 다양한 명령줄 매개 변수 옵션의 사용법에 대한 자세한 내용은 [명령 프롬프트에서 SQL Server 2016 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)를 참조하세요.  
  
## <a name="operating-system-considerations-smb-protocol-vs-includessnoversionincludesssnoversion-mdmd"></a>운영 체제 고려 사항(SMB 프로토콜 대 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])  
 Windows 운영 체제마다 포함되어 있는 SMB 프로토콜 버전이 다르며 SMB 프로토콜 버전은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 투명합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]와 관련하여 다른 SMB 프로토콜 버전의 이점을 찾을 수 있습니다.  
  
|운영 체제|SMB2 프로토콜 버전|이점 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|----------------------|---------------------------|-------------------------------------------|  
|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP 2|2.0|이전 SMB 버전보다 성능이 향상되었습니다.<br /><br /> 내구성. 일시적인 네트워크 결함을 복구하는 데 도움이 됩니다.|  
|[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP 1(Server Core 포함)|2.1|대형 MTU 지원. SQL 백업 및 복원과 같은 대량 데이터 전송에 유용합니다. 이 기능은 사용자가 사용하도록 설정해야 합니다. 이 기능을 사용하는 방법에 대한 자세한 내용은 [SMB의 새로운 기능](http://go.microsoft.com/fwlink/?LinkID=237319)(http://go.microsoft.com/fwlink/?LinkID=237319)을 참조하세요.<br /><br /> 크게 향상된 성능(특히 SQL OLTP 스타일 작업의 경우) 이러한 향상된 성능을 활용하려면 핫픽스를 적용해야 합니다. 핫픽스에 대한 자세한 내용은 [이 항목](http://go.microsoft.com/fwlink/?LinkId=237320)(http://go.microsoft.com/fwlink/?LinkId=237320))을 참조하세요.|  
|[!INCLUDE[win8srv](../../includes/win8srv-md.md)](Server Core 포함)|3.0|파일 서버 클러스터 구성에서 SQL DBA 또는 파일 서버 관리자에게 필요한 관리자 개입이 없고 작동 중단 시간이 없는 파일 공유의 투명한 장애 조치(failover) 지원<br /><br /> 여러 네트워크 인터페이스를 동시에 사용할 뿐 아니라 네트워크 인터페이스 오류에 대한 허용 오차를 사용하는 IO 지원<br /><br /> RDMA 기능을 사용하는 네트워크 인터페이스 지원<br /><br /> 이러한 기능 및 서버 메시지 블록에 대한 자세한 내용은 [서버 메시지 블록 개요](http://go.microsoft.com/fwlink/?LinkId=253174)(http://go.microsoft.com/fwlink/?LinkId=253174)를 참조하세요.<br /><br /> 지속적인 가용성과 함께 SoFS(Scale Out File Server) 지원.|  
|[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2(Server Core 포함)|3.2|파일 서버 클러스터 구성에서 SQL DBA 또는 파일 서버 관리자에게 필요한 관리자 개입이 없고 작동 중단 시간이 없는 파일 공유의 투명한 장애 조치(failover) 지원<br /><br /> SMB 다중 채널을 사용해서 여러 네트워크 인터페이스를 동시에 사용할 뿐 아니라 네트워크 인터페이스 오류에 대한 허용 오차를 사용하는 IO 지원<br /><br /> SMB 다이렉트를 사용하여 RDMA 기능을 사용하는 네트워크 인터페이스 지원<br /><br /> 이러한 기능 및 서버 메시지 블록에 대한 자세한 내용은 [서버 메시지 블록 개요](http://go.microsoft.com/fwlink/?LinkId=253174)(http://go.microsoft.com/fwlink/?LinkId=253174)를 참조하세요.<br /><br /> 지속적인 가용성과 함께 SoFS(Scale Out File Server) 지원.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLTP에 일반적인 작은 임의 읽기/쓰기 I/O에 최적화됨.<br /><br /> MTU(최대 전송 단위)는 기본적으로 설정되어 있으며, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 웨어하우스 및 데이터베이스 백업 또는 복원과 같은 대규모 순차적 전송에서 성능을 크게 향상시켜 줍니다.|  
  
## <a name="security-considerations"></a>보안 고려 사항  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정은 SMB 공유 폴더에 대해 FULL CONTROL 공유 권한 및 NTFS 권한이 있어야 합니다. SMB 파일 서버가 사용되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정은 도메인 계정 또는 시스템 계정일 수 있습니다. 공유 및 NTFS 권한에 대한 자세한 내용은 [파일 서버의 공유 및 NTFS 권한](http://go.microsoft.com/fwlink/?LinkId=245535)(http://go.microsoft.com/fwlink/?LinkId=245535)을 참조하세요.  
  
    > [!NOTE]  
    >  SMB 공유 폴더에 대한 FULL CONTROL 공유 권한 및 NTFS 권한은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정 및 관리자 서버 역할이 할당된 Windows 사용자에게만 부여되어야 합니다.  
  
     도메인 계정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정으로 사용하는 것이 좋습니다. 시스템 계정을 서비스 계정으로 사용하는 경우에는 \<*domain_name*>\\<*computer_name*>\*$* 형식으로 컴퓨터 계정에 대한 사용 권한을 부여해야 합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치할 때 SMB 파일 공유를 저장소 옵션으로 지정하는 경우 도메인 계정을 서비스 계정으로 지정해야 합니다. SMB 파일 공유를 사용하는 경우 시스템 계정은 서비스 계정 게시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치로만 지정할 수 있습니다.  
    >   
    >  가상 계정은 원격 위치에 대해 인증할 수 없습니다. 모든 가상 계정에는 시스템 계정의 사용 권한이 사용됩니다. \<*domain_name*>\\<*computer_name*>\*$* 형식으로 컴퓨터 계정을 프로비전합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 사용되는 계정에는 클러스터를 설치하는 동안 데이터 디렉터리로 사용되는 SMB 파일 공유 폴더 또는 다른 데이터 폴더(사용자 데이터베이스 디렉터리, 사용자 데이터베이스 로그 디렉터리, TempDB 디렉터리, TempDB 로그 디렉터리, 백업 디렉터리)에 대해 FULL CONTROL NTFS 권한이 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 사용되는 계정에는 SMB 파일 서버에 대한 SeSecurityPrivilege 권한이 부여되어야 합니다. 이 권한을 부여하려면 파일 서버의 로컬 보안 정책 콘솔을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 계정을 감사 및 보안 로그 관리 정책에 추가합니다. 이 설정은 로컬 보안 정책 콘솔의 로컬 정책에 있는 사용자 권한 할당 섹션에서 사용할 수 있습니다.  
  
## <a name="known-issues"></a>알려진 문제  
  
-   네트워크로 연결된 저장소에 있는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 데이터베이스를 분리한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 다시 연결하려고 시도하는 동안 데이터베이스 권한 문제가 발생할 수 있습니다. 이 문제는 [이 KB 아티클](http://go.microsoft.com/fwlink/?LinkId=237321)(http://go.microsoft.com/fwlink/?LinkId=237321)에 정의되어 있습니다. 이 문제를 해결하려면 KB 문서의 **자세한 정보** 섹션을 참조하십시오.  
  
-   SMB 파일 공유가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 클러스터형 인스턴스에 대한 저장소 옵션으로 사용되는 경우, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스 DLL에는 파일 공유에 대한 읽기/쓰기 권한이 부족하기 때문에 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 진단 로그에서 파일 공유에 쓸 수 없습니다. 이 문제를 해결하려면 다음 방법 중 하나를 사용하십시오.  
  
    1.  클러스터의 모든 컴퓨터 개체에 파일 공유에 대한 읽기/쓰기 권한을 부여합니다.  
  
    2.  진단 로그의 위치를 로컬 파일 경로로 설정합니다. 다음 예제를 참조하십시오.  
  
        ```sql  
        ALTER SERVER CONFIGURATION  
        SET DIAGNOSTICS LOG PATH = 'C:\logs';  
        ```  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
