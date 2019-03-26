---
title: 성능 카운터 | Microsoft Docs
ms.custom: supportability
ms.date: 08/27/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], performance counters
- performance counters [Integration Services]
- data flow [Integration Services], performance
- counters [Integration Services]
- data flow engine [Integration Services]
ms.assetid: 11e17f4e-72ed-44d7-a71d-a68937a78e4c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 374e977eafce0dcb679997e85655302aa7de0b4d
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58271006"
---
# <a name="performance-counters"></a>성능 카운터
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 데이터 흐름 엔진의 성능을 모니터링하는 데 사용할 수 있는 성능 카운터 집합을 설치합니다. 예를 들어 "Buffers spooled" 카운터를 보면 패키지가 실행되는 동안 데이터 버퍼가 디스크에 임시로 기록되는지 여부를 확인할 수 있습니다. 이러한 스와핑은 성능을 저하시키고 컴퓨터에 메모리가 부족함을 나타냅니다.  
  
> **참고:** [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 을 실행하는 컴퓨터에 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]를 설치한 다음 해당 컴퓨터를 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]로 업그레이드하는 경우 업그레이드 프로세스는 컴퓨터에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 성능 카운터를 제거합니다. 컴퓨터에 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 성능 카운터를 복원하려면 복원 모드에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행합니다.  
  
 다음 표에서는 성능 카운터에 대해 설명합니다.  
  
|성능 카운터|설명|  
|-------------------------|-----------------|  
|BLOB bytes read|데이터 흐름 엔진이 모든 원본에서 읽어 온 BLOB(Binary Large Object) 데이터의 바이트 수입니다.|  
|BLOB bytes written|데이터 흐름 엔진이 모든 대상에 기록한 전체 BLOB 데이터의 바이트 수입니다.|  
|BLOB files in use|데이터 흐름 엔진이 현재 스풀링을 위해 사용하고 있는 BLOB 파일 수입니다.|  
|Buffer memory|현재 사용 중인 메모리의 크기입니다. 여기에는 실제 메모리와 가상 메모리가 모두 포함됩니다. 이 값이 물리적 메모리 양보다 크면 **Buffers Spooled** 는 증가하며 이는 메모리 스와핑이 늘어남을 나타냅니다. 메모리 스와핑이 늘어나면 데이터 흐름 엔진의 성능이 느려집니다.|  
|Buffers in use|모든 데이터 흐름 구성 요소 및 데이터 흐름 엔진이 현재 사용 중인 모든 유형의 버퍼 개체 수입니다.|  
|Buffers Spooled|디스크에 현재 기록된 버퍼 수입니다. 데이터 흐름 엔진에 물리적 메모리가 부족하면 현재 사용되지 않은 버퍼는 디스크에 쓰여지고 필요에 따라 다시 로드됩니다.|  
|Flat buffer memory|모든 플랫 버퍼가 사용하는 전체 메모리(바이트)입니다. 플랫 버퍼는 구성 요소가 데이터 저장에 사용하는 메모리 블록입니다. 플랫 버퍼는 바이트의 큰 블록이며 바이트 단위로 액세스됩니다.|  
|Flat buffers in use|데이터 흐름 엔진이 사용하는 플랫 버퍼 수입니다. 모든 플랫 버퍼는 전용 버퍼입니다.|  
|Private buffer memory|모든 전용 버퍼가 사용하는 전체 메모리 양입니다. 데이터 흐름 엔진이 데이터 흐름을 지원하기 위해 만드는 버퍼는 전용 버퍼가 아닙니다. 전용 버퍼는 변환 작업에서 임시 작업용으로만 사용하는 버퍼입니다. 예를 들어 집계 변환은 전용 버퍼를 사용하여 내부 계산을 수행합니다.|  
|Private buffers in use|변환 작업에서 사용하는 버퍼 수입니다.|  
|Rows read|원본에서 생성하는 행 개수입니다. 조회 변환이 참조 테이블에서 읽은 행은 포함되지 않습니다.|  
|Rows written|대상에 제공된 행 개수입니다. 대상 데이터 저장소에 쓰여진 행은 반영되지 않습니다.|  
  
 성능 MMC(Microsoft Management Console) 스냅인을 사용하여 성능 카운터를 캡처하는 로그를 작성할 수 있습니다.  
  
 성능을 향상시키는 방법에 대한 자세한 내용은 [데이터 흐름 성능 기능](../../integration-services/data-flow/data-flow-performance-features.md)을 참조하세요.  
  
