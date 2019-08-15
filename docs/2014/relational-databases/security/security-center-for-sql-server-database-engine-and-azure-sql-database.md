---
title: SQL Server 데이터베이스 엔진 및 AAzure SQL Database에 대한 보안 센터 | Microsoft 문서
ms.custom: ''
ms.date: 09/23/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- Security [SQL Server]
helpviewer_keywords:
- SQL Server, security
- security [SQL Server]
- database security [SQL Server]
- databases [SQL Server], security
ms.assetid: dfb39d16-722a-4734-94bb-98e61e014ee7
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 131fb3639f84c1b59796d59bcfff17159da8f063
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028666"
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대한 보안 센터
  이 페이지에서는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]및 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]의 보안 및 보호에 대해 필요한 정보를 찾는 데 도움이 되는 링크를 제공합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] 의 기능은 지속적으로 개선됩니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 대한 가장 최근의 정보를 보려면 이 항목의 최신 버전을 참조하세요.  
  
|인증은 귀하는 누구인가요?|Authorization: 무엇을 할 수 있나요?|암호화 비밀 데이터 저장|연결 보안: 제한 및 보안|감사: 액세스 기록|  
|----------------------------------|-------------------------------------|-------------------------------------|---------------------------------------------------|--------------------------------|  
|**누가 인증했습니까?**<br /><br /> [![Security Center 맵 Windows 인증](../../database-engine/media/security-center-map-windows-authenticaion.png "Security Center 맵 Windows 인증")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> <br /><br /> [![Security Center 맵 SQL Server 인증](../../database-engine/media/security-center-map-sql-authenticaion.png "Security Center 맵 SQL Server 인증")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> **어디서 인증했습니까?**<br /><br /> [![로그인 및 사용자 Security Center 매핑](../../database-engine/media/security-center-map-logins-users.png "로그인 및 사용자 Security Center 매핑")](https://msdn.microsoft.com/library/aa337562.aspx)<br /><br /> <br /><br /> [![Security Center 맵에 포함 된 데이터베이스 사용자](../../database-engine/media/security-center-map-contained-users.png "Security Center 맵에 포함 된 데이터베이스 사용자")](https://msdn.microsoft.com/library/ff929188.aspx)<br /><br /> **다른 ID 사용**<br /><br /> [![Security Center 맵 자격 증명](../../database-engine/media/security-center-map-credentials.png "Security Center 맵 자격 증명")](https://msdn.microsoft.com/library/ms161950.aspx)<br /><br /> [![Security Center Map Execute As Login](../../database-engine/media/security-center-map-exec-as-login.png "Security Center Map Execute As Login")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> [![Security Center Map Execute As User](../../database-engine/media/security-center-map-exec-as-user.png "Security Center Map Execute As User")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")|**권한 부여, 취소 및 거부**<br /><br /> [![보안 개체 클래스 Security Center 매핑](../../database-engine/media/security-center-map-securable-classes.png "보안 개체 클래스 Security Center 매핑")](https://msdn.microsoft.com/library/ms190401.aspx)<br /><br /> [![Security Center Map 서버 사용 권한](../../database-engine/media/security-center-map-srv-perms.png "Security Center Map 서버 사용 권한")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> [![Security Center 맵 데이터베이스 사용 권한](../../database-engine/media/security-center-map-db-perms.png "Security Center 맵 데이터베이스 사용 권한")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> **역할별 보안**<br /><br /> [![Security Center 맵 서버 역할](../../database-engine/media/security-center-map-srv-roles.png "Security Center 맵 서버 역할")](https://msdn.microsoft.com/library/ms188659.aspx)<br /><br /> [![Security Center 맵 데이터베이스 역할](../../database-engine/media/security-center-map-db-roles.png "Security Center 맵 데이터베이스 역할")](https://msdn.microsoft.com/library/ms189121.aspx)<br /><br /> `Restricting Data Access to Selected Data Elements`<br /><br /> [![지도 보기 및 프로시저 Security Center](../../database-engine/media/security-center-map-view-procs.png "지도 보기 및 프로시저 Security Center")](https://msdn.microsoft.com/library/ms175503.aspx)<br /><br /> [![Security Center 맵 행 수준 보안](../../database-engine/media/security-center-map-row-level-sec.png "Security Center 맵 행 수준 보안")](https://msdn.microsoft.com/library/dn765131.aspx)<br /><br /> [![Security Center 맵 동적 데이터 마스킹](../../database-engine/media/security-center-map-data-masking.png "Security Center 맵 동적 데이터 마스킹")](https://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)<br /><br /> [![Security Center 맵 서명 된 개체](../../database-engine/media/security-center-map-signed-objects.png "Security Center 맵 서명 된 개체")](https://msdn.microsoft.com/library/ms181700.aspx)<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")|**파일 암호화**<br /><br /> [![Security Center 맵 BitLocker](../../database-engine/media/security-center-map-bitlocker.png "Security Center 맵 BitLocker")](https://support.microsoft.com/en-us/kb/2855131)<br /><br /> [![Security Center 맵 NTFS 암호화](../../database-engine/media/security-center-map-ntfs-encryp.png "Security Center 맵 NTFS 암호화")](https://msdn.microsoft.com/library/dd163562.aspx)<br /><br /> [![Security Center 맵 TDE](../../database-engine/media/security-center-map-tde.png "Security Center 맵 TDE")](https://msdn.microsoft.com/library/bb934049.aspx)<br /><br /> [![Security Center 맵 백업 암호화](../../database-engine/media/security-center-map-backup-encryp.png "Security Center 맵 백업 암호화")](https://msdn.microsoft.com/library/dn449489.aspx)<br /><br /> **소스 암호화**<br /><br /> [![Security Center 맵 EKM](../../database-engine/media/security-center-map-ekm.png "Security Center 맵 EKM")](https://msdn.microsoft.com/library/bb895340.aspx)<br /><br /> [![Security Center 맵 Azure Key Vault](../../database-engine/media/security-center-map-key-vault.png "Security Center 맵 Azure Key Vault")](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)<br /><br /> **열, 데이터 & 키 암호화**<br /><br /> [![인증서로 암호화 Security Center 맵](../../database-engine/media/security-center-map-cert.png "인증서로 암호화 Security Center 맵")](https://msdn.microsoft.com/library/ms188061.aspx)<br /><br /> [![대칭 키로 암호화 Security Center 맵](../../database-engine/media/security-center-map-sym-key.png "대칭 키로 암호화 Security Center 맵")](https://msdn.microsoft.com/library/ms174361.aspx)<br /><br /> [![비대칭 키로 암호화 Security Center 맵](../../database-engine/media/security-center-map-asym-key.png "비대칭 키로 암호화 Security Center 맵")](https://msdn.microsoft.com/library/ms186950.aspx)<br /><br /> [![암호를 사용한 Security Center 맵 암호화](../../database-engine/media/security-center-map-passphrase.png "암호를 사용한 Security Center 맵 암호화")](https://msdn.microsoft.com/library/ms190357.aspx)|**방화벽 보호**<br /><br /> [![Windows 방화벽 Security Center 매핑](../../database-engine/media/security-center-map-windows-firewall.png "Windows 방화벽 Security Center 매핑")](https://msdn.microsoft.com/library/ms175043.aspx)<br /><br /> [![Security Center 맵 서비스 방화벽](../../database-engine/media/security-center-map-service-firewall.png "Security Center 맵 서비스 방화벽")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> [![Security Center 맵 데이터베이스 방화벽](../../database-engine/media/security-center-map-db-firewall.png "Security Center 맵 데이터베이스 방화벽")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> **전송 중인 데이터 암호화**<br /><br /> [![Security Center 맵 강제 SSL](../../database-engine/media/security-center-map-forced-ssl.png "Security Center 맵 강제 SSL")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> [![Security Center 맵 선택적 SSL](../../database-engine/media/security-center-map-opt-ssl.png "Security Center 맵 선택적 SSL")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")|**감사 자동화**<br /><br /> [![Security Center Map SQL Server 감사](../../database-engine/media/security-center-map-sql-audit.png "Security Center Map SQL Server 감사")](https://msdn.microsoft.com/library/cc280386.aspx)<br /><br /> [![Security Center Map SQL Database 감사](../../database-engine/media/security-center-map-sqldb-audit.png "Security Center Map SQL Database 감사")](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)<br /><br /> **사용자 지정 감사**<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")<br /><br /> [![Security Center 맵 트리거](../../database-engine/media/security-center-map-triggers.png "Security Center 맵 트리거")](https://msdn.microsoft.com/library/ms175941.aspx)<br /><br /> **호환성**<br /><br /> [![SecCtrCompliance](../../database-engine/media/secctrcompliance.png "SecCtrCompliance")](https://azure.microsoft.com/support/trust-center/services/)<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")<br /><br /> ![자리 표시자](../../database-engine/media/security-center-map-blankplaceholder.png "자리 표시자")<br /><br /> ![Security Center 범례](../../database-engine/media/security-center-map-legend.png "Security Center 범례")|  
  
## <a name="links-to-specific-related-topics"></a>특정 관련 항목에 대한 링크  
 ![작은 파일 폴더 아이콘](../../integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") **인증: 누구시죠?**  
 **누가 인증 하나요? (Windows 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])**  
  
-   [인증 모드 선택](choose-an-authentication-mode.md)  
  
 **master 데이터베이스에서 인증** (로그인 및 데이터베이스 사용자)  
  
-   [SQL Server 로그인 만들기](authentication-access/create-a-login.md)  
  
-   [Azure SQL 데이터베이스에서 데이터베이스 및 로그인 관리](https://msdn.microsoft.com/library/ee336235.aspx)  
  
-   [데이터베이스 사용자 만들기](authentication-access/create-a-database-user.md)  
  
 **사용자 데이터베이스에서 인증**  
  
-   [포함된 데이터베이스 사용자 - 이식 가능한 데이터베이스 만들기](contained-database-users-making-your-database-portable.md)  
  
 **다른 ID 사용**  
  
-   [자격 증명&#40;데이터베이스 엔진&#41;](authentication-access/credentials-database-engine.md)  
  
-   [다른 로그인으로 실행합니다.](/sql/t-sql/statements/execute-as-transact-sql)  
  
-   [다른 데이터베이스 사용자로 실행](/sql/t-sql/statements/execute-as-transact-sql)  
  
 ![작은 파일 폴더 아이콘](../../integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") **암호화: 비밀 데이터 저장**  
 **파일 암호화**  
  
-   [BitLocker(드라이브 수준)](https://support.microsoft.com/kb/2855131)  
  
-   [NTFS 암호화(폴더 수준)](https://msdn.microsoft.com/library/dd163562.aspx)  
  
-   [투명한 데이터 암호화(파일 수준)](encryption/transparent-data-encryption.md)  
  
-   [백업 암호화(파일 수준)](../backup-restore/backup-encryption.md)  
  
 **소스 암호화**  
  
-   [확장 가능 키 관리 모듈](encryption/extensible-key-management-ekm.md)  
  
-   [Azure 키 자격 증명 모음에 저장된 키](encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
 **열, 데이터 및 키 암호화**  
  
-   [인증서로 암호화](/sql/t-sql/functions/encryptbycert-transact-sql)  
  
-   [비대칭 키로 암호화](/sql/t-sql/functions/encryptbyasymkey-transact-sql)  
  
-   [대칭 키로 암호화](/sql/t-sql/functions/encryptbykey-transact-sql)  
  
-   [암호로 암호화](/sql/t-sql/functions/encryptbypassphrase-transact-sql)  
  
 ![작은 파일 폴더 아이콘](../../integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") **권한 부여: 무엇을 할 수 있나요?**  
 **권한 부여, 취소 및 거부**  
  
-   [사용 권한 계층&#40;데이터베이스 엔진&#41;](permissions-hierarchy-database-engine.md)  
  
-   [사용 권한](permissions-database-engine.md)  
  
-   [보안 개체](securables.md)  
  
 **역할별 보안**  
  
-   [서버 수준 역할](authentication-access/server-level-roles.md)  
  
-   [데이터베이스 수준 역할](authentication-access/database-level-roles.md)  
  
 `Restricting Data Access to Selected Data Elements`  
  
-   [뷰](../views/views.md) 및 [프로시저](../stored-procedures/stored-procedures-database-engine.md)를 사용한 데이터 액세스 제한  
  
-   [행 수준 보안](https://msdn.microsoft.com/library/azure/dn765131.aspx)  
  
-   [동적 데이터 마스킹](https://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)  
  
-   [서명된 개체](/sql/t-sql/statements/add-signature-transact-sql)  
  
 ![작은 파일 폴더 아이콘](../../integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") **연결 보안: 제한 및 보안**  
 **방화벽 보호**  
  
-   [데이터베이스 엔진 액세스에 대한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
-   [Azure SQL 데이터베이스 방화벽 설정](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
-   [Azure 서비스 방화벽 설정](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
 **전송 중인 데이터 암호화**  
  
-   [데이터베이스 엔진에 대한 Secure Sockets Layer](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)  
  
-   [SQL 데이터베이스에 대한 Secure Sockets Layer](https://msdn.microsoft.com/library/azure/ff394108.aspx)  
  
 ![작은 파일 폴더 아이콘](../../integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") **감사: 액세스 기록**  
 **감사 자동화**  
  
-   [SQL Server Audit&#40;데이터베이스 엔진&#41;](auditing/sql-server-audit-database-engine.md)  
  
-   [SQL 데이터베이스 감사](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)  
  
 **사용자 지정 감사 구현**  
  
-   만들기 [DDL Triggers](../triggers/ddl-triggers.md) 및 [DML Triggers](../triggers/dml-triggers.md)  
  
 ![작은 파일 폴더 아이콘](../../integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") **규정 준수**  
 **SQL Server**  
  
-   [Common Criteria](https://go.microsoft.com/fwlink/?LinkId=616319)  
  
 **SQL 데이터베이스**  
  
-   [Microsoft Azure 보안 센터: 기능별 준수](https://azure.microsoft.com/support/trust-center/services/)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 보안 설정](securing-sql-server.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](authentication-access/principals-database-engine.md)   
 [SQL Server 인증서 및 비대칭 키](sql-server-certificates-and-asymmetric-keys.md)   
 [SQL Server 암호화](encryption/sql-server-encryption.md)   
 [노출 영역 구성](surface-area-configuration.md)   
 [강력한 암호](strong-passwords.md)   
 [TRUSTWORTHY 데이터베이스 속성](trustworthy-database-property.md)   
 [데이터베이스 엔진 기능 및 태스크](../../database-engine/database-engine-features-and-tasks.md)  
  
  
