---
title: "고급 분석 확장 구성 및 관리 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8d73fd98-0c61-4a62-94bb-75658195f2a6
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 20
---
# 고급 분석 확장 구성 및 관리
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을(를) 설치한 후 R 런타임 구성 및 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 와(과) 관련된 기타 서비스에 사소한 변경 내용을 만들 수 있습니다.  
  
  
 **항목 내용**  
  
-   [SQL Server R Services에 대한 사용자 계정 프로비전](#bkmk_Provisioning)  
  
-   [R 프로세스로 메모리 사용 관리](#bkmk_ManagingMemory)  
  
-   [구성 파일을 사용하여 서비스 기본값 변경](#bkmk_ChangingConfig) 

-   [실행 패드 서비스 계정을 수정](#bkmk_Launchpad) 
  
##  <a name="bkmk_Provisioning"></a> SQL Server R Services에 대한 사용자 계정 프로비전  
 R 런타임 프로세스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 권한이 낮은 로컬 사용자 계정의 컨텍스트에서 실행 됩니다. 낮은 권한의 개별 계정에서 R 런타임 프로세스를 실행하면 다음과 같은 이점이 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에서 실행 중인 R 런타임 프로세스의 권한을 줄임  
  
-   R 런타임 세션 간에 격리 제공  
  
 설치 프로세스의 일부로 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 새로운 Windows *사용자 계정 풀* 만들어집니다 R 런타임 프로세스를 실행 하는 데 필요한 로컬 사용자 계정을 포함 하 합니다. R.를 지 원하는 데 필요한 경우 사용자의 수를 수정할 수 있습니다. 데이터베이스 관리자는 R 서비스 활성화 된 모든 인스턴스에 연결 하려면이 그룹 사용 권한을 받아야 합니다. 자세한 내용은 참조 [SQL Server R 서비스에 대 한 사용자 계정 풀 수정](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)합니다.  
  
 그러나 액세스 제어 목록 (ACL)에 정의할 수 있습니다 중요 한 리소스에 대 한는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] R 런타임 프로세스 리소스에 액세스 하지 못하도록이 그룹에 대 한 액세스를 거부 하도록 합니다.  
  
-   사용자 계정 풀 특정 인스턴스에 연결 됩니다.  각 인스턴스는 r 스크립트에서 사용할 수 있는 별도 작업자 풀에 대 한 계정은 만듭니다. 계정은은 인스턴스 간에 공유할 수 없습니다.
  
-   풀의 사용자 계정 이름은 SQLInstanceName*nn*의 형식입니다. 예를 들어 R 서버로 기본 인스턴스를 사용하는 경우 사용자 계정 풀은 MSSQLSERVER01, MSSQLSERVER02 등과 같은 계정 이름을 지원합니다.  
  
-   사용자 계정 풀의 크기는 정적이고 기본값은 20입니다. 동시에 시작될 수 있는 R 런타임 세션 수는 이 사용자 계정 풀의 크기에 따라 제한됩니다. 그러나 SQL Server 구성 관리자를 사용 하 여 관리자가이 한도 변경할 수 있습니다.  
  
  
 사용자 계정 풀을 변경하는 방법에 대한 자세한 내용은 [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)을(를) 참조하세요.  
  
##  <a name="bkmk_ManagingMemory"></a> R 프로세스로 메모리 사용 관리  
 기본적으로 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 와(과) 연결된 R 런타임 프로세스는 총 컴퓨터 메모리의 20%를 초과하여 사용하지 않도록 제한됩니다. 그러나 필요한 경우 이 한도는 관리자가 늘릴 수 있습니다.  
  
 일반적으로이 크기를 교육 모델 또는 데이터 행 수를 예측 하는 등의 심각한 R 작업에 대 한 적절 한 수 없습니다. 에 대 한 예약 된 메모리의 양을 줄이기 위해 할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (또는 다른 서비스에 대 한) 리소스 관리자를 사용 하 여 외부 리소스 풀 또는 풀을 정의 하 고 할당 합니다. 자세한 내용은 참조 [R 서비스에 대 한 리소스 관리](../../advanced-analytics/r-services/resource-governance-for-r-services.md)합니다.  
  
##  <a name="bkmk_ChangingConfig"></a> 구성 파일을 사용 하 여 고급 서비스 옵션 변경  
 
일부 고급 속성을 제어할 수 있습니다 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 편집 하 여는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 구성 파일입니다. 이 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 만들어지며 기본적으로 다음 위치에 일반 텍스트 파일로 저장됩니다.  
 
```  
<instance path>\binn\rlauncher.config  
```  
  
 이 파일을 변경하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 실행 중인 컴퓨터의 관리자여야 합니다. 파일을 편집하는 경우 변경 내용을 저장하기 전에 백업 복사본을 만드는 것이 좋습니다.  
  
 예를 들어 메모장을 사용하여 기본 인스턴스(MSSQLSERVER)에 대한 구성 파일을 열려면 관리자 권한으로 명령 프롬프트를 열고 다음 명령을 입력합니다.  
  
```  
C:\>Notepad.exe "%programfiles%\Microsoft SQL Server\MSSQL13.MSSQLSERVER\mssql\binn\rlauncher.config"  
  
```  
  
###  <a name="bkmk_properties"></a> 구성 속성  
 모든 설정은 별도 줄의 각 설정으로 키-값 쌍의 형식을 사용합니다. 예를 들어 이 속성은 R 프로세스에서 시스템 메모리의 20% 이상을 사용하지 않도록 지정합니다.  
  
 기본값: `MEMORY_LIMIT_PERCENT=20`  
  
 다음 표에서 각 설정에 대 한 지원 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 허용 가능한 값을 사용 합니다.  
  
|설정 이름|값 유형|기본값|설명|  
|------------------|----------------|-------------|-----------------|  
|JOB_CLEANUP_ON_EXIT|정수<br /><br /> 0 = 사용 안 함<br /><br /> 1 = 사용|1<br /><br /> 종료 시 로그 파일 제거됨|각 R 세션에 대해 생성된 임시 작업 폴더를 R 세션이 완료된 후 정리해야 할지 여부를 지정합니다. 이 설정은 디버깅 작업에 유용합니다.<br /><br /> 참고: 이는 내부 설정용입니다. – 이 값을 변경하지 마십시오.|  
|TRACE_LEVEL|정수<br /><br /> 1 = 오류<br /><br /> 2 = 성능<br /><br /> 3 = 경고<br /><br /> 4 = 정보|1<br /><br /> 출력 경고만|디버깅을 위해 R 시작 관리자(MSSQLLAUNCHPAD)의 추적의 자세한 정도 수준을 구성합니다. 이 설정은 LOG_DIRECTORY 설정에 의해 지정된 경로에 있는 다음 추적 파일에 저장된 추적의 자세한 정도에 영향을 줍니다.<br /><br /> **rlauncher.log**: T-SQL 쿼리를 통해 시작 되는 R 세션에 대해 생성 된 추적 파일입니다.<br /><br /> 이 시나리오에 대한 자세한 내용은 [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md)를 참조하세요.|  

## <a name="bkmk_Launchpad"></a>실행 패드 서비스 계정을 수정

별도 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 를 구성한 경우 각 인스턴스에 대해 만들어진 서비스는 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]합니다. 

기본적으로, 실행 패드 NT Service\MSSQLLaunchpad R 스크립트를 실행 하는 데 필요한 모든 권한을 사용 하 여 제공 되는 계정을 사용 하 여 실행 되도록 구성 됩니다. 그러나이 계정을 변경 하면 실행 패드 못할를 시작 하거나 R 스크립트를 실행 해야 하는 SQL Server 인스턴스에 액세스할 수 있습니다.
 
  서비스 계정, 수정 하는 경우 사용 해야는 **로컬 보안 정책** 각 서비스에 대 한 권한을 이러한 사용 권한을 포함 하도록 계정을 응용 프로그램 및 업데이트 합니다.
  + 프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)
  + 트래버스 검사 무시(SeChangeNotifyPrivilege)
  + 서비스로 로그온(SeServiceLogonRight)
  + 프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)

SQL Server 서비스를 실행 하는 데 필요한 사용 권한에 대 한 자세한 내용은 참조 [Windows 서비스 계정 및 권한 구성](https://msdn.microsoft.com/library/ms143504.aspx#Windows)합니다.
   
## 참고 항목  
 [SQL Server R Services 시작하기](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  