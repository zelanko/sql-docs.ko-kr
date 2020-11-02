---
title: SQL Server 및 Azure SQL Database의 보안 문서
description: SQL Server 및 Azure SQL Database의 보안 및 보호 관련 콘텐츠 참조입니다.
ms.custom: seo-lt-2019
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e46a4a7cc107fb3d51f7f65130c3529290d54dfb
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92678961"
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대한 보안 센터
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  이 페이지에서는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 및 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]의 보안 및 보호에 대해 필요한 정보를 찾는 데 도움이 되는 링크를 제공합니다.  
  
 **범례**  
  
 ![기능 가용성 아이콘을 설명하는 범례 스크린샷](../performance/media/security-center-legend.PNG "security-center-legend")  
  
##  <a name="authentication-who-are-you"></a><a name="Who"></a> 인증: 귀하는 누구인가요?  
  
|||  
|-|-|  
|**누가 인증했습니까?**<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: Windows 인증<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증<br /><br /> :::image type="icon" source="../../relational-databases/security/media/security-center-sqldb.png"::: Azure Active Directory|누가 인증했습니까? (Windows 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])<br /><br /> [인증 모드 선택](../../relational-databases/security/choose-an-authentication-mode.md)<br /><br /> [Azure Active Directory 인증을 사용하여 SQL Database에 연결](/azure/azure-sql/database/authentication-aad-overview)|  
|**어디서 인증했습니까?**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: master 데이터베이스에서: 로그인 및 DB 사용자<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 사용자 데이터베이스에서: 포함된 DB 사용자|master 데이터베이스에서 인증(로그인 및 데이터베이스 사용자)<br /><br /> [SQL Server 로그인 만들기](../../relational-databases/security/authentication-access/create-a-login.md)<br /><br /> [Azure SQL Database에서 데이터베이스 및 로그인 관리](/previous-versions/azure/ee336235(v=azure.100))<br /><br /> [데이터베이스 사용자 만들기](../../relational-databases/security/authentication-access/create-a-database-user.md)<br /><br /> <br /><br /> 사용자 데이터베이스에서 인증<br /><br /> [포함된 데이터베이스 사용자 - 휴대용 데이터베이스 만들기](../../relational-databases/security/contained-database-users-making-your-database-portable.md)|  
|**다른 ID 사용**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 자격 증명<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: 다른 로그인으로 실행<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 다른 데이터베이스 사용자로 실행|[자격 증명&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)<br /><br /> [다른 로그인으로 실행합니다.](../../t-sql/statements/execute-as-transact-sql.md)<br /><br /> [다른 데이터베이스 사용자로 실행](../../t-sql/statements/execute-as-transact-sql.md)|  
  
##  <a name="authorization-what-can-you-do"></a><a name="What"></a> 권한 부여: 무엇을 할 수 있나요?  
  
|||  
|-|-|  
|**권한 부여, 취소 및 거부**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 보안 개체 클래스<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: 세분화된 서버 권한<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 세분화된 데이터베이스 권한|[사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)<br /><br /> [권한](../../relational-databases/security/permissions-database-engine.md)<br /><br /> [보안 개체](../../relational-databases/security/securables.md)<br /><br /> [데이터베이스 엔진 권한 시작](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)|  
|**역할별 보안**<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: 서버 수준 역할<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 데이터베이스 수준 역할|[서버 수준 역할](../../relational-databases/security/authentication-access/server-level-roles.md)<br /><br /> [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)|  
|**선택한 데이터 요소에 대한 데이터 액세스 제한**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 뷰/프로시저를 사용한 데이터 액세스 제한<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 행 수준 보안<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 동적 데이터 마스킹<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 서명된 개체|[뷰](../../relational-databases/views/views.md) 및 [프로시저](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)를 사용한 데이터 액세스 제한<br /><br /> [행 수준 보안(SQL Server)](../../relational-databases/security/row-level-security.md)<br /><br /> [행 수준 보안(Azure SQL 데이터베이스)](./row-level-security.md)<br /><br /> [동적 데이터 마스킹(SQL Server)](../../relational-databases/security/dynamic-data-masking.md)<br /><br /> [동적 데이터 마스킹(Azure SQL 데이터베이스)](/azure/azure-sql/database/dynamic-data-masking-overview)<br /><br /> [서명된 개체](../../t-sql/statements/add-signature-transact-sql.md)|  
  
##  <a name="encryption-storing-secret-data"></a><a name="Encrypt"></a> 암호화: 비밀 데이터 저장  
  
