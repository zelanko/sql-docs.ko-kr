---
title: Oracle 게시자 구성 | Microsoft 문서
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], configuring
ms.assetid: 240c8416-c8e5-4346-8433-07e0f779099f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2b91e4f912de3eff2d64e7cbbf35aad56cbccbcd
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/18/2019
ms.locfileid: "58072227"
---
# <a name="configure-an-oracle-publisher"></a>Oracle 게시자 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Oracle 게시자에서의 게시는 일반 스냅숏 및 트랜잭션 게시가 만들어지는 것과 같은 방식으로 만들어지지만 Oracle 게시자에서 게시를 만들려면 먼저 다음 단계(1, 3, 4단계는 이 항목에서 자세히 설명)를 수행해야 합니다.  
  
1.  제공된 스크립트를 사용하여 Oracle 데이터베이스 내에 복제 관리 사용자를 만듭니다.  
  
2.  게시하는 테이블에 대해서는 1단계에서 만든 Oracle 관리 사용자에게 SELECT 권한을(역할을 사용하지 않고 ) 직접 부여합니다.  
  
3.  Oracle 클라이언트 소프트웨어와 OLE DB 공급자를 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에 설치한 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 중지했다가 다시 시작합니다. 배포자가 64비트 플랫폼에서 실행되는 경우 64비트 버전의 Oracle OLE DB 공급자를 사용해야 합니다.  
  
4.  Oracle 데이터베이스를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에서 게시자로 구성합니다.  

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 트랜잭션 및 스냅숏 복제에 대해 다음과 같이 다른 유형의 시나리오를 지원합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 구독자로 데이터 게시  

-   Oracle에서 데이터를 게시할 때 다음과 같은 제한 사항이 있습니다.  

  | |2016 또는 이전 버전 |2017 이상 |
  |-------|-------|--------|
  |Oracle에서 복제 |Oracle 10g 또는 이전 버전만 지원 |Oracle 10g 또는 이전 버전만 지원 |
  |Oracle로 복제 |Oracle 12c까지 |지원되지 않음 |

 SQL Server 이외의 구독자에 대한 다른 유형의 복제는 지원되지 않습니다. Oracle 게시는 지원되지 않습니다. 데이터를 이동하려면 변경 데이터 캡처 및 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]를 사용하여 솔루션을 만듭니다.  


 Oracle 데이터베이스에서 복제할 수 있는 개체 목록은 [Oracle 게시자에 대한 디자인 고려 사항 및 제한 사항](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)을 참조하세요.  
  
> [!NOTE]  
>  게시자나 배포자를 설정하고 Oracle 게시를 만들거나 Oracle 게시에서 구독을 만들려면 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
## <a name="creating-the-replication-administrative-user-schema-within-the-oracle-database"></a>Oracle 데이터베이스 내에 복제 관리 사용자 스키마 만들기  
 복제 에이전트는 Oracle 데이터베이스에 연결한 다음 만들어야 할 사용자 스키마 컨텍스트에서 작업을 수행합니다. 이 스키마에는 몇 가지 사용 권한을 부여해야 하며 이는 다음 섹션에 나열되어 있습니다. 이 스키마는 Oracle 게시자의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제 프로세스에서 만든 모든 개체( **MSSQLSERVERDISTRIBUTOR**공용 동의어 제외)를 소유합니다. Oracle 데이터베이스에서 만든 개체에 대한 자세한 내용은 [Objects Created on the Oracle Publisher](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)를 참조하십시오.  
  
