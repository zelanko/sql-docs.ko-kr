---
title: 관리 인스턴스 세부 정보 (SQL Server 유틸리티) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 6e51b7bb-a733-4852-8c33-7f4dbdf931c2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d2b01eceff763d554644065fdb5137695bd82f69
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53374575"
---
# <a name="managed-instance-details-sql-server-utility"></a>관리되는 인스턴스 세부 정보(SQL Server 유틸리티)
  유틸리티 탐색기의 관리되는 인스턴스 뷰에 나오는 정보는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 개별 인스턴스에 대한 사용 데이터, CPU 사용 기록, 파일 수준의 저장소 사용 세부 정보, 그리고 정책 임계값을 확인 및 업데이트하는 기능을 제공합니다. 정책 임계값은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 수준, 컴퓨터, 데이터베이스 파일과 로그 파일, 그리고 저장소 볼륨 수준에서 제어할 수 있습니다. 개별 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 관리되는 인스턴스 속성 정보를 볼 수도 있습니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
 목록 뷰  
 창 맨 위에 있는 목록 뷰에는 개별 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 대한 정보가 ComputerName\InstanceName 형식의 행으로 나열 표시됩니다.  
  
 상태 아이콘은 각 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스의 상태 요약을 사용 범주별로 보여 줍니다.  
  
-   녹색 확인 표시 - ![](../../2014/database-engine/media/well-utilized.gif "Well_utilized") - 리소스 사용 정책을 위반하지 않는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 관리되는 인스턴스 수입니다. 리소스 사용이 정상적입니다.  
  
-   녹색 아래쪽 화살표 - ![](../../2014/database-engine/media/utility-down-arrow.gif "Utility_down_arrow") - 리소스가 사용 미달 상태입니다.  
  
