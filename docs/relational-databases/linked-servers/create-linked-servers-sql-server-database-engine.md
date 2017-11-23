---
title: "연결된 서버 만들기(SQL Server 데이터베이스 엔진) | Microsoft 문서"
ms.custom: 
ms.date: 11/20/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linked-servers
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.linkedserver.properties.general.f1
- sql13.swb.linkedserver.properties.security.f1
- sql13.swb.linkedserver.properties.provider.f1
- sql13.swb.linkedserver.properties.options.f1
helpviewer_keywords: linked servers [SQL Server], creating
ms.assetid: 3228065d-de8f-4ece-a9b1-e06d3dca9310
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: ba9740868c30bcc587cae0f99411bd6a49276fc1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="create-linked-servers-sql-server-database-engine"></a>연결된 서버 만들기(SQL Server 데이터베이스 엔진)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > 이전 버전의 SQL Server와 관련 된 콘텐츠를 참조 하십시오. [연결된 서버 만들기(SQL Server 데이터베이스 엔진)](https://msdn.microsoft.com/en-US/library/ff772782(SQL.120).aspx)합니다.

  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 연결된 서버를 만들고 다른 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 데이터에 액세스하는 방법을 보여 줍니다. 연결된 서버를 만들면 여러 원본의 데이터로 작업할 수 있습니다. 연결된 서버는 반드시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다른 인스턴스일 필요는 없지만 이것이 일반적인 시나리오입니다.  
  
##  <a name="Background"></a> 배경  
 연결된 서버를 만들면 OLE DB 데이터 원본과 유형이 다른 분산 쿼리에 액세스할 수 있습니다. 연결된 서버를 만든 후 이 서버에 대해 분산 쿼리를 실행할 수 있으며 쿼리로 둘 이상의 데이터 원본의 테이블을 조인할 수 있습니다. 연결된 서버를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 정의한 경우에는 원격 저장 프로시저를 실행할 수 있습니다.  
  
 연결된 서버의 기능 및 필수 인수는 크게 다를 수 있습니다. 이 항목의 예에서는 일반적인 예제를 제공하지만 모든 옵션에 대해 설명하지는 않습니다. 자세한 내용은 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)의 데이터에 액세스하는 방법을 보여 줍니다.  
  
##  <a name="Security"></a> 보안  
  
### <a name="permissions"></a>사용 권한  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용할 때는 서버에 대한 **ALTER ANY LINKED SERVER** 권한 또는 **setupadmin** 고정 서버 역할의 멤버 자격이 필요합니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 사용할 때는 **CONTROL SERVER** 권한 또는 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
##  <a name="Procedures"></a> 방법: 연결된 서버 만들기  
 다음 중 하나를 사용할 수 있습니다.  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 SQL Server의 다른 인스턴스에 연결된 서버를 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 열고 **서버 개체**를 확장한 다음 **연결된 서버**를 마우스 오른쪽 단추로 클릭하고 **새 연결된 서버**를 클릭합니다.  
  
2.  **일반** 페이지의 **연결된 서버** 상자에 연결하려는 **SQL Server** 인스턴스의 이름을 입력합니다.  
  
     **SQL Server**  
     연결된 서버를 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스로 식별합니다. 이 방법을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결된 서버를 정의하는 경우 **연결된 서버** 에 지정된 이름은 서버의 네트워크 이름이어야 합니다. 또한 서버에서 검색된 모든 테이블은 연결된 서버에 로그인할 수 있도록 정의된 기본 데이터베이스에 있어야 합니다.  
  
     **기타 데이터 원본**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이외의 OLE DB 서버 유형을 지정합니다. 이 옵션을 클릭하면 그 아래의 옵션이 활성화됩니다.  
  
     **공급자**  
     목록 상자에서 OLE DB 데이터 원본을 선택합니다. OLE DB 공급자는 레지스트리에 지정된 PROGID로 등록됩니다.  
  
     **제품 이름**  
     연결된 서버로 추가할 OLE DB 데이터 원본의 제품 이름을 입력합니다.  
  
     **데이터 원본**  
     OLE DB 공급자가 해석할 데이터 원본 이름을 입력합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결하는 경우에는 인스턴스 이름을 입력합니다.  
  
     **공급자 문자열**  
     데이터 원본에 해당하는 OLE DB 공급자의 고유한 PROGID(프로그래밍 ID)를 입력합니다. 올바른 공급자 문자열의 예는 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)의 데이터에 액세스하는 방법을 보여 줍니다.  
  
     **위치**  
     OLE DB 공급자가 해석할 데이터베이스 위치를 입력합니다.  
  
     **Catalog**  
     OLE DB 공급자에 연결할 때 사용할 카탈로그 이름을 입력합니다.  
  
     연결된 서버와의 연결을 테스트하려면 개체 탐색기에서 연결된 서버를 마우스 오른쪽 단추로 클릭한 다음 **연결 테스트**를 클릭합니다.  
  
    > [!NOTE]  
    >  **SQL Server** 인스턴스가 기본 인스턴스인 경우 **SQL Server**인스턴스를 호스팅하는 컴퓨터의 이름을 입력합니다. **SQL Server** 가 명명된 인스턴스인 경우 **Accounting\SQLExpress**와 같이 컴퓨터의 이름과 인스턴스의 이름을 입력합니다.  
  
