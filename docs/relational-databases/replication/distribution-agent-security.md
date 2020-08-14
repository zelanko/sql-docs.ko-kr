---
title: 배포 에이전트 보안 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.DA.f1
helpviewer_keywords:
- Distribution Agent Security dialog box
ms.assetid: de40cc21-2e58-4464-9be7-b5b90c925e9b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 3322ef185178ab2254066281d9f6f6a6c85611da
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87862992"
---
# <a name="distribution-agent-security"></a>배포 에이전트 보안
::: moniker range=">=sql-server-2016||=sqlallproducts-allversions" 
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
**배포 에이전트 보안** 대화 상자를 사용하여 배포 에이전트를 실행하는 Windows 계정을 지정할 수 있습니다. 배포 에이전트는 밀어넣기 구독을 위한 배포자 또는 끌어오기 구독을 위한 구독자에서 실행됩니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정으로 에이전트 프로세스가 실행되기 때문에 이 계정을 *프로세스 계정*이라고도 합니다. 이 대화 상자에서 사용 가능한 추가 옵션은 대화 상자에 액세스하는 방법에 따라 달라집니다.  
  
-   새 구독 마법사에서 이 대화 상자에 액세스하는 경우 배포 에이전트를 구독자(밀어넣기 구독의 경우) 또는 배포자(끌어오기 구독의 경우)에 연결하는 컨텍스트도 지정할 수 있습니다. Windows 계정을 가장하거나 지정한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정의 컨텍스트에서 연결을 설정할 수 있습니다.  
  
-   **구독 속성** 대화 상자에서 이 대화 상자에 액세스하는 경우 해당 대화 상자의**구독자 연결**또는 **배포자 연결** 행의 속성 단추 ( **...** )를 클릭하여 배포 에이전트를 연결하는 컨텍스트를 지정합니다. **구독 속성** 대화 상자에 액세스하는 방법은 [밀어넣기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) 및 방법: [끌어오기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)을 참조하세요.  
  
 모든 계정이 유효해야 하며 각 계정에 대해 올바른 암호를 지정해야 합니다. 계정 및 암호의 유효성은 에이전트를 실행할 때 검사합니다.  
  
## <a name="options"></a>옵션  
 **Process Account**  
 배포 에이전트를 실행하는 Windows 계정을 입력합니다.  
  
-   밀어넣기 구독의 경우 계정이 다음 조건을 만족해야 합니다.  
  
    -   적어도 배포 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
    -   PAL(게시 액세스 목록)의 멤버여야 합니다.  
  
    -   스냅샷 공유에 대해 읽기 권한이 있어야 합니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자에 대한 구독인 경우에는 구독자에 대한 OLE DB 공급자의 설치 디렉터리에 대해 읽기 권한이 있어야 합니다.  
  
-   끌어오기 구독의 경우 계정이 적어도 구독 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
 연결을 설정할 때 프로세스 계정을 가장하면 추가 사용 권한이 필요합니다. 아래의 **배포자에 연결** 및 **구독자에 연결** 섹션을 참조하십시오.  
  
 배포 에이전트가 **인스턴스에서 실행되지 않기 때문에** [!INCLUDE[msCoName](../../includes/msconame-md.md)]에 대한 끌어오기 구독에 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]프로세스 계정[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]을 지정할 수 없습니다.  
  
 **암호** 및 **암호 확인**  
 Windows 계정의 암호를 입력합니다.  
  
 **배포자에 연결**  
 밀어넣기 구독의 경우 항상 **프로세스 계정** 입력란에 지정한 계정을 가장하여 배포자에 연결합니다.  
  
 끌어오기 구독의 경우 배포 에이전트를 배포자에 연결할 때 **프로세스 계정** 입력란에 지정한 계정을 가장할지, 아니면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용할지를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용하도록 선택한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인과 암호를 입력합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용하는 것보다 Windows 계정을 가장하도록 선택하는 것이 좋습니다.  
  
 연결에 사용할 Windows 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정은 다음 조건을 만족해야 합니다.  
  
-   PAL의 멤버여야 합니다.  
  
