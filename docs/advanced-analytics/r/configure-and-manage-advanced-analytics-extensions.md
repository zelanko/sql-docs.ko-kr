---
title: "고급 컴퓨터 학습 서비스에 대 한 구성 옵션 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8d73fd98-0c61-4a62-94bb-75658195f2a6
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 872acf107d72989b4623a9d5f4ccb85c44d1f2f9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="advanced-configuration-options-for-machine-learning-services"></a>고급 기계 학습 서비스에 대 한 구성 옵션

이 문서에서는 설치 후에 R 런타임과 SQL Server의 기계 학습 연결 된 다른 서비스 구성을 수정 하려면 적용할 수 있는 변경 내용을 설명 합니다.

적용 대상: SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스

##  <a name="bkmk_Provisioning"></a>프로 비전 사용자 계정을 컴퓨터에 대 한 학습

외부 스크립트의 프로세스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 권한이 낮은 로컬 사용자 계정의 컨텍스트에서 실행 됩니다. 개별 낮은 권한 계정에서 실행 중인 이러한 프로세스는 다음과 같은 이점이 있습니다.

+ 외부 스크립트 런타임 프로세스의 권한을 완화는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터
+ 외부 런타임 Python 또는 R 등의 세션 간에 격리를 제공합니다.

새 Windows 설치 프로그램의 일부로 *사용자 계정 풀* 만들어집니다 R 런타임 프로세스를 실행 하는 데 필요한 로컬 사용자 계정을 포함 하는 합니다. R을 지원하는 데 필요한 경우 사용자 수를 수정할 수 있습니다. 데이터베이스 관리자는 R Services가 사용되는 모든 인스턴스에 연결할 수 있는 권한도 이 그룹에 제공해야 합니다. 자세한 내용은 [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)와(과) 관련된 기타 서비스에 사소한 변경 내용을 만들 수 있습니다.

그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 중요한 리소스에 대해 ACL(액세스 제어 목록)을 정의하여 이 그룹에 대한 액세스를 거부함으로써 R 런타임 프로세스가 리소스에 액세스하지 못하도록 할 수 있습니다.

+ 사용자 계정 풀은 특정 인스턴스에 연결됩니다.  R 스크립트가 사용되는 각 인스턴스에 대해 별도 작업자 계정 풀이 생성됩니다. 인스턴스 간에 계정을 공유할 수 없습니다.

+ 풀의 사용자 계정 이름은 SQLInstanceName*nn*와(과) 관련된 기타 서비스에 사소한 변경 내용을 만들 수 있습니다. 예를 들어 R 서버로 기본 인스턴스를 사용하는 경우 사용자 계정 풀은 MSSQLSERVER01, MSSQLSERVER02 등과 같은 계정 이름을 지원합니다.

+ 사용자 계정 풀의 크기는 정적이고 기본값은 20입니다. 동시에 시작될 수 있는 R 런타임 세션 수는 이 사용자 계정 풀의 크기에 따라 제한됩니다. 그러나 이 제한은 관리자가 SQL Server 구성 관리자를 사용하여 변경할 수 있습니다.

사용자 계정 풀을 변경하는 방법에 대한 자세한 내용은 [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)을(를) 참조하세요.

##  <a name="bkmk_ManagingMemory"></a>외부 스크립트 프로세스에 사용 되는 메모리 관리

기본적으로 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 와(과) 연결된 R 런타임 프로세스는 총 컴퓨터 메모리의 20%를 초과하여 사용하지 않도록 제한됩니다. 그러나 필요한 경우 이 한도는 관리자가 늘릴 수 있습니다.

일반적으로 이 크기는 교육 모델이나 많은 데이터 행 예측 등의 심각한 R 작업에 부적절합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](또는 다른 서비스)에 예약된 메모리 크기를 줄이고 리소스 관리자를 사용하여 외부 리소스 풀을 정의하고 할당해야 할 수도 있습니다. 자세한 내용은 참조 [R에 대 한 리소스 관리](../../advanced-analytics/r/resource-governance-for-r-services.md)합니다.