|||  
|-|-|  
|**파일 암호화**<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: BitLocker 암호화(드라이브 수준)<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: NTFS 암호화(폴더 수준)<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 투명한 데이터 암호화(파일 수준)<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 백업 암호화(파일 수준)|[BitLocker(드라이브 수준)](https://support.microsoft.com/kb/2855131)<br /><br /> [NTFS 암호화(폴더 수준)](/previous-versions/tn-archive/dd163562(v=technet.10))<br /><br /> [투명한 데이터 암호화(파일 수준)](../../relational-databases/security/encryption/transparent-data-encryption.md)<br /><br /> [백업 암호화(파일 수준)](../../relational-databases/backup-restore/backup-encryption.md)|  
|**소스 암호화**<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: 확장 가능 키 관리 모듈<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: Azure Key Vault에 저장된 키<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Always Encrypted|[확장 가능 키 관리 모듈](../../relational-databases/security/encryption/extensible-key-management-ekm.md)<br /><br /> [Azure 키 자격 증명 모음에 저장된 키](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)<br /><br /> [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)|  
|**열, 데이터 및 키 암호화**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 인증서로 암호화<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 대칭 키로 암호화<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 비대칭 키로 암호화<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 암호로 암호화|[인증서로 암호화](../../t-sql/functions/encryptbycert-transact-sql.md)<br /><br /> [비대칭 키로 암호화](../../t-sql/functions/encryptbyasymkey-transact-sql.md)<br /><br /> [대칭 키로 암호화](../../t-sql/functions/encryptbykey-transact-sql.md)<br /><br /> [암호로 암호화](../../t-sql/functions/encryptbypassphrase-transact-sql.md)<br /><br /> [데이터 열 암호화](../../relational-databases/security/encryption/encrypt-a-column-of-data.md)|  
  
##  <a name="connection-security-restricting-and-securing"></a><a name="Connect"></a> 연결 보안: 제한 및 보안  
  
|||  
|-|-|  
|**방화벽 보호**<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: Windows 방화벽 설정<br /><br /> :::image type="icon" source="../../relational-databases/security/media/security-center-sqldb.png"::: Azure 서비스 방화벽 설정<br /><br /> :::image type="icon" source="../../relational-databases/security/media/security-center-sqldb.png"::: 데이터베이스 방화벽 설정|[데이터베이스 엔진 액세스에 대한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)<br /><br /> [Azure SQL 데이터베이스 방화벽 설정](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)<br /><br /> [Azure 서비스 방화벽 설정](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)|  
|**전송 중인 데이터 암호화**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: 강제 SSL 연결<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: 선택적 SSL 연결|[데이터베이스 엔진에 암호화된 연결 사용](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)<br /><br /> [데이터베이스 엔진](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md), [네트워크 보안에 암호화된 연결 사용](/azure/sql-database/sql-database-security-best-practice#network-security) <br /><br /> [Microsoft SQL Server에 대한 TLS 1.2 지원](https://support.microsoft.com/kb/3135244)|  
  
##  <a name="auditing-recording-access"></a><a name="Audit"></a> 감사: 액세스 기록  
  
|||  
|-|-|  
|**감사 자동화**<br /><br /> :::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 감사(서버 및 DB 수준)<br /><br /> :::image type="icon" source="../../relational-databases/security/media/security-center-sqldb.png"::: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 감사(데이터베이스 수준)<br /><br /> :::image type="icon" source="../../relational-databases/security/media/security-center-sqldb.png"::: 위협 탐지| <br /><br /> [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)<br /><br /> [SQL 데이터베이스 감사](/azure/azure-sql/database/auditing-overview)<br /><br /> [SQL Database Advanced Threat Protection 시작](/azure/azure-sql/database/threat-detection-configure) <br /><br /> [SQL Database 취약성 평가](/azure/sql-database/sql-vulnerability-assessment) |  
|**사용자 지정 감사**<br /><br /> :::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: 트리거|사용자 지정 감사 구현: 만들기 [DDL Triggers](../../relational-databases/triggers/ddl-triggers.md) 및 [DML Triggers](../../relational-databases/triggers/dml-triggers.md)|  
|**호환성**<br /><br /> :::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: 규정 준수|SQL Server:<br />                        [Common Criteria](https://go.microsoft.com/fwlink/?LinkId=616319)<br /><br /> SQL 데이터베이스:<br />                        [Microsoft Azure 보안 센터: 기능별 준수](https://azure.microsoft.com/support/trust-center/services/)|  
  
##  <a name="sql-injection"></a><a name="SQLInjection"></a> SQL 인젝션  
 SQL 삽입은 문자열에 삽입된 악성 코드가 나중에 구문 분석 및 실행용으로 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 전달되는 방식의 공격입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 구문상 유효한 모든 수신 쿼리를 실행하므로 SQL 문을 생성하는 모든 프로시저에 삽입과 관련한 보안 위험이 있는지 확인해야 합니다. 모든 데이터베이스 시스템에는 어느 정도 SQL 삽입 공격을 받을 위험이 있으며, 대부분의 취약성은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 쿼리하는 애플리케이션에서 발생합니다. 저장 프로시저 및 매개 변수화된 명령을 사용하면 SQL 삽입 공격을 차단하여 동적 SQL을 방지하고 모든 사용자에 대해 권한을 제한할 수 있습니다.  자세한 내용은 [SQL Injection](../../relational-databases/security/sql-injection.md)을 참조하세요.  
  
 애플리케이션 프로그래머를 위한 추가 링크:  
  
-   [SQL Server의 애플리케이션 보안 시나리오](/dotnet/framework/data/adonet/sql/application-security-scenarios-in-sql-server)  
  
-   [SQL Server에서 보안 동적 SQL 작성](/dotnet/framework/data/adonet/sql/writing-secure-dynamic-sql-in-sql-server)  
  
-   [방법: ASP.NET에서 SQL 삽입으로부터 보호](/previous-versions/msp-n-p/ff648339(v=pandp.10))  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진 권한 시작](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [SQL Server 보안 설정](../../relational-databases/security/securing-sql-server.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [SQL Server 인증서 및 비대칭 키](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)   
 [SQL Server 암호화](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [노출 영역 구성](../../relational-databases/security/surface-area-configuration.md)   
 [강력한 암호](../../relational-databases/security/strong-passwords.md)   
 [TRUSTWORTHY 데이터베이스 속성](../../relational-databases/security/trustworthy-database-property.md)   
 [데이터베이스 엔진 기능 및 태스크](../../sql-server/what-s-new-in-sql-server-ver15.md)  
 [SQL Server 지적 재산 보호](../../relational-databases/security/protecting-your-sql-server-intellectual-property.md)   
  
[!INCLUDE[get-help-security](../../includes/get-help-security.md)]