-   스냅샷 공유에 대해 읽기 권한이 있어야 합니다.  
  
 **구독자에 연결**  
 끌어오기 구독의 경우 항상 **프로세스 계정** 입력란에 지정한 계정을 가장하여 구독자에 연결합니다.  
  
 밀어넣기 구독의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자 및[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자에 대한 옵션이 다음과 같이 다릅니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자의 경우 배포 에이전트를 구독자에 연결할 때 **프로세스 계정** 입력란에 지정한 계정을 가장할지, 아니면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용할지를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용하도록 선택한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인과 암호를 입력합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용하는 것보다 Windows 계정을 가장하도록 선택하는 것이 좋습니다.  
  
     구독자 연결에 사용되는 Windows 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정은 적어도 구독 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자의 경우 배포 에이전트를 구독자에 연결할 때 사용할 데이터베이스 로그인을 구독자에서 지정합니다. 해당 로그인에는 구독 데이터베이스에서 개체를 만들 권한이 있어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자에 대한 자세한 내용은 [SQL Server 이외 구독자에 대한 구독 만들기](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)를 참조하세요.  
  
 **추가 연결 옵션**  
 이 옵션은[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자에 대해서만 사용할 수 있습니다. 연결 문자열 형식으로 구독자에 대한 연결 옵션을 지정하십시오. Oracle에서는 추가 옵션을 지정할 필요가 없습니다. 각 옵션은 세미콜론으로 구분해야 합니다. 다음은 IBM DB2 연결 문자열의 예입니다. 이 예에서는 읽기 쉽도록 줄 바꿈을 넣었습니다.  
  
```  
Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
Persist Security Info=False;Connection Pooling=True;  
```  
  
 이 문자열의 옵션 대부분은 구성 중인 DB2 서버와만 관련이 있지만 **Process Binary as Character** 옵션은 항상 **False**로 설정해야 합니다. 구독 데이터베이스를 식별하려면 **Initial Catalog** 옵션 값을 지정해야 합니다. 자세한 내용은 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [복제에 대한 ID 및 액세스 제어](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [복제 에이전트 개요](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
::: moniker-end
  
::: monikerRange="azuresqldb-mi-current"
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
**배포 에이전트 보안** 대화 상자를 사용하여 배포 에이전트를 실행할 SQL 인증 계정을 지정할 수 있습니다. 배포 에이전트는 밀어넣기 구독을 위한 배포자 또는 끌어오기 구독을 위한 구독자에서 실행됩니다.  이 대화 상자에서 사용 가능한 추가 옵션은 대화 상자에 액세스하는 방법에 따라 달라집니다.  
  
-   새 구독 마법사에서 이 대화 상자에 액세스하는 경우 배포 에이전트를 구독자(밀어넣기 구독의 경우) 또는 배포자(끌어오기 구독의 경우)에 연결하는 컨텍스트도 지정할 수 있습니다. SQL Server 인증 계정을 사용하여 연결해야 합니다. 
  
-   **구독 속성** 대화 상자에서 이 대화 상자에 액세스하는 경우 해당 대화 상자의**구독자 연결**또는 **배포자 연결** 행의 속성 단추 ( **...** )를 클릭하여 배포 에이전트를 연결하는 컨텍스트를 지정합니다. **구독 속성** 대화 상자에 액세스하는 방법은 [밀어넣기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) 및 방법: [끌어오기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)을 참조하세요.  
  
 모든 계정이 유효해야 하며 각 계정에 대해 올바른 암호를 지정해야 합니다. 계정 및 암호의 유효성은 에이전트를 실행할 때 검사합니다.  
  
## <a name="options"></a>옵션  
 **Process Account**  
 배포 에이전트를 실행할 SQL Server 인증 계정을 입력합니다.  
  
-   밀어넣기 구독의 경우 계정이 다음 조건을 만족해야 합니다.  
  
    -   적어도 배포 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
    -   PAL(게시 액세스 목록)의 멤버여야 합니다.  
  
    -   스냅샷 공유에 대해 읽기 권한이 있어야 합니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자에 대한 구독인 경우에는 구독자에 대한 OLE DB 공급자의 설치 디렉터리에 대해 읽기 권한이 있어야 합니다.  
  
-   끌어오기 구독의 경우 계정이 적어도 구독 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
    
**암호** 및 **암호 확인**  
Windows 계정의 암호를 입력합니다.  
  
**배포자에 연결**  
밀어넣기 구독의 경우 항상 **프로세스 계정** 입력란에 지정한 계정을 가장하여 배포자에 연결합니다.  
  
끌어오기 구독의 경우 배포 에이전트를 배포자에 연결할 때 **프로세스 계정** 텍스트 상자에 지정한 계정을 가장할지, 아니면 SQL Server 인증 계정을 사용할지를 선택합니다. 
  
  
 **구독자에 연결**  
 끌어오기 구독의 경우 항상 **프로세스 계정** 입력란에 지정한 계정을 가장하여 구독자에 연결합니다.  
  
 밀어넣기 구독의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자 및[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자에 대한 옵션이 다음과 같이 다릅니다.

  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자의 경우 배포 에이전트를 구독자에 연결할 때 사용할 데이터베이스 로그인을 구독자에서 지정합니다. 해당 로그인에는 구독 데이터베이스에서 개체를 만들 권한이 있어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자에 대한 자세한 내용은 [SQL Server 이외 구독자에 대한 구독 만들기](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)를 참조하세요.  
  
 **추가 연결 옵션**  
 이 옵션은[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자에 대해서만 사용할 수 있습니다. 연결 문자열 형식으로 구독자에 대한 연결 옵션을 지정하십시오. Oracle에서는 추가 옵션을 지정할 필요가 없습니다. 각 옵션은 세미콜론으로 구분해야 합니다. 다음은 IBM DB2 연결 문자열의 예입니다. 이 예에서는 읽기 쉽도록 줄 바꿈을 넣었습니다.  
  
```  
Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
Persist Security Info=False;Connection Pooling=True;  
```  
  
 이 문자열의 옵션 대부분은 구성 중인 DB2 서버와만 관련이 있지만 **Process Binary as Character** 옵션은 항상 **False**로 설정해야 합니다. 구독 데이터베이스를 식별하려면 **Initial Catalog** 옵션 값을 지정해야 합니다. 자세한 내용은 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Azure SQL Database를 사용하여 트랜잭션 복제](/azure/sql-database/sql-database-managed-instance-transactional-replication) [Azure SQL Managed Instance의 복제 구성](/azure/sql-database/replication-with-sql-database-managed-instance)
::: moniker-end


