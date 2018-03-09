---
title: "SQL Server 개체 및 버전에 대한 DAC 지원 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: data-tier-applications
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data-tier application [SQL Server], supported objects
- objects [SQL Server], data-tier applications
ms.assetid: b1b78ded-16c0-4d69-8657-ec57925e68fd
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 12b99446025274f0f3652a7552f53775283af7ac
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="dac-support-for-sql-server-objects-and-versions"></a>SQL Server 개체 및 버전에 대한 DAC 지원
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] DAC(데이터 계층 응용 프로그램)는 가장 일반적으로 사용되는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 개체를 지원합니다.  
  
 **항목 내용**  
  
-   [지원되는 SQL Server 개체](#SupportedObjects)  
  
-   [각 SQL Server 버전에서 지원되는 데이터 계층 응용 프로그램](#SupportByVersion)  
  
-   [데이터 배포 제한 사항](#DeploymentLimitations)  
  
-   [배포 작업에 대한 추가 고려 사항](#Considerations)  
  
##  <a name="SupportedObjects"></a> 지원되는 SQL Server 개체  
 작성 또는 편집 중인 데이터 계층 응용 프로그램에서는 지원되는 개체만 지정할 수 있습니다. DAC를 지원하지 않는 개체가 포함된 기존 데이터베이스에서 DAC를 추출하거나 등록하거나 가져올 수 없습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 DAC에서 다음 개체를 지원합니다.  
  
|||  
|-|-|  
|DATABASE ROLE|FUNCTION: 인라인 테이블 반환|  
|FUNCTION: 다중 문 테이블 반환|FUNCTION: 스칼라|  
|INDEX: 클러스터형|INDEX: 비클러스터형|  
|INDEX: 공간|INDEX: 고유|  
|LOGIN|사용 권한|  
|역할 멤버 자격|SCHEMA|  
|통계|STORED PROCEDURE: Transact-SQL|  
|동의어|TABLE: CHECK 제약 조건|  
|TABLE: 데이터 정렬|TABLE: 계산 열을 포함하는 열|  
|TABLE: DEFAULT 제약 조건|TABLE: FOREIGN KEY 제약 조건|  
|TABLE: INDEX 제약 조건|TABLE: PRIMARY KEY 제약 조건|  
|TABLE: UNIQUE 제약 조건|TRIGGER: DML|  
|TYPE: HIERARCHYID, GEOMETRY, GEOGRAPHY|TYPE: 사용자 정의 데이터 형식|  
|TYPE: 사용자 정의 테이블 형식|USER|  
|VIEW||  
  
##  <a name="SupportByVersion"></a> 각 SQL Server 버전에서 지원되는 데이터 계층 응용 프로그램  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전마다 DAC 작업에 대해 지원되는 수준이 다릅니다. 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 모든 DAC 작업은 해당 제품의 모든 버전에서 지원됩니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에서 지원하는 DAC 작업은 다음과 같습니다.  
  
-   내보내기 및 추출은 지원되는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원됩니다.  
  
-   [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 와 모든 버전의 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]및 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]에서는 모든 작업이 지원됩니다.  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2(서비스 팩 2) 이상과 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 이상에서는 모든 작업이 지원됩니다.  
  
 DAC Framework는 DAC 패키지 및 내보내기 파일을 작성하고 처리하는 클라이언트 쪽 도구를 구성합니다. DAC Framework는 다음과 같은 제품에 포함되어 있습니다.  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 및 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 에는 모든 DAC 작업을 지원하는 DAC Framework 3.0이 포함되어 있습니다.  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 및 Visual Studio 2010 SP1에는 내보내기와 가져오기를 제외한 모든 DAC 작업을 지원하는 DAC Framework 1.1이 포함되어 있습니다.  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 및 Visual Studio 2010에는 내보내기, 가져오기 및 전체 업그레이드를 제외한 모든 DAC 작업을 지원하는 DAC Framework 1.0이 포함되어 있습니다.  
  
-   이전 버전 SQL Server 또는 Visual Studio의 클라이언트 도구는 DAC 작업을 지원하지 않습니다.  
  
 DAC Framework 버전 중 하나로 작성한 DAC 패키지 또는 내보내기 파일은 이전 버전의 DAC Framework에서 처리할 수 없습니다. 예를 들어 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 클라이언트 도구를 사용하여 추출한 DAC 패키지는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 클라이언트 도구를 사용하여 배포할 수 없습니다.  
  
 하위 버전의 DAC Framework에서 작성한 DAC 패키지 또는 내보내기 파일은 상위 버전의 DAC Framework에서 처리할 수 없습니다. 예를 들어 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 클라이언트 도구를 사용하여 추출한 DAC 패키지는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 이상의 클라이언트 도구를 사용하여 배포할 수 없습니다.  
  
##  <a name="DeploymentLimitations"></a> 데이터 배포 제한 사항  
 SQL Server 2012 SP1에서 DAC Framework 데이터 배포 엔진의 정확도 제한 사항에 유의하세요. 제한 사항은 .dacpac 파일 배포 또는 게시, .bacpac 파일 가져오기 등의 DAC Framework 작업에 적용됩니다.  
  
1.  sql_variant 열 내에서 특정 조건 및 기본 형식의 메타데이터 손실 영향을 받는 경우 다음 메시지와 함께 경고가 나타납니다.  **DAC Framework에서 배포될 때 sql_variant 열 내에 사용된 특정 데이터 형식의 특정 속성은 유지되지 않습니다.**  
  
    -   MONEY, SMALLMONEY, NUMERIC, DECIMAL 기본 형식: 전체 자릿수는 유지되지 않습니다.  
  
        -   전체 자릿수가 38인 DECIMAL/NUMERIC 기본 형식: “TotalBytes” sql_variant 메타데이터는 항상 21로 설정됩니다.  
  
    -   모든 텍스트 기본 형식: 데이터베이스 기본 데이터 정렬은 모든 텍스트에 적용됩니다.  
  
    -   BINARY 기본 형식: 최대 길이 속성은 유지되지 않습니다.  
  
    -   TIME, DATETIMEOFFSET 기본 형식: 전체 자릿수는 항상 7로 설정됩니다.  
  
2.  Sql_variant 열 내의 데이터 손실 영향을 받는 경우 다음 메시지와 함께 경고가 나타납니다. **소수 자릿수가 3보다 큰 sql_variant DATETIME2 열의 값이 DAC Framework에서 배포되면 데이터가 손실됩니다. 배포하는 동안 DATETIME2 값은 소수 자릿수가 3과 같도록 제한됩니다.**  
  
    -   소수 자릿수가 3보다 큰 DATETIME2 기본 형식: 소수 자릿수는 3으로 제한됩니다.  
  
3.  Sql_variant 열 내에서 다음 조건에 대한 배포 작업은 실패합니다. 영향을 받는 경우 다음 메시지와 함께 대화 상자가 나타납니다.  **DAC Framework의 데이터 제한으로 인해 작업을 수행하지 못했습니다.**  
  
    -   DATETIME2, SMALLDATETIME 및 DATE 기본 형식: 값이 DATETIME 외 범위인 경우(예: 연도가 1753 미만인 경우)  
  
    -   DECIMAL, NUMERIC 기본 형식: 값의 전체 자릿수가 28보다 큰 경우  
  
##  <a name="Considerations"></a> 배포 작업에 대한 추가 고려 사항  
 DAC Framework 데이터 배포 작업에 대한 다음 고려 사항에 유의하세요.  
  
-   **추출/내보내기** - DAC Framework를 사용하여 데이터베이스에서 패키지를 만드는 작업(예: .dacpac 파일 추출, .bacpac 파일 내보내기 등)에서는 이러한 제한이 적용되지 않습니다. 패키지의 데이터는 원본 데이터베이스에서 데이터의 전체 정확도 표현입니다. 패키지에 이러한 조건 중 하나라도 있는 경우 추출/내보내기 로그에는 위에서 설명한 메시지를 통한 문제 요약이 포함됩니다. 이것은 그들이 만든 패키지의 잠재적인 데이터 배포 문제에 대해 사용자에게 경고하기 위한 것입니다. 사용자는 로그에서 다음과 같은 요약 메시지를 확인할 수도 있습니다. **이러한 제한은 데이터 형식 및 DAC Framework에서 만든 DAC 패키지에 저장된 값의 정확도에 영향을 미치지 않고, DAC 패키지를 데이터베이스에 배포한 결과 발생한 데이터 유형 및 값에만 적용됩니다. 영향 받는 데이터 및 이 제한을 해결하는 방법은** [다음 항목](http://go.microsoft.com/fwlink/?LinkId=267086)을 참조하세요.  
  
-   **배포/게시/가져오기** - DAC Framework를 사용하여 패키지를 데이터베이스에 배포하는 작업(예: .dacpac 파일 배포 또는 게시, .bacpac 파일 가져오기 등)에서는 이러한 제한이 적용됩니다. 대상 데이터베이스를 만드는 데이터에 패키지에 있는 데이터의 전체 정확도 표현이 포함되지 않을 수 있습니다. 배포/가져오기 로그에는 문제가 발생한 모든 인스턴스에 대해 위에서 언급한 메시지가 포함됩니다. 오류로 인해 작업은 차단되지만(위의 범주 3 참조) 다른 경고와 함께 계속됩니다.  
  
     이 시나리오에서 영향을 받는 데이터와 배포/게시/가져오기 작업에 대한 이 제한 사항을 해결하는 방법은 [다음 항목](http://go.microsoft.com/fwlink/?LinkId=267087)을 참조하세요.  
  
-   **해결 방법** - 추출 및 내보내기 작업에서는 전체 정확도 BCP 데이터 파일을 .dacpac 또는 .bacpac 파일에 기록합니다. 제한 사항을 피하려면 SQL Server BCP.exe 명령 줄 유틸리티를 사용하여 DAC 패키지에서 대상 데이터베이스로 전체 정확도 데이터를 배포합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 계층 응용 프로그램](../../relational-databases/data-tier-applications/data-tier-applications.md)  
  
  