##  <a name="bkmk_ChangingConfig"></a>구성 파일을 사용 하 여 고급 서비스 옵션 변경

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 구성 파일을 편집하여 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]의 일부 고급 속성을 제어할 수 있습니다. 이 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 만들어지며 기본적으로 다음 위치에 일반 텍스트 파일로 저장됩니다.

`<instance path>\binn\rlauncher.config`

이 파일을 변경하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 실행 중인 컴퓨터의 관리자여야 합니다. 파일을 편집하는 경우 변경 내용을 저장하기 전에 백업 복사본을 만드는 것이 좋습니다.

예를 들어 기본 인스턴스에 대 한 구성 파일을 메모장을 사용 하는 관리자 권한으로 명령 프롬프트를 열고 다음 명령을 입력:

```
C:\>Notepad.exe "%programfiles%\Microsoft SQL Server\MSSQL13.MSSQLSERVER\mssql\binn\rlauncher.config"  
```

##  <a name="bkmk_properties"></a>구성 속성 편집

다음 표에는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 대해 지원되는 각 설정과 허용되는 값이 나와 있습니다.

모든 설정은 별도 줄의 각 설정으로 키-값 쌍의 형식을 사용합니다. 예를 들어이 속성 RLauncher에 대 한 추적 수준을 지정합니다.

기본값: TRACE_LEVEL=4


|**설정 이름**|**값 유형**|**기본값**|**설명**|
|------------------|----------------|-------------|-----------------|
|JOB_CLEANUP_ON_EXIT|정수<br /><br /> 0 = 사용 안 함<br /><br /> 1 = 사용|1<br /><br /> 종료 시 로그 파일 제거됨|각 R 세션에 대해 생성된 임시 작업 폴더를 R 세션이 완료된 후 정리해야 할지 여부를 지정합니다. 이 설정은 디버깅 작업에 유용합니다.<br /><br /> 참고: 이는 내부 설정용입니다. – 이 값을 변경하지 마십시오.|
|TRACE_LEVEL|정수<br /><br /> 1 = 오류<br /><br /> 2 = 성능<br /><br /> 3 = 경고<br /><br /> 4 = 정보|1<br /><br /> 출력 경고만|디버깅을 위해 R 시작 관리자(MSSQLLAUNCHPAD)의 추적의 자세한 정도 수준을 구성합니다. 이 설정은 LOG_DIRECTORY 설정에 의해 지정된 경로에 있는 다음 추적 파일에 저장된 추적의 자세한 정도에 영향을 줍니다.<br /><br /> **rlauncher.log**: T-SQL 쿼리를 통해 시작되는 R 세션에 대해 생성된 추적 파일입니다.<br /><br /> |

## <a name="bkmk_Launchpad"></a>실행 패드 서비스 계정 수정

별도 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 기계 학습 서비스를 구성 하는 각 인스턴스에 대 한 서비스가 만들어집니다.

기본적으로 실행 패드는 R 스크립트를 실행하는 데 필요한 모든 권한으로 프로비전된 NT Service\MSSQLLaunchpad 계정을 사용하여 실행되도록 구성됩니다. 그러나이 계정을 변경 하면 실행 패드 못할를 시작 하거나 SQL Server 인스턴스 외부 스크립트를 실행할 위치에 액세스할 수 있습니다.

서비스 계정을 수정하는 경우 **로컬 보안 정책** 응용 프로그램을 사용하고 다음 사용 권한을 포함하도록 각 서비스 계정의 사용 권한을 업데이트해야 합니다.

+ 프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)
+ 트래버스 검사 무시(SeChangeNotifyPrivilege)
+ 서비스로 로그온(SeServiceLogonRight)
+ 프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)

SQL Server 서비스를 실행하는 데 필요한 권한에 대한 자세한 내용은 [Windows 서비스 계정 및 권한 구성](https://msdn.microsoft.com/library/ms143504.aspx#Windows)을 참조하세요.

## <a name="see-also"></a>관련 항목:

[보안 고려 사항](security-considerations-for-the-r-runtime-in-sql-server.md)

