---
title: "사용자 역할 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: be0ec384-e03b-4483-96ca-02b289804d6a
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3c302cecea6c443e97badeca3737211cdadec239
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="user-roles"></a>사용자 역할
  이 섹션에서는 Attunity Oracle CDC Service의 사용자 역할에 대해 설명합니다. 여기서 설명하는 역할은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 역할, Windows 역할 또는 Oracle 데이터베이스 역할입니다.  
  
## <a name="windows-user-roles"></a>Windows 사용자 역할  
 다음에서는 Oracle CDC Service에서 사용하는 Windows 사용자 역할에 대해 설명합니다.  
  
### <a name="computer-administrator-oracle-cdc-service"></a>컴퓨터 관리자: Oracle CDC Service  
 컴퓨터 관리자는 컴퓨터에서 CDC Service를 만들고 유지 관리하는 작업을 담당하는 Windows 사용자입니다. 이 사용자는 로컬 컴퓨터 관리자 그룹에 속해야 합니다.  
  
 Oracle CDC Service 컴퓨터 관리자가 수행하는 태스크는 다음과 같습니다.  
  
-   Oracle CDC Service 소프트웨어 설치  
  
-   Oracle CDC Windows 서비스 만들기  
  
-   대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 CDC Service 연결 설정(연결 문자열 및 자격 증명)  
  
-   Oracle 로그 마이닝 자격 증명을 보호하는 CDC Service 마스터 암호 확인  
  
-   CDC Service Windows 서비스 삭제  
  
-   Oracle CDC Service 소프트웨어 제거  
  
-   Oracle CDC Service 소프트웨어 유지 관리(예: 업데이트 설치)  
  
-   CDC Service Windows 서비스 시작 및 중지  
  
 Microsoft 장애 조치(failover) 클러스터와 같은 고가용성 구성에서 작업하는 경우 컴퓨터 관리자에게 다음과 같은 추가 책임과 권한이 있어야 합니다.  
  
-   모든 클러스터 노드에서 Oracle CDC Service 소프트웨어 설치 및 유지 관리  
  
-   다양한 클러스터 노드에서 CDC Service의 Windows 서비스에 대한 일반 클러스터 서비스 리소스 정의  
  
-   Oracle CDC Service가 설치되는 컴퓨터에서 관리자로 승인된 컴퓨터 관리자 역할 수행. 이 관리자는 Oracle CDC Service를 설치하고 CDC Service 구성 콘솔을 사용하여 로컬 컴퓨터에서 Oracle CDC Service를 구성합니다.  
  
### <a name="service-account-oracle-cdc-service"></a>서비스 계정: Oracle CDC Service  
 이 Oracle CDC Service Windows 서비스 계정은 Oracle CDC Service를 실행하는 데 사용하는 Windows 계정입니다(서비스 계정).  
  
 서비스 계정에 필요한 유일한 필수 권한은 Oracle 클라이언트와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 공급자를 사용할 수 있는 권한입니다. 이 계정은 특정 공급자에 필요하지 않은 한 파일에 액세스할 필요가 없습니다. 예를 들어, Oracle 클라이언트 연결 문자열이 **tnsnames.ora** 파일의 Oracle 데이터베이스 인스턴스를 참조하는 경우 서비스 계정은 해당 파일에 읽기 액세스 가능해야 합니다.  
  
 Windows Vista 또는 Windows Server 2008에서 Oracle CDC Service를 만드는 경우 기본 서비스 계정은 NETWORK SERVICE 계정입니다.  
  
 Windows 7, Windows Server 2008 R2 이상에서 기본 서비스 계정은 NT Service\\<service-name>입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 다른 컴퓨터에서 실행되거나 클러스터형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스이고 여기서 서비스가 Windows 인증을 사용하여 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결해야 하는 경우 서비스 계정은 도메인 계정이어야 합니다.  
  
## <a name="sql-server-user-roles"></a>SQL Server 사용자 역할  
 다음에서는 Oracle CDC Service에서 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 역할에 대해 설명합니다.  
  
