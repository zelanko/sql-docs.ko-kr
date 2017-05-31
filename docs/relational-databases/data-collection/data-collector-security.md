---
title: "데이터 수집기 보안 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data collection [SQL Server]
- security [data collector]
- data collector [SQL Server], security
ms.assetid: e75d6975-641e-440a-a642-cb39a583359a
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d5b90faa09f6185ffe5e273e43707bc9dc2dc1c0
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="data-collector-security"></a>데이터 수집기 보안
  데이터 수집기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 구현하는 역할 기반 보안 모델을 사용합니다. 이 모델을 사용하면 데이터베이스 관리자가 해당 태스크를 수행하는 데 반드시 필요한 사용 권한만 있는 보안 컨텍스트에서 다양한 데이터 수집기 태스크를 실행할 수 있습니다. 이 방법은 저장 프로시저 또는 뷰를 사용해야만 액세스할 수 있는 내부 테이블 관련 작업에도 사용됩니다. 내부 테이블에 대한 사용 권한이 부여되지 않는 대신, 해당 테이블에 액세스하는 데 사용되는 저장 프로시저 또는 뷰의 사용자에 대해 사용 권한을 확인합니다.  
  
> [!IMPORTANT]  
>  이 보안 모델의 다른 핵심 요소는 공통적 사용 권한입니다. 공통적 사용 권한에서는 개체(예: 경고, 운영자, 작업, 일정 및 프록시)에 대해 사용 권한이 많은 역할이 사용 권한이 적은 역할의 사용 권한을 상속받습니다. 자세한 내용은 [SQL Server Agent Fixed Database Roles](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)을 참조하세요.  
  
 다음 섹션에서는 일반적인 데이터 컬렉션 보안을 비롯하여 데이터 수집기를 구성 및 사용하고 관리 데이터 웨어하우스 관련 태스크를 수행할 수 있도록 사용자에게 부여해야 하는 역할에 대해 설명합니다.  
  
## <a name="general-security"></a>일반 보안  
 데이터 수집기는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 대해 지정된 문서화된 표준에 따라 설치됩니다.  
  
### <a name="network-security"></a>네트워크 보안  
 대상 인스턴스, 구성 서버와 연결된 관계형 인스턴스, 실행 중인 컬렉션 집합 및 관리 데이터 웨어하우스를 호스팅하는 서버 간에 중요한 정보를 전달할 수 있습니다.  
  
 네트워크를 통해 전송되는 데이터를 보호하기 위해 [!INCLUDE[tsql](../../includes/tsql-md.md)]에 대한 프로토콜 암호화와 같은 표준 보안 메커니즘이 구현됩니다.  
  
## <a name="permissions-for-configuring-and-using-the-data-collector"></a>데이터 수집기 구성 및 사용 권한  
 태스크에 따라 사용자는 데이터 수집기에 대해 제공된 하나 이상의 고정 데이터베이스 역할의 멤버여야 합니다. 역할은 액세스 권한이 많은 것부터 적은 순서대로 다음과 같습니다.  
  
-   **dc_admin**  
  
-   **dc_operator**  
  
-   **dc_proxy**  
  
 이러한 역할은 msdb 데이터베이스에 저장됩니다. 기본적으로 사용자는 이러한 데이터베이스 역할의 멤버가 아닙니다. 이러한 역할의 사용자 멤버 자격은 명시적으로 부여되어야 합니다.  
  
 **sysadmin** 고정 서버 역할의 멤버인 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 개체 및 데이터 수집기 뷰에 대한 모든 액세스 권한을 가집니다. 단, 데이터 수집기 역할에 명시적으로 추가되어야 합니다.  
  
> [!IMPORTANT]  
>  db_ssisadmin 및 dc_admin 역할의 멤버는 해당 권한을 sysadmin으로 승격할 수 있습니다. 이러한 권한 승격이 발생할 수 있는 것은 이러한 역할이 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 수정할 수 있고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 sysadmin 보안 컨텍스트를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 패키지를 실행할 수 있기 때문입니다. 유지 관리 계획, 데이터 컬렉션 집합 및 기타 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 실행할 때 이러한 권한 상승이 발생하지 않도록 하려면 패키지를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업이 제한된 권한을 갖는 프록시 계정을 사용하도록 구성하거나 db_ssisadmin 및 dc_admin 역할에 sysadmin 멤버만 추가합니다.  
  
### <a name="dcadmin-role"></a>dc_admin 역할  
 **dc_admin** 역할에 할당된 사용자는 서버 인스턴스의 데이터 수집기 구성에 대한 모든 관리자 권한(만들기, 읽기, 업데이트 및 삭제)을 갖습니다. 이 역할의 멤버는 다음 작업을 수행할 수 있습니다.  
  
-   수집기 수준 속성 설정  
  
-   새 컬렉션 집합 추가  
  
-   새 컬렉션 유형 설치  
  
-   **dc_operator** 역할에 허용된 모든 작업 수행  
  
 **dc_admin** 역할은 다음 역할의 멤버입니다.  
  
-   **SQLAgentUserRole**. 이 역할은 일정을 만들고 작업을 실행하기 위해 필요합니다.  
  
    > [!NOTE]  
    >  프록시가 필요한 작업 단계에서 프록시를 만들어 사용하려면 데이터 수집기에 대해 생성된 프록시가 **dc_admin** 에 액세스 권한을 부여해야 합니다.  
  
-   **dc_operator**. **dc_admin** 의 멤버는 **dc_operator**에 부여된 사용 권한을 상속받습니다.  
  