3.  **서버 유형** 영역에서 연결된 서버가 **SQL Server** 의 다른 인스턴스임을 나타낼 수 있도록 **SQL Server**를 선택합니다.  
  
4.  **보안** 페이지에서 원본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결을 연결된 서버에 연결할 때 사용할 보안 컨텍스트를 지정합니다. 사용자가 도메인 로그인을 사용하여 연결하는 도메인 환경에서는 **로그인의 현재 보안 컨텍스트를 사용하여 연결** 을 선택하는 것이 이상적입니다. 사용자가 **SQL Server** 로그인을 사용하여 원본 **SQL Server** 에 연결하는 경우에는 **다음 보안 컨텍스트를 사용하여 연결**을 선택한 다음 연결된 서버에서 인증하기 위해 필요한 자격 증명을 제공하는 것이 이상적입니다.  
  
     **로컬 로그인**  
     연결된 서버에 연결할 수 있는 로컬 로그인을 지정합니다. 로컬 로그인은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 로그인이나 Windows 인증 로그인 중 하나일 수 있습니다. 이 목록을 사용하여 특정 로그인에 대한 연결을 제한하거나 일부 로그인이 다른 로그인으로 연결하도록 허용할 수 있습니다.  
  
     **Impersonate**  
     사용자 이름과 암호를 로컬 로그인에서 연결된 서버로 전달합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증의 경우 이름과 암호가 완전히 동일한 로그인이 원격 서버에 있어야 합니다. Windows 로그인의 경우 로그인이 연결된 서버에서 유효한 로그인이어야 합니다.  
  
     가장을 사용하려면 구성이 위임 요구 사항을 만족해야 합니다.  
  
     **원격 사용자**  
     원격 사용자를 사용하여 **로컬 로그인**에 정의되어 있지 않은 사용자를 매핑합니다. **원격 사용자** 는 원격 서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인이어야 합니다.  
  
     **원격 암호**  
     원격 사용자의 암호를 지정합니다.  
  
     **추가**  
     새 로컬 로그인을 추가합니다.  
  
     **제거**  
     기존 로컬 로그인을 제거합니다.  
  
     **연결 안 함**  
     목록에 정의되어 있지 않은 로그인의 경우 연결하지 않도록 지정합니다.  
  
     **보안 컨텍스트 없이 연결**  
     목록에 정의되어 있지 않은 로그인의 경우 보안 컨텍스트를 사용하지 않고 연결하도록 지정합니다.  
  
     **로그인의 현재 보안 컨텍스트를 사용하여 연결**  
     목록에 정의되어 있지 않은 로그인의 경우 로그인의 현재 보안 컨텍스트를 사용하여 연결하도록 지정합니다. Windows 인증을 사용하여 로컬 서버에 연결한 경우 원격 서버에 연결하는 데 해당 Windows 자격 증명이 사용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 로컬 서버에 연결한 경우 원격 서버에 연결하는 데 로그인 이름 및 암호가 사용됩니다. 이 경우 이름과 암호가 완전히 동일한 로그인이 원격 서버에 있어야 합니다.  
  
     **다음 보안 컨텍스트를 사용하여 연결**  
     목록에 정의되어 있지 않은 로그인의 경우 **원격 로그인** 및 **암호** 상자에서 지정한 로그인과 암호를 사용하여 연결하도록 지정합니다. 원격 로그인은 원격 서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인이어야 합니다.  
  