### <a name="oracle-cdc-service-administrator"></a>Oracle CDC Service 관리자  
 CDC Service 관리자는 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 Oracle CDC Service 아티팩트를 완전히 제어할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자입니다. CDC Service 관리자는 Oracle CDC Designer 콘솔을 사용하여 Oracle CDC 인스턴스를 디자인합니다.  
  
 CDC Service 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고정 서버 역할 **public** 및 **dbcreator**를 부여받아야 합니다.  
  
 CDC Service 관리자가 수행하는 태스크는 다음과 같습니다.  
  
-   Oracle CDC 인스턴스( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스)를 호스트하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 준비. 이 태스크에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 MSXDBCDC라는 특수 데이터베이스가 만들어집니다.  
  
-   Oracle CDC 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 만들기. 태스크에는 새로 만든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 CDC에 대해 활성화하는 작업이 포함되며 이 작업에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자(**sysadmin**)가 필요합니다.  
  
-   Oracle CDC 인스턴스 디자인. 이 태스크에는 원본 Oracle 데이터베이스 및 캡처된 테이블에 대한 정보를 제공하는 작업이 포함되며 이 작업에는 Oracle 데이터베이스 관리자가 필요합니다.  
  
-   캡처 인스턴스 추가/제거 및 구성 업데이트를 비롯하여 시간 경과에 따른 Oracle CDC 인스턴스 유지 관리  
  
-   Oracle CDC 인스턴스 활성화 또는 비활성화  
  
-   Oracle CDC 인스턴스의 상태 모니터링  
  