> [!NOTE]  
>  **CASCADE** 옵션으로 **MSSQLSERVERDISTRIBUTOR** 공용 동의어와 구성된 Oracle 복제 사용자를 삭제하면 Oracle 게시자에서 모든 복제 개체가 제거됩니다.  
  
 Oracle 복제 사용자 스키마의 설치를 도와 주는 예제 스크립트가 제공됩니다. 이 스크립트는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 후 *\<드라이브>*:\\\Program Files\Microsoft SQL Server\\*\<InstanceName>* \MSSQL\Install\oracleadmin.sql 디렉터리에서 사용할 수 있습니다. 이 스크립트에 대한 내용은 [Script to Grant Oracle Permissions](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md)항목에도 포함되어 있습니다.  
  
 DBA 권한이 있는 계정을 사용하여 Oracle 데이터베이스에 연결하고 해당 스크립트를 실행합니다. 이 스크립트는 개체를 만들 기본 테이블스페이스(이 테이블스페이스는 이미 Oracle 데이터베이스에 있어야 함)를 비롯하여 복제 관리 사용자 스키마에 대한 사용자 이름 및 암호를 묻는 메시지를 표시합니다. 개체에 대해 다른 테이블스페이스를 지정하는 방법은 [Oracle 테이블스페이스 관리](../../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md)를 참조하세요. 원하는 사용자 이름과 강력한 암호를 선택한 다음 이를 기록해 둡니다. 나중에 Oracle 데이터베이스를 게시자로 구성할 때 이러한 정보를 제공해야 합니다. 복제에 필요한 개체에 대해서만 스키마를 사용하는 것이 좋습니다. 이 스키마에 게시될 테이블은 만들지 마십시오.  
  
### <a name="creating-the-user-schema-manually"></a>수동으로 사용자 스키마 만들기  
 복제 관리 사용자 스키마를 수동으로 만드는 경우에는 스키마에 다음 사용 권한을 직접 또는 데이터베이스 역할을 통해 부여해야 합니다.  
  
-   CREATE PUBLIC SYNONYM 및 DROP PUBLIC SYNONYM  
  
-   CREATE PROCEDURE  
  
-   CREATE SEQUENCE  
  
-   CREATE SESSION  
  
 또한 사용자에게 다음 사용 권한을 역할을 사용하지 않고 직접 부여해야 합니다.  
  
-   CREATE ANY TRIGGER. 스냅숏 및 트랜잭션 복제에만 필요합니다.  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
## <a name="installing-and-configuring-oracle-client-networking-software-on-the-sql-server-distributor"></a>SQL Server 배포자에 Oracle 클라이언트 네트워킹 소프트웨어 설치 및 구성  
 Oracle 클라이언트 네트워킹 소프트웨어와 Oracle OLE DB 공급자를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에서 설치 및 구성해야 Oracle 게시자에 배포자를 연결할 수 있습니다. 소프트웨어를 설치한 후에는 소프트웨어가 설치된 폴더에 적절한 사용 권한을 설정한 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 중지했다가 다시 시작하여 모든 설정을 업데이트합니다. 사용 권한은 아래의 "디렉터리 사용 권한 설정" 섹션에서 설명합니다.  
  
> [!NOTE]  
>  Oracle 클라이언트 네트워킹 소프트웨어는 사용 가능한 최신 버전이어야 합니다. Oracle에서는 최신 버전의 클라이언트 소프트웨어를 설치할 것을 권장합니다. 따라서 클라이언트 소프트웨어 버전이 데이터베이스 소프트웨어 버전보다 최신인 경우가 종종 있습니다.  
  
 클라이언트 네트워킹 소프트웨어를 설치하고 구성할 수 있는 가장 간단한 방법은 Oracle 클라이언트 디스크에 있는 Oracle Universal Installer와 Net Configuration Assistant를 사용하는 것입니다.  
  
 Oracle Universal Installer에서 다음 정보를 제공해야 합니다.  
  
|정보|설명|  
|-----------------|-----------------|  
|Oracle|Oracle 소프트웨어 설치를 위한 디렉터리 경로입니다. 기본값(C:\oracle\ora90 또는 유사한 경로)을 그대로 적용하거나 다른 경로를 입력합니다. Oracle 홈에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "Oracle 홈에 대한 고려 사항" 섹션을 참조하십시오.|  
|Oracle 홈 이름|Oracle 홈 경로에 대한 별칭입니다.|  
|설치 유형|Oracle 10g에서 **관리자** 설치 옵션을 선택합니다.|  
  
 Oracle Universal Installer가 작업을 완료하면 Net Configuration Assistant를 사용하여 네트워크 연결을 구성합니다. 네트워크 연결을 구성하려면 다음 4가지 정보를 입력해야 합니다. Oracle 데이터베이스 관리자는 데이터베이스와 수신기를 설정할 때 네트워크를 구성하며, 필요한 경우 이 정보를 사용자에게 제공할 수 있어야 합니다. 다음과 같은 작업을 수행해야 합니다.  
  
