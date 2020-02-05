---
title: 시스템 데이터 컬렉션 집합 보고서 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collector [SQL Server], server activity
- server activity [SQL Server]
- reports [SQL Server], data collection
- reports [SQL Server], disk usage
- collection sets [SQL Server], reports
- data collector [SQL Server], reports
- reports [SQL Server], query statistics
- query statistics reports [SQL Server]
- disk usage reports [SQL Server]
ms.assetid: 0b126b8d-4fe7-443d-8a9a-c266350181e5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d171085f34e2a20f9e4b1db809327d078ce08436
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67990595"
---
# <a name="system-data-collection-set-reports"></a>시스템 데이터 컬렉션 집합 보고서
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  데이터 수집기는 각 시스템 데이터 컬렉션 집합에 대한 기록 보고서를 제공합니다. 다음 보고서 각각은 관리 데이터 웨어하우스에 저장된 데이터를 사용합니다.  
  
-   [디스크 사용 요약](#Disk)  
  
-   [쿼리 통계 기록](#Query)  
  
-   [서버 작업 기록](#Server)  
  
 이러한 보고서를 사용하여 시스템 용량을 모니터링하고 시스템 성능 문제를 해결하는 데 필요한 정보를 얻을 수 있습니다.  
  
##  <a name="Disk"></a> 디스크 사용 요약 보고서  
 디스크 사용 요약 보고서에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 있는 모든 데이터베이스의 디스크 공간 사용에 대한 데이터가 포함되어 있습니다. 이 보고서에 제공되는 데이터는 일반 T-SQL 쿼리 수집기 형식을 사용하는 디스크 사용 컬렉션 집합을 사용하여 가져옵니다.  
  
 개체 탐색기에서 디스크 사용 요약 보고서에 액세스할 수 있습니다. 이 보고서를 보려면 **관리** 폴더를 확장하고 **데이터 컬렉션**을 마우스 오른쪽 단추로 클릭한 다음 **보고서**, **관리 데이터 웨어하우스**를 차례로 가리키고 **디스크 사용 요약**을 클릭합니다. 자세한 내용은 [컬렉션 집합 보고서 보기&#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)인스턴스에 있는 모든 데이터베이스의 디스크 공간 사용에 대한 데이터가 포함되어 있습니다.  
  
### <a name="disk-usage-collection-set-report"></a>디스크 사용 컬렉션 집합 보고서  
 디스크 사용 컬렉션 집합 보고서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 데이터베이스에 사용되는 디스크 공간에 대한 개요와 이러한 각 데이터베이스의 데이터 및 로그 파일에 대한 증가 추세를 제공합니다.  
  
-   요약 테이블에 데이터 수집기가 모니터링하는 서버에 설치되어 있는 모든 데이터베이스의 시작 크기와 현재 크기가 MB 단위로 표시됩니다.  
  
-   데이터 및 로그 파일에 대한 추세 및 평균 증가 정보가 그래픽과 숫자로 표시됩니다.  
  
#### <a name="disk-usage-collection-set---database-database_name-subreport"></a>디스크 사용량 컬렉션 집합 - 데이터베이스: &lt;database_name&gt; 하위 보고서  
 디스크 사용 컬렉션 집합 보고서의 요약 테이블에 있는 특정 데이터베이스 또는 로그 파일의 추세 선을 클릭하면 디스크 사용 컬렉션 집합 - 데이터베이스: *<database_name>* 하위 보고서가 표시됩니다. 이 보고서에서는 보고서 기간 동안 디스크 공간 사용의 증가 추세를 그래픽으로 나타냅니다. 디스크 사용량은 데이터 파일의 경우 사용 중인 공간, 데이터 공간, 할당되지 않은 공간 및 인덱스 공간별로, 로그 파일의 경우 사용 중인 공간과 사용하지 않은 공간별로 구성되고 보고됩니다.  
  
 그래프 아래의 테이블에서는 데이터 컬렉션 시간 및 해당 사용량 현황 데이터를 보여 줍니다.  
  
#### <a name="disk-usage-for-database-database_name-subreport"></a>데이터베이스에 대한 디스크 사용: <database_name> 하위 보고서  
 디스크 사용 컬렉션 집합 보고서의 요약 테이블에 있는 데이터베이스 이름을 클릭하면 **데이터베이스에 대한 디스크 사용:** _<database_name>_ 하위 보고서가 표시됩니다. 이 보고서에서는 데이터베이스의 데이터 및 트랜잭션 로그 파일에 의한 공간 사용을 숫자와 그래픽으로 분석하여 제공합니다. 데이터 파일의 공간 사용량은 인덱스 페이지, 할당되지 않은 공간, 데이터 페이지 및 사용하지 않은 공간에 할당된 백분율로 분류됩니다. 이러한 범주는 다음과 같이 정의됩니다.  
  
|Category|정의|  
|--------------|----------------|  
|인덱스|인덱스 페이지를 보관하기 위해 사용된 디스크 공간의 양|  
|할당되지 않음|데이터베이스에 사용할 수 있지만 아직 개체에 할당되지 않은 디스크 공간의 양|  
|data|데이터 페이지가 사용하는 디스크 공간의 양|  
|사용 안 함|하나 이상의 개체에 할당되었지만 아직 사용되지 않은 디스크 공간의 양|  
  
 트랜잭션 로그 파일의 공간 사용은 사용 중인 공간과 사용하지 않은 공간으로 분류됩니다.  
  
 데이터베이스에서 자동 증가 및 자동 축소 이벤트가 발생한 경우 이러한 이벤트는 데이터 파일과 로그 파일 둘 다에 대해 보고됩니다. 이 보고서에는 각 이벤트의 시작 시간과 기간, 그리고 이러한 이벤트에 의한 파일 크기의 변경 결과가 표시됩니다.  
  
 데이터베이스의 각 데이터 파일이 사용하는 디스크 공간이 보고됩니다. 예약된 공간으로 보고된 공간은 사용 중인 공간과 파일에 할당되었지만 아직 사용되지 않은 공간을 더한 양입니다. 사용 중인 공간으로 보고된 공간은 할당된 공간을 제외한 파일이 현재 사용하는 실제 공간입니다.  
  
##  <a name="Query"></a> 쿼리 통계 기록 보고서  
 쿼리 통계 기록 보고서에는 쿼리 실행 통계가 포함되어 있습니다. 이 보고서에서 사용되는 데이터는 쿼리 작업 수집기 유형을 사용하는 쿼리 통계 컬렉션 집합을 사용하여 가져옵니다.  
  
 개체 탐색기에서 쿼리 통계 기록 보고서에 액세스할 수 있습니다. 이 보고서를 보려면 **관리** 폴더를 확장하고 **데이터 컬렉션**을 마우스 오른쪽 단추로 클릭한 다음 **보고서**, **관리 데이터 웨어하우스**를 차례로 가리키고 **쿼리 통계 기록**을 클릭합니다. 자세한 내용은 [컬렉션 집합 보고서 보기&#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)인스턴스에 있는 모든 데이터베이스의 디스크 공간 사용에 대한 데이터가 포함되어 있습니다.  
  
### <a name="selecting-data-to-include-in-the-report"></a>보고서에 포함할 데이터 선택  
 보고서에는 전체 데이터 컬렉션 기간의 쿼리 실행 통계가 포함됩니다. 보려는 데이터 세그먼트를 선택하기 위해 데이터 컬렉션 시간대를 탐색하는 방법에는 두 가지가 있습니다.  
  
 **시간대 제어 및 탐색 단추**  
  
 이 시간대 제어 및 탐색 단추를 사용하여 시간대를 탐색하거나 데이터 범위를 선택할 수 있습니다. 화살표 단추로 왼쪽 및 오른쪽으로 스크롤할 수 있기 때문에 시간대를 앞이나 뒤로 탐색할 수 있습니다. 기본적으로 화살표는 시간대를 4시간 단위로 탐색합니다. 돋보기 단추를 사용하면 이 시간 단위를 15분, 1시간, 4시간, 12시간 또는 24시간으로 변경할 수 있습니다. 현재 선택한 시간 범위는 시간대 아래의 텍스트에서 강조 표시됩니다. 이러한 값과 보고서의 데이터는 시간대를 클릭하거나 탐색 단추를 사용할 때마다 업데이트됩니다.  
  
 **달력 단추**  
  
 이 달력 단추를 사용하여 보고하려는 데이터의 시작 날짜, 시작 시간 및 기간을 지정할 수 있습니다.  
  
#### <a name="query-statistics-history-report"></a>쿼리 통계 기록 보고서  
 총 CPU별 상위 쿼리 그래프는 총 CPU 사용량을 기반으로 선택한 시간 범위 동안의 각 쿼리의 상대 비용을 보여 줍니다. 상대적 쿼리 비용의 서로 다른 뷰를 표시하려면 그래프 아래에 표시되는 **기간**, **총 I/O**, **물리적 읽기**또는 **논리적 쓰기**하이퍼링크 중 하나를 클릭합니다.  
  
 그래프 아래의 테이블에서는 추가 쿼리 데이터를 제공합니다. 이 테이블에서는 그래프로 나타낸 각 쿼리에 대한 텍스트와 함께 자세한 통계 정보를 보여 줍니다. 그래프 막대는 이 테이블에서 보여 주는 각 쿼리와 같이 활성 링크입니다. 활성 링크를 클릭하면 쿼리에 대한 쿼리 세부 정보 하위 보고서가 열립니다.  
  
#### <a name="query-details-subreport"></a>쿼리 세부 정보 하위 보고서  
 쿼리 세부 정보 하위 보고서에서는 전체 쿼리 텍스트를 제공합니다. 쿼리 옆에는 **쿼리 텍스트 편집** 하이퍼링크가 있는데, 이 링크를 클릭하면 쿼리 편집기에서 쿼리를 열 수 있습니다. 쿼리 아래의 테이블에서는 쿼리 실행당 평균 기간과 같은 쿼리 실행 통계를 제공합니다.  
  
 쿼리 계획의 그래프와 쿼리 실행당 평균 기간이 표시됩니다. 상대적 쿼리 계획 비용의 서로 다른 뷰를 표시하려면 그래프 아래에 표시되는 **기간**, **물리적 읽기**또는 **논리적 쓰기**하이퍼링크 중 하나를 클릭합니다. 그래프 선은 활성 상태이므로 아무 점이나 클릭하여 쿼리 세부 정보 하위 보고서를 열 수 있습니다.  
  
 그래프 아래의 테이블에서는 실행당 CPU 사용을 기반으로 상위 10개의 쿼리 계획을 보여 줍니다. **계획 번호** 열의 각 번호는 쿼리 계획 세부 정보 하위 보고서를 열기 위해 클릭할 수 있는 활성 링크입니다.  
  
#### <a name="query-plan-details-subreport"></a>쿼리 계획 세부 정보 하위 보고서  
 이 보고서에는 쿼리 계획에 대한 정보가 표시됩니다. 이 보고서에서는 쿼리를 편집하고 실행 통계를 볼 수 있을 뿐만 아니라 쿼리 계획에 대한 자세한 정보도 볼 수 있습니다. **그래픽 쿼리 실행 계획 보기** 하이퍼링크는 현재 쿼리에 대한 실행 계획을 그래픽으로 나타냅니다.  
  
## <a name="server-activity-history-report"></a>서버 작업 기록 보고서  
 서버 작업 기록 보고서에는 서버 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 리소스 사용 및 서버 작업 데이터를 포함되어 있습니다. 이 보고서에 제공되는 데이터는 일반 T-SQL 쿼리 수집기 형식 및 성능 카운터 수집기 형식을 사용하는 서버 작업 컬렉션 집합을 사용하여 수집합니다.  
  
 개체 탐색기에서 서버 작업 기록 보고서에 액세스할 수 있습니다. 이 보고서를 보려면 **관리** 폴더를 확장하고 **데이터 컬렉션**을 마우스 오른쪽 단추로 클릭한 다음 **보고서**, **관리 데이터 웨어하우스**를 차례로 가리키고 **서버 작업 기록**을 클릭합니다. 자세한 내용은 [컬렉션 집합 보고서 보기&#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)인스턴스에 있는 모든 데이터베이스의 디스크 공간 사용에 대한 데이터가 포함되어 있습니다.  
  
### <a name="selecting-data-to-include-in-the-report"></a>보고서에 포함할 데이터 선택  
 보고서에는 전체 데이터 컬렉션 기간의 서버 작업이 포함됩니다. 보려는 데이터 세그먼트를 선택하기 위해 데이터 컬렉션 시간대를 탐색하는 방법에는 두 가지가 있습니다.  
  
 **시간대 제어 및 탐색 단추**  
  
 이 시간대 제어 및 탐색 단추를 사용하여 시간대를 탐색하거나 데이터 범위를 선택할 수 있습니다. 화살표 단추로 왼쪽 및 오른쪽으로 스크롤할 수 있기 때문에 시간대를 앞이나 뒤로 탐색할 수 있습니다. 기본적으로 화살표는 시간대를 4시간 단위로 탐색합니다. 돋보기 단추를 사용하면 이 시간 단위를 15분, 1시간, 4시간, 12시간 또는 24시간으로 변경할 수 있습니다. 현재 선택한 시간 범위는 시간대 아래의 텍스트에서 강조 표시됩니다. 이러한 값과 보고서의 데이터는 시간대를 클릭하거나 탐색 단추를 사용할 때마다 업데이트됩니다.  
  
 **달력 단추**  
  
 이 달력 단추를 사용하여 보고하려는 데이터의 시작 날짜, 시작 시간 및 기간을 지정할 수 있습니다.  
  
###  <a name="Server"></a> 서버 작업 기록 보고서  
 서버 작업 기록 보고서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 호스트 운영 체제에 대한 서버 작업의 초기 보기를 보여 줍니다.  
  
 다음 표에서는 이 보고서의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 시스템 작업을 표시하는 그래프와 이 그래프를 통해 액세스할 수 있는 자세한 하위 보고서에 대해 설명합니다.  
  
|그래프|보고서 설명|  
|-----------|------------------------|  
|CPU(%)|CPU(%) 그래프의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 시스템 그래프 선에 있는 점을 클릭하면 이러한 하위 보고서에 액세스할 수 있습니다.<br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : 쿼리 통계 기록 보고서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 가장 비용이 많이 드는 쿼리의 그래프를 제공합니다. 이 그래프 아래의 테이블에는 쿼리 목록과 각 쿼리에 대한 통계 데이터가 표시됩니다. 쿼리를 클릭하면 추가 정보를 볼 수 있습니다.<br /><br /> **시스템**: 시스템 CPU 사용량 보고서에서는 프로세서당 CPU 시간(%)에 대한 그래프 및 각 프로세스에 대한 통계 데이터를 테이블 형식으로 제공합니다.|  
|메모리 사용량|메모리 사용량 그래프의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 시스템 그래프 선에 있는 점을 클릭하면 이러한 하위 보고서에 액세스할 수 있습니다.<br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 사용량 보고서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 메모리 사용량, 메모리 카운터, 유형별 내부 메모리 사용에 대한 그래프 및 구성 요소 유형별 평균 메모리 사용량에 대한 데이터를 나열하는 테이블을 제공합니다.<br /><br /> **시스템**: 시스템 메모리 사용량 보고서에서는 메모리 사용량, 캐시 및 페이지 적중률에 대한 그래프 및 각 프로세스의 작업 집합 및 프라이빗 바이트에 대한 정보를 나열하는 테이블을 제공합니다.|  
|디스크 I/O 사용량|디스크 I/O 사용량 그래프의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 시스템 그래프 선에 있는 점을 클릭하면 이러한 하위 보고서에 액세스할 수 있습니다.<br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디스크 I/O 사용량 보고서에서는 디스크 응답 시간 및 디스크 전송 속도에 대한 그래프를 제공합니다. 디스크, 데이터베이스 및 파일별 가상 파일 통계는 추가 테이블에서 제공합니다.<br /><br /> **시스템**: 시스템 디스크 사용량 보고서에서는 디스크 응답 시간, 평균 디스크 큐 길이 및 디스크 전송 속도에 대한 그래프 및 각 프로세스의 I/O 쓰기 및 읽기에 대한 정보를 나열하는 테이블을 제공합니다.|  
|네트워크 사용량|사용할 수 있는 추가 보고서가 없습니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대기 작업|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대기 작업 그래프는 실행 중인 스레드로 인해 발생한 대기 작업을 대기 범주별로 보여 줍니다. 이 그래프에 있는 세그먼트를 클릭하면 자세한 보고서에 액세스할 수 있습니다. 이 보고서에서는 좁은 시간 프레임 동안의 그래픽 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대기 작업 통계를 제공할 뿐만 아니라 대기 범주에 대한 정보를 테이블 형식으로 제공합니다. CPU 및 해당 하위 범주와 같은 각 범주에 대해 테이블에서 대기 작업 수, 대기 시간 및 총 대기 시간 비율을 보여 줍니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업 그래프에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업의 다양한 측면에 액세스할 수 있습니다. SQL 컴파일/초 그래프 선 위의 점을 클릭하여 다음과 같은 보고서를 가져올 수 있습니다.<br /><br /> <br /><br /> 연결 및 세션<br /><br /> 요청<br /><br /> 계획 캐시 적중률<br /><br /> tempdb 특징|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)   
 [컬렉션 집합 보고서 보기&#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)  
  
  