5.  필요에 따라 서버 옵션을 보거나 지정하려면 **서버 옵션**  페이지를 클릭합니다.  
  
     **데이터 정렬 호환**  
     연결된 서버에 대한 분산 쿼리 실행에 영향을 줍니다. 이 옵션을 true로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 연결된 서버의 모든 문자에 대한 문자 집합 및 데이터 정렬 시퀀스(또는 정렬 순서)가 로컬 서버와 호환된다고 가정합니다. 이렇게 함으로써 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 문자 열에 관한 비교를 공급자에 전달할 수 있습니다. 이 옵션을 설정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 항상 문자 열에 관한 비교를 로컬로 평가합니다.  
  
     이 옵션은 연결된 서버에 해당되는 데이터 원본이 로컬 서버와 동일한 문자 집합 및 정렬 순서를 갖고 있는 것이 확실한 경우에만 설정해야 합니다.  
  
     **데이터 액세스**  
     분산 쿼리 액세스에 대해 연결된 서버의 사용 여부를 설정합니다.  
  
     **RPC**  
     지정된 서버에서 RPC를 사용하도록 설정합니다.  
  
     **RPC 내보내기**  
     지정된 서버에 RPC를 사용하도록 설정합니다.  
  
     **원격 데이터 정렬 사용**  
     원격 열의 데이터 정렬을 사용할지 로컬 서버의 데이터 정렬을 사용할지 결정합니다.  
  
     true로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본에 대해서는 원격 열의 데이터 정렬이 사용되고[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 아닌 데이터 원본에 대해서는 데이터 정렬 이름에 지정된 데이터 정렬이 사용됩니다.  
  
     false로 설정하면 분산 쿼리에서 항상 로컬 서버의 기본 데이터 정렬을 사용하는 반면에 데이터 정렬 이름 및 원격 열의 데이터 정렬은 무시됩니다. 기본값은 false입니다.  
  
     **데이터 정렬 이름**  
     원격 데이터 정렬 사용이 true이고 데이터 원본이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본이 아닌 경우에 원격 데이터 원본에서 사용하는 데이터 정렬의 이름을 지정합니다. 이름은 반드시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원하는 데이터 정렬 중 하나여야 합니다.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 아닌 OLE DB 데이터 원본에 액세스할 때 해당 데이터 정렬이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬 중 하나와 일치하면 이 옵션을 사용하세요.  
  
     연결된 서버는 반드시 해당 서버의 모든 열에 대해 사용할 단일 데이터 정렬을 지원해야 합니다. 연결된 서버에서 단일 데이터 원본 내에 여러 데이터 정렬을 지원하거나 연결된 서버의 데이터 정렬이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬 중 하나와 일치하는지 확인할 수 없는 경우에는 이 옵션을 사용하지 않습니다.  
  
     **연결 제한 시간**  
     연결된 서버에 연결하는 제한 시간 값(초)입니다.  
  
     0으로 설정하면 **sp_configure** 의 기본값인 [원격 로그인 제한 시간](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md) 옵션 값을 사용합니다.  
  
     **쿼리 제한 시간**  
     연결된 서버에 대한 쿼리의 제한 시간 값(초)입니다.  
  
     0으로 설정하면 **sp_configure** 의 기본값인 [원격 쿼리 제한 시간](../../database-engine/configure-windows/configure-the-remote-query-timeout-server-configuration-option.md) 옵션 값을 사용합니다.  
  
     **RPC에 대한 분산 트랜잭션 승격 설정**  
     이 옵션을 사용하여 MS DTC( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator) 트랜잭션을 통해 서버 간 프로시저 동작을 보호할 수 있습니다. 이 옵션이 TRUE인 경우 원격 저장 프로시저를 호출하면 분산 트랜잭션이 시작되고 MS DTC를 사용하여 이 트랜잭션을 참여시킵니다. 자세한 내용은 [sp_serveroption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)의 데이터에 액세스하는 방법을 보여 줍니다.  
  
6.  **확인**을 클릭합니다.  
  
##### <a name="to-view-the-provider-options"></a>공급자 옵션을 보려면  
  
-   공급자를 사용할 수 있도록 설정하는 옵션을 보려면 **공급자 옵션** 페이지를 클릭합니다.  
  
     공급자마다 사용 가능한 옵션은 다릅니다. 예를 들어 일부 데이터 형식에는 사용 가능한 인덱스가 있지만 사용 가능한 인덱스가 없는 데이터 형식도 있습니다. 이 대화 상자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서의 공급자 기능을 이해할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 몇 가지 일반 데이터 공급자를 설치하는데, 데이터를 공급하는 제품이 변경되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 설치한 공급자가 모든 최신 기능을 지원하지 않을 수 있습니다. 데이터를 공급하는 제품 기능에 대한 가장 유용한 정보는 해당 제품 설명서에서 제공합니다.  
  
     **동적 매개 변수**  
     공급자에서 매개 변수가 있는 쿼리에 대해 '?' 매개 변수 표식 구문을 허용한다는 것을 나타냅니다. 이 옵션은 공급자가 **ICommandWithParameters** 인터페이스를 지원하고 '?'를 매개 변수 표식으로 지원하는 경우에만 설정합니다. 이 옵션을 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 공급자에 대해 매개 변수가 있는 쿼리를 실행할 수 있습니다. 공급자에 대해 매개 변수가 있는 쿼리를 실행할 수 있는 기능으로 인해 특정 쿼리의 경우 성능이 향상될 수 있습니다.  
  
     **중첩 쿼리**  
     공급자가 FROM 절의 `SELECT` 중첩문을 허용함을 나타냅니다. 이 옵션을 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 FROM 절의 SELECT 중첩문을 요청하는 공급자에게 특정 쿼리를 위임할 수 있습니다.  
  
     **0 수준만**  
     공급자에 대해 수준 0 OLE DB 인터페이스만 호출됩니다.  
  
     **Inprocess 허용**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 공급자가 in-process 서버로 인스턴스화될 수 있습니다. 이 옵션을 설정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 외부에서 공급자를 인스턴스화하는 것이 기본 동작입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 외부에서 공급자를 인스턴스화하면 공급자 오류로부터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스를 보호할 수 있습니다. 공급자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 외부에서 인스턴스화되면 긴 열(**text**, **ntext**또는 **image**)을 참조하는 업데이트나 삽입은 허용되지 않습니다.  
  
     **트랜잭션되지 않은 업데이트**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 **ITransactionLocal** 을 사용할 수 없는 경우에도 업데이트를 허용합니다. 이 옵션을 사용하면 공급자가 트랜잭션을 지원하지 않으므로 공급자에 대한 업데이트를 복구할 수 없습니다.  
  
     **액세스 경로인 인덱스**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 공급자 인덱스를 사용하여 데이터를 인출하려고 합니다. 기본적으로 인덱스는 메타데이터에만 사용되며 열리지 않습니다.  
  
     **임시 액세스 허용 안 함**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 OLE DB 공급자에 대해 OPENROWSET 및 OPENDATASOURCE 함수를 통한 임시 액세스를 허용하지 않습니다. 이 옵션을 설정하지 않은 경우에도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 임시 액세스를 허용하지 않습니다.  
  
     **'LIKE' 연산자를 지원합니다.**  
     공급자가 LIKE 키워드를 사용하는 쿼리를 지원한다는 것을 나타냅니다.  
  
###  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 연결된 서버를 만들려면 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)[CREATE LOGIN&#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md) 및 [sp_addlinkedsrvlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md) 문을 사용합니다.  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-transact-sql"></a>Transact-SQL을 사용하여 SQL Server의 다른 인스턴스에 연결된 서버 만들기  
  
1.  쿼리 편집기에서 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 입력하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 명명된 `SRVR002\ACCTG`인스턴스에 연결합니다.  
  
    ```tsql  
    USE [master]  
    GO  
    EXEC master.dbo.sp_addlinkedserver   
        @server = N'SRVR002\ACCTG',   
        @srvproduct=N'SQL Server' ;  
    GO  
  
    ```  
  
2.  다음 코드를 실행하여 연결된 서버에서 연결된 서버를 사용하는 로그인의 도메인 자격 증명을 사용하도록 구성합니다.  
  
    ```tsql  
    EXEC master.dbo.sp_addlinkedsrvlogin   
        @rmtsrvname = N'SRVR002\ACCTG',   
        @locallogin = NULL ,   
        @useself = N'True' ;  
    GO  
  
    ```  
  
##  <a name="FollowUp"></a> 추가 작업: 연결된 서버를 만든 후 수행할 단계  
  
#### <a name="to-test-the-linked-server"></a>연결된 서버 테스트  
  
-   다음 코드를 실행하여 연결된 서버에 대한 연결을 테스트합니다. 이 예에서는 연결된 서버의 데이터베이스 이름을 반환합니다.  
  
    ```tsql  
    SELECT name FROM [SRVR002\ACCTG].master.sys.databases ;  
    GO  
  
    ```  
  
#### <a name="writing-a-query-that-joins-tables-from-a-linked-server"></a>연결된 서버의 테이블을 조인하는 쿼리 작성  
  
-   네 부분으로 이루어진 이름을 사용하여 연결된 서버의 개체를 참조합니다. 다음 코드를 실행하면 로컬 서버의 모든 로그인 및 연결된 서버에서 이와 일치하는 로그인의 목록이 반환됩니다.  
  
    ```tsql  
    SELECT local.name AS LocalLogins, linked.name AS LinkedLogins  
    FROM master.sys.server_principals AS local  
    LEFT JOIN [SRVR002\ACCTG].master.sys.server_principals AS linked  
        ON local.name = linked.name ;  
    GO  
    ```  
  
     연결된 서버에 대해 NULL이 반환되면 로그인이 연결된 서버에 없음을 의미합니다. 이러한 로그인은 연결된 서버가 다른 보안 컨텍스트를 통과시키거나 연결된 서버가 익명 연결을 허용하도록 구성되어야 연결된 서버를 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [연결된 서버&#40;데이터베이스 엔진&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)  
  
  