-   Oracle CDC 인스턴스에 영향을 주는 문제 해결  
  
 CDC Service 관리자는 최소한 처음에는 Oracle CDC 인스턴스와 연결된 **CDC 데이터베이스의** db_owner [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고정 데이터베이스 역할에 속합니다. 이 역할은 CDC 데이터베이스에 저장된 변경 데이터에 대한 CDC Service 관리자 액세스 권한을 제공합니다. 역할을 만든 후에는 **인스턴스 준비 및 다른 Oracle CDC 인스턴스 만들기를 제외하고 위에 나열된 모든 태스크를 수행할 수 있는 다른 사용자에게 CDC 데이터베이스의** db_owner [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 역할을 할당할 수 있습니다.  
  
 CDC Service 관리자는 Oracle CDC Windows 서비스 생성 시 지정되는 마스터 암호를 알 필요가 없습니다.  
  
### <a name="system-administrator"></a>시스템 관리자  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자이며 Oracle CDC Service와 연결된 **인스턴스에서 고정 서버** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 역할을 부여받아야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자가 수행하는 Oracle CDC에 특정한 태스크는 단 하나이며 이 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC용 Oracle CDC 인스턴스에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 활성화하는 것입니다. 이 태스크는 새 Oracle CDC 인스턴스를 만들 때 Oracle CDC Designer 콘솔을 사용하여 수행됩니다.  
  
### <a name="oracle-cdc-service-user"></a>Oracle CDC Service 사용자  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC Service 사용자는 Oracle CDC Service에서 MSXDBCDC 및 이 서비스에서 처리되는 모든 Oracle CDC 인스턴스(CDC 데이터베이스)에 대한 작업을 수행하는 데 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC Service 사용자는 다음을 부여받아야 합니다.  
  
-   서버에서 처리되는 모든 CDC 데이터베이스에 대한 고정 데이터베이스 역할 **db_dlladmin**, **db_datareader**및 **db_datawriter** 의 멤버  
  
-   MSXDBCDC 데이터베이스에 대한 고정 데이터베이스 역할 **db_datareader** 및 **db_datawriter** 의 멤버  
  
 Oracle CDC Service는 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용하여 모든 CDC 데이터베이스와 MSXDBCDC 데이터베이스에 대해 작업하므로 이러한 모든 데이터베이스에서 이 로그인을 매핑해야 합니다.  
  
### <a name="oracle-cdc-change-consumer"></a>Oracle CDC 변경 소비자  
 Oracle CDC 변경 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 인스턴스 데이터베이스의 CDC 테이블에 저장된 변경 내용을 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자입니다.  
  
 이 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 인프라에서 생성된 CDC 기능을 통해 각 CDC 테이블에 액세스하는 데 필요한 사용자 역할을 결정합니다. 캡처 인스턴스를 지정할 때 사용자 역할을 지정하지 않으면 변경 내용에 대한 액세스는 CDC 데이터베이스의 **db_owner** 고정 데이터베이스 역할의 멤버로 제한됩니다.  
  
## <a name="oracle-user-roles"></a>Oracle 사용자 역할  
 다음에서는 Oracle CDC Service에서 사용하는 Oracle 사용자 역할에 대해 설명합니다.  
  
### <a name="database-administrator-dba"></a>데이터베이스 관리자(DBA)  
 Oracle 데이터베이스 관리자(DBA)는 Oracle 데이터베이스 사용자입니다. Oracle DBA가 수행하는 태스크는 다음과 같습니다.  
  
-   ARCHIVELOG 모드에서 작동하도록 원본 Oracle 데이터베이스 설정  
  
-   필요한 권한을 갖춘 로그 마이닝 사용자 설정  
  
-   캡처된 테이블에 대한 보완 로깅 설정  
  
-   더 이상 사용할 수 없는 보관된 트랜잭션 로그 파일을 처리할 수 있도록 복원  
  
 Oracle 데이터베이스 관리자는 실행해야 할 Oracle SQL 스크립트를 얻을 수 있으므로 스크립트를 실행하기 전에 평가할 수 있습니다. Oracle 데이터베이스 관리자는 Oracle CDC Designer 콘솔에서 Oracle SQL 스크립트를 직접 실행할 수도 있습니다.  
  
 Oracle 데이터베이스 관리자가 Oracle CDC Designer 콘솔을 사용할 경우 실제 사용된 컨텍스트(대화 상자)를 제외하고 관리자의 자격 증명이 유지되지 않습니다.  
  
 Oracle 데이터베이스 관리자는 Oracle CDC Service 관리자와 협력하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 인스턴스를 구성합니다.  
  
### <a name="log-mining-user"></a>로그 마이닝 사용자  
 Oracle 로그 마이너 사용자는 Oracle 트랜잭션 로그에 액세스하고 처리하는 데 필요한 권한이 부여된 특수한 Oracle 데이터베이스 사용자입니다.  
  
 이 사용자의 자격 증명은 비대칭 키 암호화를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 인스턴스 데이터베이스에 저장됩니다. 이 자격 증명에는 Oracle CDC Service만 액세스할 수 있으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 인스턴스 데이터베이스 소유자는 액세스할 수 없습니다.  
  
 다음 목록에서는 로그 마이닝 사용자에게 부여되어야 할 필수 권한에 대해 설명합니다.  
  
-   에 선택 \<any 캡처된 테이블 >  
  
-   SELECT ANY TRANSACTION  
  
-   DBMS_LOGMNR에 대한 EXECUTE 권한  
  
-   V$LOGMNR_CONTENTS에 대한 SELECT 권한  
  
-   V$ARCHIVED_LOG에 대한 SELECT 권한  
  
-   V$LOG에 대한 SELECT 권한  
  
-   V$LOGFILE에 대한 SELECT 권한  
  
-   V$DATABASE에 대한 SELECT 권한  
  
-   V$THREAD에 대한 SELECT 권한  
  
-   ALL_INDEXES에 대한 SELECT 권한  
  
-   ALL_OBJECTS에 대한 SELECT 권한  
  
-   DBA_OBJECTS에 대한 SELECT 권한  
  
-   ALL_TABLES에 대한 SELECT 권한  
  
 이러한 권한을 V$xxx에 부여할 수 없는 경우 V $xxx에 부여해야 합니다.  
  
### <a name="schema-user"></a>스키마 사용자  
 Oracle 스키마 사용자는 캡처할 Oracle 테이블의 스키마에 대해 읽기 액세스 권한이 있는 Oracle 사용자입니다. 이 사용자는 Oracle CDC Designer 콘솔에서 작업하면서 Oracle 스키마 목록, 캡처할 테이블과 열, 인덱스 및 키를 검색할 때 필요합니다.  
  
 이 사용자의 자격 증명은 저장되지 않습니다. CDC Designer 콘솔에서 필요할 때마다 자격 증명을 요청하며 나머지 UI 세션을 위해 유지됩니다.  
  
  
