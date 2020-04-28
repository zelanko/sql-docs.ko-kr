---
title: SQL Server 속성 (시작 매개 변수 탭) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 16942624-5374-446c-8de4-ee6ed34d6e94
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5ab3d9e9e4178b1ee2e10e5be63f0ea9252fd4a4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62679181"
---
# <a name="sql-server-properties-startup-parameters-tab"></a>SQL Server 속성(시작 매개 변수 탭)
  이 대화 상자를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 대한 시작 매개 변수를 추가하거나 제거할 수 있습니다. 시작 매개 변수는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 성능에 많은 영향을 미칠 수 있습니다. 시작 매개 변수를 추가하거나 변경하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 " [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 옵션 사용" 항목을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **시작 매개 변수 지정**  
 매개 변수를 추가하려면 매개 변수를 입력한 다음 **추가**를 클릭합니다.  
  
 필수 매개 변수 중 하나를 수정하려면 **기존 매개 변수** 상자에서 매개 변수를 선택하고 **시작 매개 변수 지정** 상자에서 값을 변경한 다음 **업데이트**를 클릭합니다.  
  
 **기존 매개 변수**  
 매개 변수를 제거하려면 매개변수를 선택한 다음 **제거**를 클릭합니다.  
  
## <a name="parameter-format"></a>매개 변수 형식  
 매개 변수 사이에 구분 기호를 입력하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 구분 기호를 자동으로 추가합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 다음 매개 변수 요구 사항을 적용합니다.  
  
-   선행 공백과 후행 공백은 시작 매개 변수에서 잘립니다.  
  
-   모든 시작 매개 변수는 –(대시)로 시작하고 두 번째 값은 문자입니다.  
  
## <a name="required-parameters"></a>필수 매개 변수  
 필수 매개 변수는 다음과 같습니다. 필수 매개 변수는 변경할 수 있지만 제거할 수는 없습니다.  
  
-   -d는 **master.mdf** 파일(master 데이터베이스 데이터 파일)의 경로입니다.  
  
-   -l는 **master.ldf** 파일(master 데이터베이스 로그 파일)의 경로입니다.  
  
-   -e는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그 파일의 경로입니다.  
  
> [!CAUTION]  
>  파일 경로 매개 변수가 잘못된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 시작할 수 없습니다.  
  
 master 데이터베이스를 이동하는 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "시스템 데이터베이스 이동" 항목을 참조하십시오.  
  
## <a name="optional-parameters"></a>선택적 매개 변수  
 모든 지원되는 시작 매개 변수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 " [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 옵션 사용" 항목에 설명되어 있습니다. 시작 매개 변수 -T*trace#* 은 지정된 추적 플래그( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trace# *) 적용 시*인스턴스를 시작해야 함을 나타냅니다. 추적 플래그는 비표준 동작으로 서버를 시작하는 데 사용합니다. 추적 플래그에 대한 자세한 내용은[!INCLUDE[tsql](../../includes/tsql-md.md)]온라인 설명서에서 "추적 플래그( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )" 항목을 참조하세요.  
  
> [!CAUTION]  
>  인터넷에서 문서화되지 않은 추가 시작 매개 변수 및 추적 플래그를 참조할 수 있습니다. 문서화되지 않은 시작 매개 변수 및 추적 플래그를 만들어 특수한 문제를 해결하거나 테스트하는 데 필요한 특정 조건을 강제 적용할 수 있습니다. 문서화되지 않은 시작 매개 변수를 사용하면 예기치 못한 결과가 발생할 수 있습니다. 문서화되지 않은 매개 변수는 Microsoft 고객 지원 서비스에서 안내하는 경우에만 사용하십시오.  
  
 다음 목록에서는 일부 일반적인 선택 매개 변수에 대해 설명합니다.  
  
|매개 변수|간단한 설명|  
|---------------|-----------------------|  
|-M|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 단일 사용자 모드로 시작합니다.|  
|-T1204|교착 상태에 있는 잠금의 유형과 리소스 및 현재 영향을 받은 명령을 반환합니다.|  
|-T1224|잠금 수를 기반으로 잠금 에스컬레이션을 해제합니다.|  
|-T3608|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 master 데이터베이스를 제외한 모든 데이터베이스를 자동으로 시작 및 복구하지 못하도록 방지합니다.|  
|-T7806|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]에 DAC(관리자 전용 연결)를 설정합니다.|  
  
> [!CAUTION]  
>  일부 선택 매개 변수는 서버 동작을 변경하고 성능에 영향을 줄 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 이 페이지는 레지스트리에서 관련 항목을 변경할 수 있는 사용자만 사용해야 합니다. 해당되는 사용자는 다음과 같습니다.  
  
-   로컬 Administrators 그룹의 멤버  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용되는 도메인 계정( [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 도메인 계정에서 실행하도록 구성된 경우)  
  
## <a name="books-online-references"></a>온라인 설명서 참조  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시작 매개 변수에 대한 자세한 내용은[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "방법: 서버 시작 옵션 구성( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자)"을 참조하세요.  
  
  