-   빨강색 위쪽 화살표 - ![](../../2014/database-engine/media/utility-up-arrow.gif "Utility_down_arrow") - 리소스가 초과 사용 상태입니다.  
  
 목록 뷰의 열 순서는 마우스로 왼쪽이나 오른쪽으로 끌어서 변경할 수 있습니다. 목록 뷰에서 열 머리글을 마우스 오른쪽 단추로 클릭하고 열을 선택하거나 선택을 취소하여 열을 추가하거나 삭제할 수 있습니다. 오른쪽 클릭 메뉴에도 정렬 옵션이 있습니다. 열 이름 위쪽을 클릭하여 정렬을 활성화할 수도 있습니다.  
  
 유틸리티 목록 뷰의 필터 옵션에 액세스하려면 유틸리티 탐색기 탐색 창의 **관리되는 인스턴스** 노드를 마우스 오른쪽 단추로 클릭하고 **필터**를 선택합니다. 필터 설정이 구현된 후에는 유틸리티 탐색기의 **관리되는 인스턴스** 노드가 **관리되는 인스턴스(필터링됨)** 라고 표시됩니다. 자세한 내용은 [필터 설정&#40;개체 탐색기 및 유틸리티 탐색기&#41;](../ssms/object/filter-settings-object-explorer-and-utility-explorer.md)을 참조하세요.  
  
 기본적으로 각 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 관리되는 인스턴스 상태 정보가 다음과 같은 열에 표시됩니다.  
  
-   인스턴스 CPU – 이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 할당된 프로세서 사용률의 성능 상태가 표시됩니다. 이 매개 변수의 상태는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 설정된 CPU 사용 정책과 일시적 리소스 평가 정책의 구성 설정에 따라 결정됩니다. 자세한 내용은 [CPU 사용 정책에서 노이즈 줄이기&#40;SQL Server 유틸리티&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)를 참조하세요.  
  
     이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스의 프로세서 사용 기록을 보거나 정책 제한을 확인 또는 변경하려면 **CPU 사용** 탭을 클릭합니다.  
  
-   컴퓨터 CPU - 컴퓨터 프로세서 사용 상태가 표시됩니다. 이 매개 변수의 상태는 컴퓨터에 설정된 CPU 사용 정책과 일시적 리소스 평가 정책의 구성 설정에 따라 결정됩니다. 자세한 내용은 [CPU 사용 정책에서 노이즈 줄이기&#40;SQL Server 유틸리티&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)를 참조하세요.  
  
     이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스의 프로세서 사용 기록을 보거나 정책 제한을 확인 또는 변경하려면 **CPU 사용** 탭을 클릭합니다.  
  
-   파일 공간 - 선택된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 속하는 모든 데이터베이스에 대한 파일 공간 사용률 상태의 요약을 표시합니다. 초과 사용 상태의 데이터베이스가 있으면 파일 공간 상태가 목록 뷰에 초과 사용으로 보고됩니다. 미달 사용 상태의 데이터베이스가 있고 초과 사용 상태의 데이터베이스가 없으면 파일 공간 상태가 목록 뷰에 미달 사용으로 보고됩니다. 이러한 경우가 아니면 목록 뷰에 파일 공간 상태가 정상 사용으로 보고됩니다. 정책 제한을 보거나 변경하려면 **저장소 사용** 탭을 클릭합니다.  
  
-   볼륨 공간 – 선택된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 속하는 데이터베이스를 포함하는 모든 볼륨의 볼륨 공간 사용 상태 요약이 표시됩니다. 사용 과다 상태의 볼륨이 있으면 목록 뷰에 볼륨 공간 상태가 사용 과다로 보고됩니다. 사용 미달 상태의 볼륨이 있고 사용 초과인 볼륨이 없으면 목록 뷰에 볼륨 공간 상태가 사용 미달로 보고됩니다. 이러한 경우가 아니면 목록 뷰에 볼륨 공간 상태가 정상 사용으로 보고됩니다. 정책 제한을 보거나 변경하려면 **저장소 사용** 탭을 클릭합니다.  
  
-   정책 유형 - [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 관리되는 인스턴스에 "전역" 기본 정책과 "덮어쓰기" 사용자 지정 정책 중 어떤 것이 적용되는지 표시됩니다.  
  
 목록 뷰의 열 머리글 영역에서 오른쪽 클릭 메뉴를 사용하여 표시할 수 있는 다른 열은 다음과 같습니다.  
  
-   프로세서 이름:  
  
-   프로세서 속도(MHz):  
  
-   프로세서 수:  
  
-   실제 메모리(MB):  
  
-   운영 체제 버전:  
  
-   SQL Server 버전:  
  
-   SQL Server 에디션:  
  
-   클러스터형: (True 또는 False)  
  
-   백업 디렉터리:  
  
-   데이터 정렬:  
  
-   대/소문자 구분: (True 또는 False)  
  
-   언어:  
  
-   마지막 보고 시간: 이 열에는 datetime 데이터 형식을 사용하여 UCP 로컬 날짜 및 시간이 표시됩니다. 자세한 내용은 SQL Server 온라인 설명서의 [datetime(Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071)을 참조하세요. 유틸리티 개체 모델을 사용할 때는 SSMS가 datetimeoffset 데이터 형식을 사용합니다. 자세한 내용은 SQL Server 온라인 설명서의 [datetimeoffset(Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713)을 참조하세요.  
  
 CPU 사용 탭  
 CPU 사용 탭에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스와 컴퓨터 CPU 사용의 기록 데이터 그래프가 함께 표시됩니다.  
  
 그래프에는 표시 영역 오른쪽에 있는 라디오 단추에 지정된 간격에 따라 프로세서 사용 기록이 표시됩니다. 표시 간격을 변경하고 데이터 집합을 새로 고치려면 목록에서 라디오 단추를 선택합니다.  
  
 다음과 같은 간격 옵션이 있습니다.  
  
-   1일, 15분 간격으로 표시  
  
-   1주, 1일 간격으로 표시  
  
-   1개월, 1주 간격으로 표시  
  
-   1년, 1개월 간격으로 표시  
  
 저장소 사용 탭  
 저장소 사용 탭에는 저장소 사용 세부 정보를 표시하는 트리 뷰가 있습니다. 시간 데이터는 datetime 데이터 형식을 사용하여 UCP 로컬 날짜 및 시간을 보여 줍니다. 자세한 내용은 SQL Server 온라인 설명서의 [datetime(Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) 을 참조하세요. 유틸리티 개체 모델을 사용할 때는 SSMS가 datetimeoffset 데이터 형식을 사용합니다. 자세한 내용은 SQL Server 온라인 설명서의 [datetimeoffset(Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) 을 참조하세요.  
  
 표시는 데이터베이스별 또는 볼륨별로 그룹화할 수 있습니다. 데이터베이스 트리 뷰를 사용하려면 **파일 그룹화 방법:** 선택에서 **데이터베이스** 라디오 단추를 선택합니다. 개별 데이터베이스 파일의 저장소 사용 상태를 보려면 트리 뷰에서 데이터베이스 이름 옆에 있는 더하기 기호를 클릭합니다. 나열되는 데이터베이스 파일에는 목록 뷰에서 선택한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 관리되는 인스턴스에 속한 모든 시스템 및 사용자 데이터베이스가 포함됩니다.  
  
 트리 구조는 저장소의 계층과 상응합니다. 트리 뷰의 루트 노드는 데이터베이스입니다. 트리 뷰의 다음 수준에는 파일 그룹 노드 한 개 또는 데이터베이스에 속한 여러 노드, 그리고 데이터베이스에 속한 로그에 대한 로그 파일 노드 한 개가 포함됩니다. 다음 수준에는 파일 그룹에 속한 데이터 파일이 포함됩니다.  
  
 저장소 사용 기록 그래프에 표시되는 데이터는 트리 뷰에 선택된 노드에 따라 다릅니다.  
  
-   파일 그룹 노드를 선택하면 선택된 파일 그룹에 속한 모든 데이터 파일에 사용되는 파일 공간 그래프가 표시됩니다.  
  
-   로그 파일 노드를 선택하면 선택된 데이터베이스에 속한 모든 로그 파일에 사용되는 파일 공간 그래프가 표시됩니다.  
  
-   데이터베이스 노드를 선택하면 선택된 데이터베이스에 속한 모든 데이터 파일과 모든 로그 파일에 사용되는 파일 공간을 더한 그래프가 표시됩니다.  
  
 상태 아이콘은 데이터베이스 파일, 파일 그룹 및 로그 파일에 대한 알아보기 쉬운 요약입니다.  
  
 데이터베이스:  
  
-   녹색 확인 표시 - 모든 파일 그룹과 로그 파일이 사용 과다 또는 사용 미달 상태가 아닙니다.  
  
-   녹색 아래쪽 화살표 - 하나 이상의 파일 그룹이나 로그 파일이 사용 미달 상태이며 사용 과다 상태가 아닙니다.  
  
-   빨강 위쪽 화살표 - 하나 이상의 파일 그룹이나 로그 파일이 사용 과다 상태입니다.  
  
 파일 그룹 및 로그 파일:  
  
-   녹색 확인 표시 - 파일 그룹 내 모든 파일의 파일 공간 사용이 사용 과다 또는 사용 미달이 아닙니다.  
  
-   녹색 아래쪽 화살표 - 파일 그룹에서 하나 이상 파일의 파일 공간 사용이 사용 미달이며 파일 그룹에 사용 과다인 파일이 없습니다.  
  
-   빨강 위쪽 화살표 - 파일 그룹 내 모든 데이터 파일의 파일 공간 사용이 사용 과다입니다.  
  
 볼륨별로 파일을 보려면 **파일 그룹화 방법:** 선택에서 **볼륨** 라디오 단추를 선택합니다. 저장소 사용 기록 그래프에는 저장소 볼륨의 모든 데이터 파일과 모든 로그 파일에 사용되는 파일 공간이 표시됩니다. 각 데이터베이스 데이터 파일과 로그 파일의 세부 정보를 보려면 트리를 확장합니다.  
  
 각 볼륨의 상태를 표시하는 데 다음 상태 아이콘이 사용됩니다.  
  
-   녹색 확인 표시 - 리소스 사용이 정상적입니다.  
  
-   녹색 아래쪽 화살표 - 리소스가 사용 미달 상태입니다.  
  
-   빨강 위쪽 화살표 - 리소스가 사용 과다 상태입니다.  
  
 저장소 사용 탭에서 각 파일 이름 옆의 계기에는 파일에 사용되는 공간 크기가 파일의 유효 용량을 기준으로 표시됩니다. 계기 옆에 표시되는 백분율 값은 파일의 유효 용량을 기준으로 한 파일 사용 공간 크기의 비율입니다. 도구 설명에는 유효 용량과 비교하여 각 볼륨과 각 파일의 백분율을 계산하는 데 사용된 데이터가 표시됩니다.  
  
 파일이 자동 증가하도록 구성되지 않은 경우 유효 용량은 파일에 할당된 공간의 양입니다. 파일이 자동 증가하도록 구성된 경우 유효 용량은 현재 파일에 할당된 공간의 양과 볼륨에서 현재 사용 가능한 공간의 양의 합계입니다.  
  
 저장소 사용 정책은 데이터 파일과 로그 파일에 대해 구성할 수 있습니다. 파일의 저장소 사용 정책 임계값을 보거나 변경하려면 저장소 사용 창 아래쪽에 **파일 정책** 링크를 클릭합니다. 저장소 볼륨의 저장소 사용 정책 임계값을 보거나 변경하려면 저장소 사용 창 아래쪽에 **볼륨 정책** 링크를 클릭합니다.  
  
 기본 정책 임계값을 덮어쓰려면 **기본 정책 재정의**라디오 단추를 클릭하고 상한과 하한에 값을 지정한 다음 **확인**을 클릭합니다.  
  
 정책 위반에 대한 허용 오차를 변경하는 방법에 대한 자세한 내용은 [CPU 사용 정책에서 노이즈 줄이기&#40;SQL Server 유틸리티&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)를 참조하세요.  
  
 속성 정보 탭  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 대한 속성 정보에는 다음 범주가 포함됩니다.  
  
-   프로세서 이름:  
  
-   프로세서 속도(MHz):  
  
-   프로세서 수:  
  
-   실제 메모리(MB):  
  
-   운영 체제 버전:  
  
-   SQL Server 버전:  
  
-   SQL Server 에디션:  
  
-   클러스터형: (True 또는 False)  
  
-   백업 디렉터리:  
  
-   데이터 정렬:  
  
-   대/소문자 구분: (True 또는 False)  
  
-   언어:  
  
## <a name="see-also"></a>관련 항목  
 [배포된 데이터 계층 응용 프로그램 세부 정보&#40;SQL Server 유틸리티&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)   
 [유틸리티 대시보드 &#40;SQL Server 유틸리티&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [SQL Server 유틸리티에서 SQL Server 인스턴스 모니터링](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [SQL Server 유틸리티 기능 및 태스크](../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [SQL Server 유틸리티 문제 해결](../../2014/database-engine/troubleshoot-the-sql-server-utility.md)  
  
  