## <a name="obtain-performance-counter-statistics"></a>성능 카운터 통계 가져오기  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트의 경우 [dm_execution_performance_counters&#40;SSISDB 데이터베이스&#41;](../../integration-services/functions-dm-execution-performance-counters.md) 함수를 사용하여 성능 카운터 통계를 가져올 수 있습니다.  
  
 다음 예에서는 이 함수가 ID가 34인 실행 인스턴스에 대한 통계를 반환합니다.  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (34)  
```  
  
 다음 예에서는 이 함수가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에서 실행 중인 모든 실행 인스턴스에 대한 통계를 반환합니다.  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (NULL)  
  
```  
  
> **중요!!** **ssis_admin** 데이터베이스 역할의 멤버에게는 진행 중인 모든 실행에 대한 성능 통계가 반환됩니다.  **ssis_admin** 데이터베이스 역할이 아닌 멤버에게는 읽기 권한이 있는 진행 중인 실행에 대한 성능 통계가 반환됩니다.  
  
## <a name="related-content"></a>관련 내용  
  
-   codeplex.com의 도구, [SSIS Performance Visualization for Business Intelligence Development Studio(CodePlex 프로젝트)](https://go.microsoft.com/fwlink/?LinkId=146626)  
  
-   msdn.microsoft.com의 비디오, [기업에서 SSIS 패키지의 성능 측정 및 이해(SQL Server 비디오)](https://go.microsoft.com/fwlink/?LinkId=150497)  
  
-   support.microsoft.com의 지원 문서, [Windows Server 2008로 업그레이드한 후 성능 모니터에서 SSIS 성능 카운터를 더 이상 사용할 수 없다.](https://go.microsoft.com/fwlink/?LinkId=235319)  

## <a name="add-a-log-for-data-flow-performance-counters"></a>데이터 흐름 성능 카운터에 대한 로그 추가
  이 절차에서는 데이터 엔진에서 제공하는 성능 카운터에 대한 로그를 추가하는 방법을 설명합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 을 실행하는 컴퓨터에 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]를 설치한 다음 해당 컴퓨터를 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]로 업그레이드하는 경우 업그레이드 프로세스는 컴퓨터에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 성능 카운터를 제거합니다. 컴퓨터에 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 성능 카운터를 복원하려면 복원 모드에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행합니다.  
  
### <a name="to-add-logging-of-performance-counters"></a>성능 카운터 로깅을 추가하려면  
  
1.  클래식 보기를 사용하는 경우 **제어판**에서 **관리 도구**를 클릭합니다. 종류별 보기를 사용하는 경우 **성능 및 유지 관리** 를 클릭한 다음 **관리 도구**를 클릭합니다.  
  
2.  **성능**을 클릭합니다.  
  
3.  **성능** 대화 상자에서 **성능 로그 및 경고**를 확장하고 **카운터 로그**를 마우스 오른쪽 단추로 클릭한 다음 **새 로그 설정**을 클릭합니다. 로그 이름을 입력합니다. 예를 들어 **MyLog**를 입력합니다.  
  
4.  **확인**을 클릭합니다.  
  
5.  **MyLog** 대화 상자에서 **카운터 추가**를 클릭합니다.  
  
6.  **로컬 컴퓨터 카운터 사용** 을 클릭하여 로컬 컴퓨터에 성능 카운터를 로그하거나 **다음 컴퓨터에서 카운터 선택** 을 클릭하고 목록에서 컴퓨터를 선택하여 지정된 컴퓨터에서 성능 카운터를 로그합니다.  
  
7.  **카운터 추가** 대화 상자의 **성능 개체** 목록에서 **SQL Server:SSIS Pipeline** 을 선택합니다.  
  
8.  다음 중 하나를 수행하여 성능 카운터를 선택합니다.  
  
    -   **모든 카운터** 를 선택하여 모든 성능 카운터를 로그합니다.  
  
    -   **목록에서 카운터 선택** 을 선택하고 사용할 성능 카운터를 선택합니다.  
  
9. **추가**를 클릭합니다.  
  
10. **닫기**를 클릭합니다.  
  
11. **MyLog** 대화 상자의 **카운터** 목록에서 로깅 성능 카운터 목록을 검토합니다.  
  
12. 추가 카운터를 추가하려면 5단계~10단계를 반복합니다.  
  
13. **확인**을 클릭합니다.  
  
    > [!NOTE]  
    >  Administrators 그룹의 멤버인 로컬 계정 또는 도메인 계정을 사용하여 성능 로그 및 경고 서비스를 시작해야 합니다.  

## <a name="see-also"></a>참고 항목  
 [프로젝트 및 패키지 실행](../packages/run-integration-services-ssis-packages.md) [Integration Services 패키지에서 기록하는 이벤트](../../integration-services/performance/events-logged-by-an-integration-services-package.md)  
