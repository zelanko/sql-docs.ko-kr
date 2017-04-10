---
title: "SQL Server R Services용 사용자 계정 풀 수정 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 58b79170-5731-46b5-af8c-21164d28f3b0
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# SQL Server R Services용 사용자 계정 풀 수정
  설치 과정의 일환으로 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], 새로운 Windows *사용자 계정 풀* 사용 하 여 작업의 실행을 지원 하기 위해 만들어지는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스입니다. 이러한 작업자 계정의 목적은 동시에 여러 SQL 사용자 R 스크립트 실행을 격리 하는 것입니다.
  
  이 풀의 사용자 계정 수에 따라 동시에 활성화할 수 있는 R 세션의 수가 결정됩니다.   동일한 사용자 여러 R 스크립트를 동시에 실행 하는 경우 해당 사용자가 세션을 실행 하는 모든는 같은 작업자 계정을 사용 합니다. 결과적으로 사용자 한 명이 동시에 실행 리소스를 허용 하는 다른 R 스크립트 100 있을 수 있습니다.

## 기본 구성   
-   기본 인스턴스를 그룹 이름은 **SQLRUserGroup**합니다. 
-   인스턴스 이름으로 명명된 된 인스턴스를 기본 그룹 이름을 붙습니다: 예를 들어 **SQLRUserGroupMyInstanceName**합니다. 
-   계정: 기본적으로 사용자 계정 풀에 20 개의 사용자 계정, 명명 된 **MSSQLSERVER01** 통해 **MSSQLSERVER20** 기본 인스턴스에 대 한 합니다.  
-   명명된 된 인스턴스에 대 한 사용자 계정 이름은 인스턴스 이름을 사용 하 여: 예를 들어 **MyInstanceName01** 통해 **MyInstanceName20**합니다.  


## 각 인스턴스에 대 한 사용자 그룹 관리
Windows 계정 그룹이 만들어집니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 각 인스턴스에 R 서비스가 설치 되어 있으므로 R를 지 원하는 여러 인스턴스를 설치한 경우 여러 사용자 그룹에 대 한 설치 합니다.
그러나 각 사용자 그룹은 연결 된는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 특정 인스턴스에서 서비스 및 다른 인스턴스에서 실행 되는 R 작업을 지원할 수 없습니다.

기본적으로 그룹에서는 **하지** 에 대 한 로그인 권한이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 연관 된 인스턴스. 데이터베이스 관리자가이 그룹을 제공 해야 할 경우에는 사용자가 R 스크립트 실행을 사용 하도록 설정 하려면, **연결할** 사용 권한입니다.  

### Windows 사용자 그룹에 있는 작업자 계정의 수 변경

속성을 편집 해야 계정 풀의 사용자 수를 수정 하려면는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 아래 설명 된 대로 서비스입니다.  
  
각 사용자 계정에 연결 된 암호는 임의로 생성 하지만 계정이 작성 되 면 나중에 변경할 수 있습니다.  
  
1. SQL Server 구성 관리자를 열고 선택 **SQL Server 서비스**합니다.
2. SQL Server 실행 패드 서비스를 두 번 클릭 하 고 실행 하는 경우 서비스를 중지 합니다. 
3.  에 **서비스** 탭 시작 모드가 자동으로 설정 되어 있는지 확인 합니다. R 스크립트 실행 패드를 실행 하지 않는 경우 실패 합니다.
4.  클릭 된 **고급** 탭 및의 값을 편집할 **외부 사용자 수** 필요한 경우. 이 설정은 다른 SQL 사용자가 얼마나 많은 쿼리가 동시에 실행할 수 r 제어 기본값은 20 개의 계정 대부분의 경우 R 세션을 지 원하는 가장 적절 합니다.
5. 옵션을 설정할 수는 필요에 따라 **외부 사용자가 암호 재설정** 를 _예_ 조직에 90 일 마다 암호를 변경 해야 하는 정책을 경우. 이렇게 실행 패드 사용자 계정에 대 한 유지 관리 하는 암호화 된 암호를 다시 생성 됩니다.    
6.  서비스를 다시 시작합니다.  

## 원격 스크립트 실행에 필요한 추가 사용 권한
실행 하는 경우 컨텍스트를 계산 하는 R 스크립트를 원격으로 SQL Server 컴퓨터와,이 작업자 그룹에 R 스크립트를 실행 하는 SQL Server 인스턴스에 로그인 할 수 있는 권한이 필요 합니다.

자세한 내용은 참조 [업그레이드 및 설치 FAQ](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)합니다. 

  
## 참고 항목  
 [구성 (SQL Server R Services)](../../advanced-analytics/r-services/configuration-sql-server-r-services.md)
  