### <a name="dcoperator-role"></a>dc_operator 역할  
 **dc_operator** 역할의 멤버는 읽기 및 업데이트 권한을 갖습니다. 이 역할은 컬렉션 집합 실행 및 구성과 관련된 작업 태스크를 지원합니다. 이 역할의 멤버는 다음 작업을 수행할 수 있습니다.  
  
-   컬렉션 집합 시작 또는 중지  
  
-   기존 컬렉션 집합 열거  
  
-   컬렉션 항목 및 컬렉션 빈도와 같은 컬렉션 집합 관련 세부 정보 확인  
  
-   기존 컬렉션 집합의 업로드 빈도 변경  
  
-   기존 컬렉션 집합의 일부인 컬렉션 항목의 컬렉션 빈도 변경  
  
 **dc_operator** 역할은 데이터 수집기 패키지를 열거하고 보는 데 필요한 다음 역할의 멤버입니다.  
  
-   **db_ssisltduser**  
  
-   **db_ssisoperator**  
  
 자세한 내용은 [Integration Services 경로&#40;SSIS Service&#41;](../../integration-services/service/integration-services-roles-ssis-service.md)를 참조하세요.  
  
### <a name="dcproxy-role"></a>dc_proxy 역할  
 **dc_proxy** 역할의 멤버는 데이터 수집기 컬렉션 집합 및 수집기 수준 속성에 대한 읽기 권한을 갖습니다. 이 역할의 멤버는 자신이 소유하는 작업을 실행할 수 있으며 기존 프록시 계정으로 실행되는 작업 단계를 만들 수도 있습니다.  
  
 이 역할의 멤버는 다음 작업을 수행할 수 있습니다.  
  
-   컬렉션 항목에 대한 입력 매개 변수 및 이러한 항목의 컬렉션 빈도와 같은 컬렉션 집합 구성 정보 확인  
  
-   데이터 업로드에 사용되는 데이터 웨어하우스 연결 정보와 같이 서명된 저장 프로시저로만 액세스할 수 있는 암호화된 내부 정보 가져오기  
  
-   컬렉션 집합 런타임 이벤트 기록  
  
 **dc_proxy** 역할은 데이터 수집기 패키지를 열거하고 보는 데 필요한 다음 역할의 멤버입니다.  
  
-   **db_ssisltduser**.  
  
-   **db_ssisoperator**  
  
 자세한 내용은 [Integration Services 경로&#40;SSIS Service&#41;](../../integration-services/service/integration-services-roles-ssis-service.md)를 참조하세요.  
  
## <a name="permissions-for-configuring-and-using-the-management-data-warehouse"></a>관리 데이터 웨어하우스 구성 및 사용 권한  
 태스크에 따라 사용자는 관리 데이터 웨어하우스에 액세스하기 위해 제공된 하나 이상의 고정 데이터베이스 역할의 멤버여야 합니다. 역할은 액세스 권한이 많은 것부터 적은 순서대로 다음과 같습니다.  
  
-   **mdw_admin**  
  
-   **mdw_writer**  
  
-   **mdw_reader**  
  
 이러한 역할은 msdb 데이터베이스에 저장됩니다. 기본적으로 사용자는 이러한 데이터베이스 역할의 멤버가 아닙니다. 이러한 역할의 사용자 멤버 자격은 명시적으로 부여되어야 합니다.  
  
 **sysadmin** 고정 서버 역할의 멤버인 사용자는 데이터 수집기 뷰에 대한 모든 액세스 권한을 가집니다. 하지만 다른 작업을 수행하기 위한 데이터베이스 역할에 명시적으로 추가되어야 합니다.  
  
### <a name="mdwadmin-role"></a>mdw_admin 역할  
 **mdw_admin** 역할의 멤버는 관리 데이터 웨어하우스에 대한 읽기, 쓰기, 업데이트 및 삭제 권한을 갖습니다.  
  
 이 역할의 멤버는 다음 작업을 수행할 수 있습니다.  
  
-   새 컬렉션 유형 설치 시 새 테이블을 추가하는 것과 같이 필요 시 관리 데이터 웨어하우스 스키마 변경.  
  
    > [!NOTE]  
    >  스키마를 변경할 경우 새 수집기 유형 설치에 msdb의 데이터 수집기 구성에 대한 업데이트 권한이 필요하므로 해당 동작을 수행하려면 사용자가 **dc_admin** 역할의 멤버이기도 해야 합니다.  
  
-   관리 데이터 웨어하우스에 대한 보관 또는 정리와 같은 유지 관리 작업 실행  
  
### <a name="mdwwriter-role"></a>mdw_writer 역할  
 **mdw_writer** 역할의 멤버는 관리 데이터 웨어하우스에 데이터를 업로드하고 쓸 수 있습니다. 관리 데이터 웨어하우스에 데이터를 저장하는 모든 데이터 수집기는 이 역할의 멤버여야 합니다.  
  
### <a name="mdwreader-role"></a>mdw_reader 역할  
 **mdw_reader** 역할의 멤버는 관리 데이터 웨어하우스에 대한 읽기 권한을 갖습니다. 이 역할은 기록 데이터에 대한 액세스를 제공하여 문제 해결을 지원하기 위한 것이므로 이 역할의 멤버는 관리 데이터 웨어하우스 스키마의 다른 요소를 볼 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 에이전트 보안 구현](http://msdn.microsoft.com/library/d770d35c-c8de-4e00-9a85-7d03f45a0f0d)  
  
  