|작업|설명|  
|------------|-----------------|  
|데이터베이스 식별|두 가지 방법으로 데이터베이스를 식별할 수 있습니다. 첫 번째 방법은 Oracle SID(시스템 식별자)를 사용하는 것으로 모든 Oracle 릴리스에서 사용할 수 있습니다. 두 번째 방법은 서비스 이름을 사용하는 것으로 Oracle 릴리스 8.0부터 사용할 수 있습니다. 두 가지 방법 모두 데이터베이스를 만들 때 구성된 값을 사용하며 클라이언트 네트워크 구성에서 데이터베이스를 위한 수신기를 구성할 때 관리자가 사용한 것과 동일한 명명 규칙을 사용하는 것이 중요합니다.|  
|데이터베이스에 대한 네트워크 별칭 식별|Oracle 데이터베이스 액세스에 사용할 네트워크 별칭을 지정해야 합니다. 이 별칭은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에서 Oracle 데이터베이스를 게시자로 식별할 때도 제공해야 합니다. 네트워크 별칭은 데이터베이스를 만들 때 구성된 원격 SID 또는 서비스 이름을 가리킵니다. 이 별칭은 다양한 Oracle 릴리스 및 제품에서 네트 서비스 이름 및 TNS 별칭 등 여러 이름으로 불립니다. SQL*Plus의 경우 로그인 시 이 별칭을 "Host String" 매개 변수로 입력하라는 메시지가 나타납니다.|  
|네트워크 프로토콜 선택|지원할 적절한 프로토콜을 선택합니다. 대부분의 애플리케이션은 TCP를 사용합니다.|  
|데이터베이스 수신기를 식별할 호스트 정보 지정|호스트는 Oracle 수신기가 실행 중인 컴퓨터의 이름이나 DNS 별칭이며, 일반적으로 Oracle 수신기는 데이터베이스가 상주하는 컴퓨터에서 실행됩니다. 일부 프로토콜의 경우 추가 정보를 제공해야 합니다. 예를 들어 TCP를 선택할 경우 수신기가 대상 데이터베이스에 대한 연결 요청을 수신하는 포트를 지정해야 합니다. 기본 TCP 구성은 포트 1521을 사용합니다.|  
  
### <a name="setting-directory-permissions"></a>디렉터리 사용 권한 설정  
 배포자에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 실행되는 계정에는 Oracle 클라이언트 네트워킹 소프트웨어를 설치할 디렉터리 및 모든 하위 디렉터리에 대한 읽기 및 실행 권한이 부여되어야 합니다.  
  
### <a name="testing-connectivity-between-the-sql-server-distributor-and-the-oracle-publisher"></a>SQL Server 배포자와 Oracle 게시자 간 연결 테스트  
 Net Configuration Assistant의 후반부에는 Oracle 게시자에 대한 연결을 테스트하는 옵션이 있습니다. 연결을 테스트하기 전에 Oracle 데이터베이스 인스턴스가 온라인 상태인지 Oracle 수신기가 실행 중인지 확인합니다. 테스트가 실패하면 연결하려는 데이터베이스를 담당하는 Oracle DBA에게 문의하십시오.  
  
 Oracle 게시자에 성공적으로 연결한 다음에는 만든 복제 관리 사용자 스키마에 연결된 계정과 암호를 사용하여 데이터베이스에 로그인합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 사용하는 것과 같은 Windows 계정으로 실행하는 동안 다음을 수행해야 합니다.  
  
1.  **시작**을 클릭한 다음 **실행**을 클릭합니다.  
  
2.  `cmd` 를 입력한 다음 **확인**을 클릭합니다.  
  
3.  명령 프롬프트에서 다음을 입력합니다.  
  
     `sqlplus <UserSchemaLogin>/<UserSchemaPassword>@<NetServiceName>`  
  
     예: `sqlplus replication/$tr0ngPasswerd@Oracle90Server`  
  
