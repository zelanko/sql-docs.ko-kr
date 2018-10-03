---
title: Oracle CDC Service | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 47759ddc-358d-405b-acb9-189ada76ea6d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 105f32a1e95852a0c08b47da0632b53522718957
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47780497"
---
# <a name="the-oracle-cdc-service"></a>Oracle CDC Service
  Oracle CDC Service는 xdbcdcsvc.exe 프로그램을 실행하는 Windows 서비스입니다. 동일한 컴퓨터에서 각각 다른 Windows 서비스 이름이 있는 여러 Windows 서비스를 실행하도록 Oracle CDC Service를 구성할 수 있습니다. 일반적으로 서비스 간을 더 잘 분리하기 위해 또는 각 서비스가 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 작업해야 하는 경우에 단일 컴퓨터에서 여러 Oracle CDC Windows 서비스를 만듭니다.  
  
 Oracle CDC Service는 Oracle CDC Service 구성 콘솔을 사용하여 만들어지거나 xdbcdcsvc.exe 프로그램에 기본 제공되는 명령줄 인터페이스를 통해 정의됩니다. 두 경우 모두 만들어진 각 Oracle CDC Service는 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스( **Always On** 설정 시 클러스터링하거나 미러할 수 있음)와 연결되며 연결 정보(연결 문자열 및 액세스 자격 증명)는 서비스 구성의 일부입니다.  
  
 Oracle CDC Service가 시작되면 관련된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결을 시도하고, 처리해야 할 Oracle CDC 인스턴스 목록을 가져온 다음, 초기 환경 유효성 검사를 수행합니다. 서비스 시작 중 오류와 모든 시작/중지 정보가 항상 Windows 응용 프로그램 이벤트 로그에 기록됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결이 설정되면 모든 오류와 정보 메시지가 **인스턴스의 MSXDBCDC 데이터베이스에 있는** dbo.xdbcdc_trace [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 기록됩니다. 시작 중에 수행되는 확인 중 하나는 같은 이름의 다른 Oracle CDC Service가 현재 작업 중이 아닌지 확인하는 것입니다. 같은 이름의 서비스가 다른 컴퓨터에서 현재 연결되어 있는 경우 Oracle CDC Service는 대기 루프를 시작하여 다른 서비스의 연결이 끊어질 때까지 기다린 후 Oracle CDC 작업 처리를 진행합니다.  
  
 Oracle CDC Service가 모든 시작 확인을 통과하면 MSXDBCDC 데이터베이스의 **dbo.xdbcdc_databases** 테이블에서 사용되는 Oracle CDC 인스턴스가 있는지 확인합니다. 활성화된 모든 Oracle CDC 인스턴스에 대해 서비스는 해당 Oracle CDC 인스턴스를 처리하는 하위 프로세스를 시작합니다.  
  
 Oracle CDC 인스턴스가 시작되면 CDC 인스턴스와 이름이 같은 SQL Server CDC 데이터베이스를 평가하고 이전 실행에서 상태를 검색합니다. 모두 제대로 실행 중인지도 확인합니다. 그런 다음 처리 변경을 재개하여 Oracle 트랜잭션 로그를 읽고 CDC 데이터베이스에 변경 내용을 기록합니다.  
  
 Oracle CDC Service는 MSXDBCDC 데이터베이스의 **dbo.xdbcdc_tables** 테이블을 정기적으로 모니터링하여 Oracle CDC 인스턴스 구성에 구성 변경이 있는지 확인합니다. 변경이 발견되면 Oracle CDC Service는 Oracle CDC 인스턴스에 구성 변경을 확인해야 한다고 알립니다. 캡처 인스턴스 추가 및 제거와 같은 대부분의 구성 변경은 Oracle CDC 인스턴스가 사용되는 동안 적용할 수 있으며, 다른 변경은 Oracle CDC 인스턴스를 다시 시작해야 합니다.  
  
 Oracle CDC Designer 콘솔을 사용하는 경우 변경 내용은 자동으로 감지됩니다. SQL을 사용하여 Oracle CDC 구성을 직접 업데이트하는 경우 Oracle CDC Service에서 구성 변경을 알리기 위해 다음 절차를 호출해야 합니다.  
  
```sql
DECLARE @dbname nvarchar(128) = 'HRcdc'  
EXECUTE [MSXDBCDC].[dbo].[xdbcdc_update_config_version] @dbname  
GO  
  
```  
  
 Oracle CDC 인스턴스 프로세스는 시스템 테이블 **cdc.xdbcdc_state** 에서 상태를 업데이트하고 오류 정보를 **cdc.xdbcdc_trace** 테이블에 기록합니다. **Xdbcdc_state** 테이블은 Oracle CDC 인스턴스의 상태를 모니터링하는 데 유용합니다. 이 테이블은 최신 상태, 다양한 카운터(예: Oracle에서 읽은 변경 수, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 기록한 변경 수, 기록된 커밋된 트랜잭션 수 및 현재 진행 중인 트랜잭션 수) 및 대기 시간 표시를 제공합니다.  
  
 Oracle CDC 인스턴스 구성은 Oracle CDC Designer 콘솔이 작업하는 테이블인 **cdc.xdbcdc_config** 테이블에 저장됩니다. Oracle CDC 인스턴스의 전체 구성이 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 CDC 데이터베이스에 있으므로 Oracle CDC 인스턴스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포 스크립트를 만들 수 있습니다. 이 작업은 Oracle CDC Service 구성 및 Oracle CDC Designer 콘솔을 사용하여 수행됩니다.  
  
## <a name="security-considerations"></a>보안 고려 사항  
 다음에서는 Oracle CDC Service에서 작업하는 데 필요한 보안 요구 사항에 대해 설명합니다.  
  
### <a name="protection-of-source-oracle-data"></a>원본 Oracle 데이터의 보호  
 Oracle CDC Service는 Oracle 원본 데이터에 액세스할 필요가 없으며 로그 마이닝 자격 증명이 고객 Oracle 테이블에 대한 SELECT 권한을 부여하지 않는지 확인하여 보호됩니다.  
  
### <a name="protection-of-source-oracle-change-data"></a>원본 Oracle 변경 데이터의 보호  
 Oracle CDC Service에는 Oracle 데이터베이스의 테이블에 대해 서비스 캡처 변경을 수행할 수 있도록 허용하는 로그 마이닝 자격 증명이 제공됩니다. 변경 데이터에는 일반 테이블에 있는 세부적인 액세스 권한이 없으므로 변경 데이터 액세스는 기본 제공된 Oracle 데이터 액세스 컨트롤을 무시합니다.  
  
 CDC 데이터베이스에는 캡처된 원본 Oracle 테이블과 동일한 스키마와 테이블 이름을 사용하는 빈 미러 테이블이 있습니다. 캡처된 데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 캡처 인스턴스에 저장되며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 캡처된 변경 내용에 제공하는 것과 동일한 보호를 제공합니다. 캡처 인스턴스와 연결된 변경 데이터에 액세스하려면 연결된 미러 테이블의 캡처된 모든 열에 대한 선택 액세스 권한을 사용자에게 부여해야 합니다. 또한 캡처 인스턴스를 만들 때 제어 역할을 지정한 경우 호출자도 지정된 제어 역할의 멤버여야 합니다. 반환된 메타데이터에 대한 액세스는 기본 원본 테이블에 대한 선택 액세스 권한을 사용하거나 정의된 제어 역할의 멤버 자격을 통해 일반적으로 제어되지만, 메타데이터에 액세스하기 위한 다른 일반적인 변경 데이터 캡처 함수에 대해서는 모든 데이터베이스 사용자가 public 역할을 통해 액세스할 수 있습니다.  
  
 따라서 **sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할이 있는 사용자는 기본적으로 캡처된 데이터에 대해 모든 권한이 있으며, 제어 역할을 통하거나 캡처된 열에 선택 액세스를 부여하여 추가 액세스 권한을 부여받을 수 있습니다.  
  
### <a name="protection-of-source-oracle-log-mining-credentials"></a>원본 Oracle 로그 마이닝 자격 증명의 보호  
 CDC 데이터베이스(cdc.xdbcdc_config 테이블)에 저장된 Oracle CDC Service 구성에는 로그 마이닝 사용자 이름 및 관련 암호가 포함됩니다.  
  
 로그 마이닝 암호는 다음 명령을 통해 자동으로 만들어지는 고정 이름 `xdbcdc_asym_key` 와 함께 비대칭 키를 사용하여 암호화된 상태로 저장됩니다.  
  
```sql
USE [<cdc-database-name>]  
CREATE ASYMMETRIC KEY xdbcdc_asym_key  
    WITH ALGORITHM = RSA_1024  
    ENCRYPTION BY PASSWORD = '<cdc-database-name><asym-key-password>'  
  
```  
  
 다른 알고리즘을 사용할 경우 이 키를 삭제할 수 있으며 동일한 암호로 암호화된 동일한 이름의 새 키를 만들 수 있습니다.  
  
 비대칭 키 암호는 레지스트리의 **HKLM\Software\Microsoft\XDBCDCSVC\\<service-name>** 경로에 저장되는 마스터 암호입니다. 로컬 관리자 및 Oracle CDC Windows 서비스 계정만 해당 키에 액세스할 수 있습니다. 키에는 비대칭 키 암호를 저장하는 암호화된 이진 값 **AsymmetricKeyPassword** 가 들어 있습니다. Oracle 로그 마이닝 자격 증명에 액세스하려면 이 레지스트리 키에 액세스해야 합니다.  
  
 ENCRYPTION BY PASSWORD 절을 사용하려면 암호는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 컴퓨터의 Windows 암호 정책 요구 사항을 따라야 합니다. 이 작업은 해당 정책에 따라 비대칭 키 암호를 선택하여 수행됩니다.  
  
 비대칭 키 암호를 잃어버린 경우 Oracle CDC Service 디자이너에서 각 Oracle CDC 인스턴스에 대한 로그 마이닝 자격 증명을 다시 지정해야 합니다.  
  
 CDC Service에서 이 비대칭 키가 없는 Oracle 인스턴스 CDC 데이터베이스를 발견하거나 키가 존재하지만 암호가 일치하지 않는 경우 CDC 데이터베이스에서 비대칭 키가 자동으로 만들어집니다.  
  
### <a name="oracle-cdc-service-windows-service-account"></a>Oracle CDC Service Windows 서비스 계정  
 Oracle CDC Windows 서비스에 사용하는 서비스 계정에는 추가 권한이 필요 없습니다. 이 계정은 Oracle Native Client API와 SQL Server Native Client ODBC API를 모두 사용할 수 있어야 합니다. 또한 레지스트리에서 서비스 구성 키에 액세스할 수 있어야 합니다(이 CDC Service 구성 콘솔에서 해당 작업에 대한 ACL이 설정됨).  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [고가용성 지원](../../integration-services/change-data-capture/high-availability-support.md)  
  
-   [SQL Server 연결 CDC Service에 필요한 권한](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
-   [사용자 역할](../../integration-services/change-data-capture/user-roles.md)  
  
-   [Oracle CDC Service 작업](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md)  
  
## <a name="see-also"></a>참고 항목  
 [로컬 CDC Service를 관리하는 방법](../../integration-services/change-data-capture/how-to-manage-a-local-cdc-service.md)   
 [Oracle CDC Service 관리](../../integration-services/change-data-capture/manage-an-oracle-cdc-service.md)  
  
  