4.  네트워크 구성이 성공했다면 로그인이 성공하고 `SQL` 프롬프트가 표시됩니다.  
  
5.  Oracle 데이터베이스 연결에 문제가 있으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 " [ssNoVersion](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)을 참조하십시오.  
  
### <a name="considerations-for-oracle-home"></a>Oracle 홈에 대한 고려 사항  
 Oracle은 애플리케이션 이진 파일을 함께 설치하도록 지원하지만 복제에서는 특정 시간에 하나의 이진 파일 집합만 사용할 수 있습니다. 각 이진 파일 집합은 Oracle 홈과 연결되어 있으며 이진 파일은 %ORACLE_HOME%\bin 디렉터리에 있습니다. 복제에서 Oracle 게시자에 연결할 때는 올바른 이진 집합(최신 버전의 클라이언트 네트워킹 소프트웨어)이 사용되어야 합니다.  
  
 배포자에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 서비스에서 사용하는 계정으로 로그인하여 적절한 환경 변수를 설정합니다. %ORACLE_HOME% 변수는 클라이언트 네트워킹 소프트웨어 설치 시 지정한 설치 지점을 참조할 수 있도록 설정되어야 합니다. %PATH%는 %ORACLE_HOME% \bin 디렉터리를 처음 검색되는 Oracle 항목으로 포함해야 합니다. 환경 변수 설정 방법은 Windows 설명서를 참조하십시오.  
  
## <a name="configuring-the-oracle-database-as-a-publisher-at-the-sql-server-distributor"></a>SQL Server 배포자에서 Oracle 데이터베이스를 게시자로 구성  
 Oracle 게시자는 항상 원격 배포자를 사용하므로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인스턴스가 Oracle 게시자의 배포자로 동작하도록 구성해야 합니다. Oracle 게시자는 배포자를 하나만 사용할 수 있지만 단일 배포자는 두 개 이상의 Oracle 게시자에 사용될 수 있습니다. 배포자를 구성한 다음에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에서 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], Transact-SQL 또는 RMO(복제 관리 개체)를 통해 Oracle 데이터베이스 인스턴스를 게시자로 식별합니다. 배포자 구성에 대한 자세한 내용은 [배포 구성](../../../relational-databases/replication/configure-distribution.md)을 참조하세요.  
  
> [!NOTE]  
>  Oracle 게시자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자 또는 동일한 배포자를 사용하는 모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 게시자와 같은 이름을 가질 수 없습니다.  
  
 Oracle 데이터베이스를 게시자로 식별하는 경우 Oracle 게시 옵션인 Oracle Complete 또는 Oracle Gateway 중 하나를 선택해야 합니다. 게시자를 식별한 다음에 이 옵션을 변경하려면 해당 게시자를 삭제하고 다시 구성해야 합니다. Oracle Complete 옵션은 Oracle 게시에 대해 지원되는 전체 기능 집합과 함께 스냅숏 및 트랜잭션 게시를 제공하도록 디자인되었습니다. Oracle Gateway 옵션은 복제가 시스템 간 게이트웨이 역할을 하는 경우 성능을 향상시킬 수 있도록 특정 디자인 최적화를 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에서 Oracle 게시자를 식별한 다음 복제는 Oracle 데이터베이스의 TNS 서비스 이름과 같은 이름으로 연결된 서버를 만듭니다. 이 연결된 서버는 복제에서만 사용할 수 있습니다. 연결된 서버 연결을 통해 Oracle 게시자에 연결하려면 다른 TNS 서비스 이름을 만든 다음 이 이름을 사용하여 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)를 호출합니다.  
  
 Oracle 게시자를 구성하고 게시를 만들려면 [Create a Publication from an Oracle Database](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시자에 대한 관리 고려 사항](../../../relational-databases/replication/non-sql/administrative-considerations-for-oracle-publishers.md)   
 [Oracle 게시자에 대한 데이터 형식 매핑](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Oracle 게시를 위한 용어 설명](../../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Oracle 게시 개요](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
