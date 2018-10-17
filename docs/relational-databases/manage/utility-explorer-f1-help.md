---
title: 유틸리티 탐색기 F1 도움말 | Microsoft 문서
ms.custom: ''
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
f1_keywords:
- sql13.swb.ue.navigation.f1
- sql13.SWB.UE.dac.details.F1
- sql13.SQB.UE.dac.details.F1
- utility details
helpviewer_keywords:
- Utility
- management
- data-tier application
ms.assetid: 8697e4a4-4f59-4cda-af71-7de86005bd4a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2bd5d38c0541a6e56b73cf5da321844eaa94fd5b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47702551"
---
# <a name="utility-explorer-f1-help"></a>유틸리티 탐색기 F1 도움말
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  다음 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 기능 및 이와 관련된 작업에 대해 설명합니다.  
  
  ## <a name="utility-dashboard-sql-server-utility"></a>유틸리티 대시보드(SQL Server 유틸리티)
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 대시보드에서 데이터를 보려면 "Utility<UCP_Name>\\(ComputerName\UCP)"라고 표시된 유틸리티 탐색기 트리의 최상위 노드를 선택합니다. 대시보드에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티의 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스와 데이터 계층 응용 프로그램의 요약과 세부 데이터가 포함됩니다. 대시보드의 데이터를 새로 고치려면 유틸리티 탐색기 트리에서 최상위 노드를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택합니다.  
  
 유틸리티 제어 지점을 만드는 방법은 [SQL Server 유틸리티 제어 지점 만들기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)을 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 추가하는 방법은 [SQL Server 인스턴스 등록&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)을 참조하세요.  
 
  
### <a name="uielement-list"></a>UIElement 목록  
 관리되는 인스턴스 상태  
 ph x="1" /&gt; 의 관리되는 인스턴스 상태는 유틸리티 탐색기 내용 창에서 왼쪽에 표시됩니다.  
  
 관리되는 인스턴스 상태 매개 변수는 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 CPU 사용  
  
-   데이터베이스 파일 사용  
  
-   저장소 볼륨 공간 사용  
  
-   컴퓨터에 대한 CPU 사용  
  
-   각 매개 변수의 상태는 세 범주로 나뉩니다.  
  
-   충분히 사용됨 – 리소스 사용 정책을 위반하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스 수입니다.  
  
-   사용 미달 - 리소스 사용 미달 정책을 위반하는 관리 리소스의 수입니다.  
  
-   사용 과다 - 리소스 사용 과다 정책을 위반하는 관리 리소스의 수입니다.  
  
-   사용 가능한 데이터 없음 - SQL Server 인스턴스가 방금 등록되어 첫 번째 데이터 컬렉션 작업이 아직 완료되지 않았거나 SQL Server의 관리되는 인스턴스 수집 및 UCP로 데이터 업로드 작업에 문제가 발생하여 SQL Server의 관리되는 인스턴스에 대한 사용 가능한 데이터가 없습니다.  
  
 각 상태 매개 변수에 대한 자세한 상태는 슬라이딩 표시기에 나열됩니다. 슬라이딩 표시기의 오른쪽 부분에는 각 상태 범주에 얼마나 많은 관리되는 인스턴스가 해당되는지 표시됩니다.  
  
 ph x="1" /&gt; 의 관리되는 인스턴스 또는 데이터 계층 응용 프로그램에 대한 필터링된 뷰를 만들려면 유틸리티 대시보드에서 해당 슬라이딩 표시기 옆에 있는 사용 범주 링크를 클릭합니다. 예를 들어 **유틸리티 탐색기 내용** 창에서 **초과 사용 인스턴스 CPU**를 클릭할 경우, SSMS에서는 현재 정책 설정을 기반으로 CPU가 초과 사용된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스에 대한 필터링된 목록 뷰를 만듭니다.  
  
 사용 범주 링크를 클릭할 때 유틸리티 탐색기 탐색 창의 해당 노드에 **(필터링됨)** 이 추가됩니다. 즉, **관리되는 인스턴스** 레이블이 **관리되는 인스턴스(필터링됨)** 로 바뀝니다. 필터 설정을 보려면 탐색 창의 노드를 마우스 오른쪽 단추로 클릭하고 **필터**를 선택한 다음 **필터 설정**을 클릭합니다. 필터 설정을 지우려면 탐색 창의 노드를 마우스 오른쪽 단추로 클릭하고 **필터**를 선택한 다음 **필터 제거**를 클릭합니다.  
  
 개별 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 상태를 보는 방법과 정책 구성 설정을 보거나 변경하는 방법은 [관리되는 인스턴스 세부 정보&amp;#40;SQL Server 유틸리티&amp;#41;](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)를 참조하세요.  
  
 유틸리티 요약  
 ph x="1" /&gt; 유틸리티에서 관리되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스 수와 데이터 계층 응용 프로그램의 수를 표시합니다.  
  
 데이터 계층 응용 프로그램 상태  
 데이터 계층 응용 프로그램의 상태는 유틸리티 탐색기 내용 창에서 오른쪽에 표시됩니다.  
  
 데이터 계층 응용 프로그램 상태 매개 변수는 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 CPU 사용  
  
-   데이터베이스 파일 사용  
  
-   저장소 볼륨 공간 사용  
  
-   컴퓨터에 대한 CPU 사용  
  
 각 매개 변수의 상태는 세 범주로 나뉩니다.  
  
-   충분히 사용됨 - 리소스 사용 정책을 위반하지 않는 데이터 계층 응용 프로그램의 수 입니다.  
  
-   사용 과다 - 리소스 사용 과다 정책을 위반하지 않는 데이터 계층 응용 프로그램의 수 입니다.  
  
-   사용 미달 - 리소스 사용 미달 정책을 위반하지 않는 데이터 계층 응용 프로그램의 수 입니다.  
  
-   사용 가능한 데이터 없음 - 데이터 계층 응용 프로그램을 포함하는 SQL Server의 관리되는 인스턴스가 데이터를 보고하지 않기 때문에 데이터 계층 응용 프로그램에 대한 사용 가능한 데이터가 없습니다.  
  
 각 상태 매개 변수에 대한 자세한 상태는 슬라이딩 표시기에 나열됩니다. 슬라이딩 표시기의 오른쪽 부분에는 각 상태 범주에 얼마나 많은 데이터 계층 응용 프로그램이 해당되는지 표시됩니다. 개별 데이터 계층 응용 프로그램의 상태를 보는 방법과 정책 구성 설정을 보거나 변경하는 방법은 [배포된 데이터 계층 응용 프로그램 세부 정보&#40;SQL Server 유틸리티&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)를 참조하세요.  
  
 유틸리티 저장소 사용 기록  
 사용 기록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 대시보드 아래쪽의 시간 그래프에 표시됩니다. 시간 데이터는 datetime 데이터 형식을 사용하여 UCP 로컬 날짜 및 시간을 보여 줍니다. 자세한 내용은 [datetime(TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 항목을 참조하세요. 유틸리티 개체 모델을 사용할 때는 SSMS가 datetimeoffset 데이터 형식을 사용합니다. 자세한 내용은 [datetimeoffset(TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 항목을 참조하세요.  
  
 표시 영역 왼쪽에 있는 라디오 단추를 사용하여 그래프의 보고 기간을 변경할 수 있습니다.  
  
 보고 기간 옵션은 다음과 같습니다.  
  
-   1일, 15분 간격으로 표시  
  
-   1주, 1일 간격으로 표시  
  
-   1개월, 1주 간격으로 표시  
  
-   1년, 1개월 간격으로 표시  
  
 보고 간격을 변경하면 자동으로 데이터가 새로 고쳐집니다.  
  
 유틸리티 저장소 사용  
 대시보드 오른쪽 아래에 있는 저장소 사용 원형 차트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스를 포함하는 컴퓨터의 볼륨에서 사용된 공간과 사용 가능한 공간의 비율을 표시합니다. 여기에 표시되는 데이터는 15분마다 새로 고쳐집니다.  
 
 ## <a name="deployed-data-tier-application-details-sql-server-utility"></a>배포된 데이터 계층 응용 프로그램 세부 정보(SQL Server 유틸리티)
  유틸리티 탐색기의 배포된 데이터 계층 응용 프로그램 뷰에 나오는 정보는 개별 데이터 계층 응용 프로그램의 사용 데이터, CPU 사용 기록, 파일 수준의 저장소 사용 세부 정보, 그리고 정책 임계값을 확인 및 업데이트하는 기능을 제공합니다. 정책 임계값은 데이터 계층 응용 프로그램 수준에서 CPU 사용에 대해, 그리고 데이터베이스 데이터 파일 및 로그 파일에 대해 제어할 수 있습니다. 개별 데이터 계층 응용 프로그램의 속성 정보를 볼 수도 있습니다.  
  
### <a name="uielement-list"></a>UIElement 목록  
 목록 뷰  
 창 맨 위에 있는 목록 뷰에서는 개별 데이터 계층 응용 프로그램에 대한 데이터를 표시됩니다. 상태 아이콘은 각 데이터 계층 응용 프로그램의 상태 요약을 사용 범주별로 보여 줍니다.  
  
-   녹색 확인 표시 - ![](../../relational-databases/manage/media/well-utilized.gif "Well_utilized") - 리소스 사용 정책을 위반하지 않는 데이터 계층 응용 프로그램의 수입니다. 리소스 사용이 정상적입니다.  
  
-   녹색 아래쪽 화살표 - ![](../../relational-databases/manage/media/utility-down-arrow.gif "Utility_down_arrow") - 리소스가 사용 미달 상태입니다.  
  
-   빨강색 위쪽 화살표 - ![](../../relational-databases/manage/media/utility-up-arrow.gif "Utility_down_arrow") - 리소스가 초과 사용 상태입니다.  
  
 목록 뷰의 열 순서는 마우스로 왼쪽이나 오른쪽으로 끌어서 변경할 수 있습니다. 목록 뷰에서 열 머리글을 마우스 오른쪽 단추로 클릭하고 열을 선택하거나 선택을 취소하여 열을 추가하거나 삭제할 수 있습니다. 오른쪽 클릭 메뉴에도 정렬 옵션이 있습니다. 열 이름 위쪽을 클릭하여 정렬을 활성화할 수도 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 목록 뷰의 필터 옵션에 액세스하려면 유틸리티 탐색기 탐색 창의 **배포된 데이터 계층 응용 프로그램** 노드를 마우스 오른쪽 단추로 클릭하고 **필터**를 선택합니다. 필터 설정이 구현된 후에는 유틸리티 탐색기의 **배포된 데이터 계층 응용 프로그램** 노드가 **배포된 데이터 계층 응용 프로그램(필터링됨)** 이라고 표시됩니다. 자세한 내용은 [필터 설정&#40;개체 탐색기 및 유틸리티 탐색기&#41;](http://msdn.microsoft.com/library/4aab04bc-e1ab-4d4b-ab74-b287fc805bc2)을 참조하세요.  
  
 기본적으로 각 데이터 계층 응용 프로그램의 상태 정보가 다음과 같은 열에 표시됩니다.  
  
-   이름 - 데이터 계층 응용 프로그램의 이름입니다.  
  
-   응용 프로그램 CPU - 이 데이터 계층 응용 프로그램의 프로세서 사용 상태를 표시합니다. 이 매개 변수의 상태는 데이터 계층 응용 프로그램에 설정된 CPU 사용 정책과 일시적 리소스 평가 정책의 구성 설정에 따라 결정됩니다. 자세한 내용은 [CPU 사용 정책에서 노이즈 줄이기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)를 참조하세요.  
  
     이 데이터 계층 응용 프로그램의 프로세서 사용 기록을 보거나 정책 제한을 확인 또는 변경하려면 **CPU 사용** 탭을 클릭합니다.  
  
-   컴퓨터 CPU - 컴퓨터 프로세서 사용 상태가 표시됩니다. 이 매개 변수의 상태는 컴퓨터에 설정된 CPU 사용 정책과 일시적 리소스 평가 정책의 구성 설정에 따라 결정됩니다. 자세한 내용은 [CPU 사용 정책에서 노이즈 줄이기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)를 참조하세요.  
  
     이 데이터 계층 응용 프로그램의 프로세서 사용 기록을 보거나 정책 제한을 확인 또는 변경하려면 **CPU 사용** 탭을 클릭합니다.  
  
-   파일 공간 - 각 데이터 계층 응용 프로그램의 파일 공간 사용 상태 요약을 표시합니다.  
  
    -   녹색 확인 표시 - 모든 파일 그룹과 로그 파일 그룹이 사용 과다 또는 사용 미달 상태가 아닙니다.  
  
    -   녹색 아래쪽 화살표 - 하나 이상의 파일 그룹이나 로그 파일 그룹이 사용 미달 상태이며 사용 과다 상태인 파일 그룹이나 로그 파일 그룹이 없습니다.  
  
    -   빨강 위쪽 화살표 - 하나 이상의 파일 그룹이나 로그 파일 그룹이 사용 과다 상태입니다. 데이터베이스가 "응급" 상태인 경우 상태에는 사용 과다 상태의 로그 파일 공간이 표시됩니다.  
  
     파일 공간 정책 제한을 보거나 변경하려면 **저장소 사용** 탭을 클릭합니다.  
  
-   볼륨 공간 - 선택된 데이터 계층 응용 프로그램에 속하는 데이터베이스를 포함하는 모든 볼륨의 볼륨 공간 사용 상태 요약이 표시됩니다. 사용 과다 상태의 볼륨이 있으면 목록 뷰에 볼륨 공간 상태가 사용 과다로 보고됩니다. 사용 미달 상태의 볼륨이 있고 사용 초과인 볼륨이 없으면 목록 뷰에 볼륨 공간 상태가 사용 미달로 보고됩니다. 이러한 경우가 아니면 목록 뷰에 볼륨 공간 상태가 정상 사용으로 보고됩니다. 정책 제한을 보거나 변경하려면 **저장소 사용** 탭을 클릭합니다.  
  
-   정책 유형 - 데이터 계층 응용 프로그램에 "전역" 기본 정책과 "재정의" 사용자 지정 정책 중 어떤 것이 적용되는지 표시됩니다.  
  
-   인스턴스 이름 – 데이터 계층 응용 프로그램을 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 표시합니다.  
  
 목록 뷰의 열 머리글 영역에서 오른쪽 클릭 메뉴를 사용하여 표시할 수 있는 다른 열은 다음과 같습니다.  
  
-   데이터베이스 이름  
  
-   배포된 날짜  
  
-   신뢰성: (True 또는 False)  
  
-   데이터 정렬  
  
-   호환성 수준: (예: Version100)  
  
-   암호화 사용: (True 또는 False)  
  
-   복구 모델: (단순, 전체 또는 대량 로그)  
  
-   마지막 보고 시간: 이 열에는 날짜 및 시간 데이터 형식을 사용하여 UCP 로컬 날짜 및 시간이 표시됩니다. 자세한 내용은 [datetime(TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 항목을 참조하세요. 유틸리티 개체 모델을 사용할 때는 SSMS가 datetimeoffset 데이터 형식을 사용합니다. 자세한 내용은 [datetimeoffset(TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 항목을 참조하세요.  
  
 CPU 사용 탭  
 CPU 사용 탭에는 데이터 계층 응용 프로그램과 컴퓨터 CPU 사용의 기록 데이터 그래프가 함께 표시됩니다.  
  
 그래프에는 표시 영역 오른쪽에 있는 라디오 단추에 지정된 간격에 따라 프로세서 사용 기록이 표시됩니다. 표시 간격을 변경하고 데이터 집합을 새로 고치려면 목록에서 라디오 단추를 선택합니다.  
  
 다음과 같은 간격 옵션이 있습니다.  
  
-   1일, 15분 간격으로 표시  
  
-   1주, 1일 간격으로 표시  
  
-   1개월, 1주 간격으로 표시  
  
-   1년, 1개월 간격으로 표시  
  
 저장소 사용 탭  
 저장소 사용 탭에는 목록 뷰에 선택된 데이터 계층 응용 프로그램에 속한 데이터베이스 파일과 로그 파일의 저장소 사용 정보를 표시하는 트리 뷰가 있습니다. 시간 데이터는 datetime 데이터 형식을 사용하여 UCP 로컬 날짜 및 시간을 보여 줍니다. 자세한 내용은 [datetime(TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 항목을 참조하세요. 유틸리티 개체 모델을 사용할 때는 SSMS가 datetimeoffset 데이터 형식을 사용합니다. 자세한 내용은 [datetimeoffset(TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 항목을 참조하세요.  
  
 표시는 파일 그룹별 또는 볼륨별로 그룹화할 수 있습니다. 파일 그룹 트리 뷰를 사용하려면 **파일 그룹화 방법:** 선택에서 **파일 그룹** 라디오 단추를 선택합니다.  
  
 저장소 사용 기록 그래프에 표시되는 데이터는 트리 뷰에 선택된 노드에 따라 다릅니다.  
  
-   파일 그룹 노드를 선택하면 선택된 파일 그룹에 속한 모든 데이터 파일에 사용되는 파일 공간 그래프가 표시됩니다.  
  
-   로그 파일 노드를 선택하면 선택된 데이터베이스에 속한 모든 로그 파일에 사용되는 파일 공간 그래프가 표시됩니다.  
  
-   데이터베이스 노드를 선택하면 선택된 데이터베이스에 속한 모든 데이터 파일과 모든 로그 파일에 사용되는 파일 공간을 더한 그래프가 표시됩니다.  
  
 개별 파일의 저장소 사용 상태를 보려면 트리 뷰에서 파일 이름 옆에 있는 더하기 기호를 클릭합니다.  
  
 상태 아이콘은 정책 임계값과 비교한 각 파일 그룹의 상태를 알기 쉽게 보여줍니다.  
  
-   녹색 확인 표시 - 파일 그룹의 하나 이상의 데이터 파일의 파일 공간 사용률이 사용 과다 또는 사용 미달이 아닙니다.  
  
-   녹색 아래쪽 화살표 - 파일 그룹에 파일 공간 사용률이 사용 미달인 데이터 파일이 하나 이상 있으며 사용 과다인 파일은 없습니다.  
  
-   빨강 위쪽 화살표 - 파일 그룹 내 모든 데이터 파일의 파일 공간 사용이 사용 과다입니다. 데이터베이스가 "응급" 상태인 경우 상태에는 사용 과다 상태의 로그 파일 공간이 표시됩니다.  
  
 볼륨별로 파일을 보려면 **파일 그룹화 방법:** 선택에서 **볼륨** 라디오 단추를 선택합니다. 저장소 사용 기록 그래프에는 저장소 볼륨의 모든 데이터 파일과 모든 로그 파일에 사용되는 파일 공간이 표시됩니다. 각 데이터베이스 데이터 파일과 로그 파일의 세부 정보를 보려면 트리를 확장합니다.  
  
 각 볼륨의 상태를 표시하는 데 다음 상태 아이콘이 사용됩니다.  
  
-   녹색 확인 표시 - 리소스 사용이 정상적입니다.  
  
-   녹색 아래쪽 화살표 - 리소스가 사용 미달 상태입니다.  
  
-   빨강 위쪽 화살표 - 리소스가 사용 과다 상태입니다.  
  
 저장소 사용 탭에서 각 파일 이름 옆의 계기에는 파일에 사용되는 공간 크기가 파일의 유효 용량을 기준으로 표시됩니다. 계기 옆에 표시되는 백분율 값은 파일의 유효 용량을 기준으로 한 파일 사용 공간 크기의 비율입니다. 도구 설명에는 유효 용량과 비교하여 각 볼륨과 각 파일의 백분율을 계산하는 데 사용된 데이터가 표시됩니다.  
  
 파일이 자동 증가하도록 구성되지 않은 경우 유효 용량은 파일에 할당된 공간의 양입니다. 파일이 자동 증가하도록 구성된 경우 유효 용량은 현재 파일에 할당된 공간의 양과 볼륨에서 현재 사용 가능한 공간의 양의 합계입니다.  
  
 저장소 사용 정책은 데이터 파일과 로그 파일에 대해 구성할 수 있습니다. 파일의 저장소 사용 정책 임계값을 보거나 변경하려면 저장소 사용 창 아래쪽에 **파일 정책** 링크를 클릭합니다. 저장소 볼륨의 저장소 사용 정책 임계값을 보거나 변경하려면 저장소 사용 창 아래쪽에 **볼륨 정책** 링크를 클릭합니다.  
  
 기본 정책 임계값을 덮어쓰려면 **기본 정책 재정의**라디오 단추를 클릭하고 상한과 하한에 값을 지정한 다음 **확인**을 클릭합니다.  
  
 정책 위반에 대한 허용 오차를 변경하는 방법에 대한 자세한 내용은 [CPU 사용 정책에서 노이즈 줄이기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)를 참조하세요.  
  
 속성 정보 탭  
 데이터 계층 응용 프로그램에 대한 속성 정보에는 다음 범주가 포함됩니다.  
  
-   데이터베이스 이름  
  
-   배포된 날짜  
  
-   신뢰성: (True 또는 False)  
  
-   데이터 정렬  
  
-   호환성 수준: (예: Version100)  
  
-   암호화 사용: (True 또는 False)  
  
-   복구 모델: (단순, 전체 또는 대량 로그)  
  
-   마지막 보고 시간: 이 열에는 날짜 및 시간 데이터 형식을 사용하여 UCP 로컬 날짜 및 시간이 표시됩니다. 자세한 내용은 [datetime(TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 항목을 참조하세요. 유틸리티 개체 모델을 사용할 때는 SSMS가 datetimeoffset 데이터 형식을 사용합니다. 자세한 내용은 [datetimeoffset(TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 항목을 참조하세요.

## <a name="managed-instance-details-sql-server-utility"></a>관리되는 인스턴스 세부 정보(SQL Server 유틸리티)
 유틸리티 탐색기의 관리되는 인스턴스 뷰에 나오는 정보는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 개별 인스턴스에 대한 사용 데이터, CPU 사용 기록, 파일 수준의 저장소 사용 세부 정보, 그리고 정책 임계값을 확인 및 업데이트하는 기능을 제공합니다. 정책 임계값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 수준, 컴퓨터, 데이터베이스 파일과 로그 파일, 그리고 저장소 볼륨 수준에서 제어할 수 있습니다. 개별 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스 속성 정보를 볼 수도 있습니다.  
  
### <a name="uielement-list"></a>UIElement 목록  
 목록 뷰  
 창 맨 위에 있는 목록 뷰에는 개별 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 정보가 ComputerName\InstanceName 형식의 행으로 나열 표시됩니다.  
  
 상태 아이콘은 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 상태 요약을 사용 범주별로 보여 줍니다.  
  
-   녹색 확인 표시 - ![](../../relational-databases/manage/media/well-utilized.gif "Well_utilized") - 리소스 사용 정책을 위반하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스 수입니다. 리소스 사용이 정상적입니다.  
  
-   녹색 아래쪽 화살표 - ![](../../relational-databases/manage/media/utility-down-arrow.gif "Utility_down_arrow") - 리소스가 사용 미달 상태입니다.  
  
-   빨강색 위쪽 화살표 - ![](../../relational-databases/manage/media/utility-up-arrow.gif "Utility_down_arrow") - 리소스가 초과 사용 상태입니다.  
  
 목록 뷰의 열 순서는 마우스로 왼쪽이나 오른쪽으로 끌어서 변경할 수 있습니다. 목록 뷰에서 열 머리글을 마우스 오른쪽 단추로 클릭하고 열을 선택하거나 선택을 취소하여 열을 추가하거나 삭제할 수 있습니다. 오른쪽 클릭 메뉴에도 정렬 옵션이 있습니다. 열 이름 위쪽을 클릭하여 정렬을 활성화할 수도 있습니다.  
  
 유틸리티 목록 뷰의 필터 옵션에 액세스하려면 유틸리티 탐색기 탐색 창의 **관리되는 인스턴스** 노드를 마우스 오른쪽 단추로 클릭하고 **필터**를 선택합니다. 필터 설정이 구현된 후에는 유틸리티 탐색기의 **관리되는 인스턴스** 노드가 **관리되는 인스턴스(필터링됨)** 라고 표시됩니다. 자세한 내용은 [필터 설정&#40;개체 탐색기 및 유틸리티 탐색기&#41;](http://msdn.microsoft.com/library/4aab04bc-e1ab-4d4b-ab74-b287fc805bc2)을 참조하세요.  
  
 기본적으로 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스 상태 정보가 다음과 같은 열에 표시됩니다.  
  
-   인스턴스 CPU – 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 할당된 프로세서 사용률의 성능 상태가 표시됩니다. 이 매개 변수의 상태는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 설정된 CPU 사용 정책과 일시적 리소스 평가 정책의 구성 설정에 따라 결정됩니다. 자세한 내용은 [CPU 사용 정책에서 노이즈 줄이기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)를 참조하세요.  
  
     이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 프로세서 사용 기록을 보거나 정책 제한을 확인 또는 변경하려면 **CPU 사용** 탭을 클릭합니다.  
  
-   컴퓨터 CPU - 컴퓨터 프로세서 사용 상태가 표시됩니다. 이 매개 변수의 상태는 컴퓨터에 설정된 CPU 사용 정책과 일시적 리소스 평가 정책의 구성 설정에 따라 결정됩니다. 자세한 내용은 [CPU 사용 정책에서 노이즈 줄이기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)를 참조하세요.  
  
     이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 프로세서 사용 기록을 보거나 정책 제한을 확인 또는 변경하려면 **CPU 사용** 탭을 클릭합니다.  
  
-   파일 공간 - 선택된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 속하는 모든 데이터베이스에 대한 파일 공간 사용률 상태의 요약을 표시합니다. 초과 사용 상태의 데이터베이스가 있으면 파일 공간 상태가 목록 뷰에 초과 사용으로 보고됩니다. 미달 사용 상태의 데이터베이스가 있고 초과 사용 상태의 데이터베이스가 없으면 파일 공간 상태가 목록 뷰에 미달 사용으로 보고됩니다. 이러한 경우가 아니면 목록 뷰에 파일 공간 상태가 정상 사용으로 보고됩니다. 정책 제한을 보거나 변경하려면 **저장소 사용** 탭을 클릭합니다.  
  
-   볼륨 공간 – 선택된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 속하는 데이터베이스를 포함하는 모든 볼륨의 볼륨 공간 사용 상태 요약이 표시됩니다. 사용 과다 상태의 볼륨이 있으면 목록 뷰에 볼륨 공간 상태가 사용 과다로 보고됩니다. 사용 미달 상태의 볼륨이 있고 사용 초과인 볼륨이 없으면 목록 뷰에 볼륨 공간 상태가 사용 미달로 보고됩니다. 이러한 경우가 아니면 목록 뷰에 볼륨 공간 상태가 정상 사용으로 보고됩니다. 정책 제한을 보거나 변경하려면 **저장소 사용** 탭을 클릭합니다.  
  
-   정책 유형 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스에 "전역" 기본 정책과 "덮어쓰기" 사용자 지정 정책 중 어떤 것이 적용되는지 표시됩니다.  
  
 목록 뷰의 열 머리글 영역에서 오른쪽 클릭 메뉴를 사용하여 표시할 수 있는 다른 열은 다음과 같습니다.  
  
-   프로세서 이름:  
  
-   프로세서 속도(MHz):  
  
-   프로세서 수:  
  
-   실제 메모리(MB):  
  
-   운영 체제 버전:  
  
-   SQL Server 버전:  
  
-   SQL Server 에디션:  
  
-   클러스터: (True 또는 False)  
  
-   백업 디렉터리:  
  
-   데이터 정렬:  
  
-   대/소문자 구분: (True 또는 False)  
  
-   언어:  
  
-   마지막 보고 시간: 이 열에는 날짜 및 시간 데이터 형식을 사용하여 UCP 로컬 날짜 및 시간이 표시됩니다. 자세한 내용은 [datetime(TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 항목을 참조하세요. 유틸리티 개체 모델을 사용할 때는 SSMS가 datetimeoffset 데이터 형식을 사용합니다. 자세한 내용은 [datetimeoffset(TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 항목을 참조하세요.  
  
 CPU 사용 탭  
 CPU 사용 탭에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 컴퓨터 CPU 사용의 기록 데이터 그래프가 함께 표시됩니다.  
  
 그래프에는 표시 영역 오른쪽에 있는 라디오 단추에 지정된 간격에 따라 프로세서 사용 기록이 표시됩니다. 표시 간격을 변경하고 데이터 집합을 새로 고치려면 목록에서 라디오 단추를 선택합니다.  
  
 다음과 같은 간격 옵션이 있습니다.  
  
-   1일, 15분 간격으로 표시  
  
-   1주, 1일 간격으로 표시  
  
-   1개월, 1주 간격으로 표시  
  
-   1년, 1개월 간격으로 표시  
  
 저장소 사용 탭  
 저장소 사용 탭에는 저장소 사용 세부 정보를 표시하는 트리 뷰가 있습니다. 시간 데이터는 datetime 데이터 형식을 사용하여 UCP 로컬 날짜 및 시간을 보여 줍니다. 자세한 내용은 [datetime(TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 항목을 참조하세요. 유틸리티 개체 모델을 사용할 때는 SSMS가 datetimeoffset 데이터 형식을 사용합니다. 자세한 내용은 [datetimeoffset(TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 항목을 참조하세요.  
  
 표시는 데이터베이스별 또는 볼륨별로 그룹화할 수 있습니다. 데이터베이스 트리 뷰를 사용하려면 **파일 그룹화 방법:** 선택에서 **데이터베이스** 라디오 단추를 선택합니다. 개별 데이터베이스 파일의 저장소 사용 상태를 보려면 트리 뷰에서 데이터베이스 이름 옆에 있는 더하기 기호를 클릭합니다. 나열되는 데이터베이스 파일에는 목록 뷰에서 선택한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스에 속한 모든 시스템 및 사용자 데이터베이스가 포함됩니다.  
  
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
  
 정책 위반에 대한 허용 오차를 변경하는 방법에 대한 자세한 내용은 [CPU 사용 정책에서 노이즈 줄이기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)를 참조하세요.  
  
 속성 정보 탭  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 속성 정보에는 다음 범주가 포함됩니다.  
  
-   프로세서 이름:  
  
-   프로세서 속도(MHz):  
  
-   프로세서 수:  
  
-   실제 메모리(MB):  
  
-   운영 체제 버전:  
  
-   SQL Server 버전:  
  
-   SQL Server 에디션:  
  
-   클러스터: (True 또는 False)  
  
-   백업 디렉터리:  
  
-   데이터 정렬:  
  
-   대/소문자 구분: (True 또는 False)  
  
-   언어:  

## <a name="utility-administration-sql-server-utility"></a>유틸리티 관리(SQL Server 유틸리티)
유틸리티 관리 탭을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티의 정책, 보안 및 데이터 웨어하우스 설정을 관리할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 개념에 대한 자세한 내용은 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)를 참조하세요.  
  
### <a name="uielement-list"></a>UIElement 목록
 **정책 탭** - 정책 탭을 사용하여 전역 모니터링 정책을 보거나 지정할 수 있습니다.  
  
 전역 데이터 계층 응용 프로그램의 모니터링 정책을 설정합니다. 이 옵션의 값 목록을 확장하려면 정책 이름 옆에 있는 화살표를 클릭하거나 정책 제목을 클릭합니다.  
 언제 응용 프로그램에서 프로세서 용량이 부족합니까? 이 정책을 변경하려면 정책 설명 오른쪽에 있는 컨트롤을 사용하고 **적용**을 클릭합니다. 아래쪽에 있는 단추를 사용하여 기본값으로 복원하거나 변경을 취소할 수도 있습니다.  
  
-   프로세서 사용률의 기본 최대값은 70%입니다.  
  
-   프로세서 사용률의 기본 최소값은 0%입니다.  
  
 언제 응용 프로그램에서 파일 공간이 부족합니까? 데이터 파일이나 로그 파일 공간 사용률에 대한 정책을 변경하려면 정책 설명 오른쪽에 있는 컨트롤을 사용하고 **적용**을 클릭합니다. 아래쪽에 있는 단추를 사용하여 기본값으로 복원하거나 변경을 취소할 수도 있습니다.  
  
-   파일 공간 사용률의 기본 최대값은 70%입니다.  
  
-   파일 공간 사용률의 기본 최소값은 0%입니다.  
  
 전역 SQL Server의 관리되는 인스턴스 응용 프로그램 모니터링 정책을 설정합니다. 이 옵션의 값 목록을 확장하려면 정책 이름 옆에 있는 화살표를 클릭하거나 정책 제목을 클릭합니다.  
 언제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스에서 프로세서 용량이 부족합니까? 이 정책을 변경하려면 정책 설명 오른쪽에 있는 컨트롤을 사용하고 **적용**을 클릭합니다. 아래쪽에 있는 단추를 사용하여 기본값으로 복원하거나 변경을 취소할 수도 있습니다.  
  
-   인스턴스 프로세서 사용률의 기본 최대값은 70%입니다.  
  
-   인스턴스 프로세서 사용률의 기본 최소값은 0%입니다.  
  
 언제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스 컴퓨터에서 프로세서 용량이 부족합니까? 이 정책을 변경하려면 정책 설명 오른쪽에 있는 컨트롤을 사용하고 **적용**을 클릭합니다. 아래쪽에 있는 단추를 사용하여 기본값으로 복원하거나 변경을 취소할 수도 있습니다.  
  
-   컴퓨터 프로세서 사용률의 기본 최대값은 70%입니다.  
  
-   컴퓨터 프로세서 사용률의 기본 최소값은 0%입니다.  
  
 언제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스에서 파일 공간이 부족합니까? 데이터 파일이나 로그 파일 공간 사용률에 대한 정책을 변경하려면 정책 설명 오른쪽에 있는 컨트롤을 사용하고 **적용**을 클릭합니다. 아래쪽에 있는 단추를 사용하여 기본값으로 복원하거나 변경을 취소할 수도 있습니다.  
  
-   파일 공간 사용률의 기본 최대값은 70%입니다.  
  
-   파일 공간 사용률의 기본 최소값은 0%입니다.  
  
 언제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스 컴퓨터에서 스토리지 볼륨 공간이 부족합니까? 이 정책을 변경하려면 정책 설명 오른쪽에 있는 컨트롤을 사용하고 **적용**을 클릭합니다. 아래쪽에 있는 단추를 사용하여 기본값으로 복원하거나 변경을 취소할 수도 있습니다.  
  
-   컴퓨터 볼륨 공간 사용률의 기본 최대값은 70%입니다.  
  
-   컴퓨터 볼륨 공간 사용률의 기본 최소값은 0%입니다.  
  
 매우 불안정한 리소스에 의해 발생하는 정책 위반 노이즈를 줄입니다. 이 기능의 컨트롤을 확장하려면 오른쪽에 표시되는 아래쪽 화살표를 클릭합니다.  
 자세한 내용은 [CPU 사용 정책에서 노이즈 줄이기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)를 참조하세요.  
  
 
**보안 탭** - UCP를 관리하거나 읽을 수 있는 권한이 있는 로그인 이름을 표시합니다.  
  
 Utility 읽기 역할에 추가될 UCP에서 로그인을 선택합니다.  
 Utility 읽기 권한이 있는 사용자 계정으로 다음과 같은 작업을 할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 연결합니다.  
  
-   SSMS의 유틸리티 탐색기에서 모든 뷰포인트를 봅니다.  
  
-   SSMS의 유틸리티 탐색기의 유틸리티 관리 노드에 있는 설정을 봅니다.  
  
 유틸리티 관리자는 SQL Server Utility에 SQL Server 인스턴스를 등록하거나 제거할 수 있으며 관리되는 인스턴스의 정책을 수정하고 UCP의 관리 설정을 수정할 수 있습니다.  
  
 유틸리티 관리자가 되려면 SQL Server 인스턴스에 대한 sysadmin 권한이 있어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP에 대한 사용자 계정을 추가하거나 변경하려면 SSMS의 개체 탐색기를 사용하여 SQL Server UCP 인스턴스의 서버 로그인에 사용자를 추가합니다. 자세한 내용은 [sp_addlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)을 참조하세요.  
  
 
**데이터 웨어하우스** 탭 - 유틸리티 관리 데이터 웨어하우스에 대한 구성 세부 정보를 표시합니다.  
  
 데이터 보존 기간  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스에 대해 수집된 사용률 정보의 데이터 보존 기간을 지정합니다. 기본 기간은 1년입니다. 최소값은 1개월입니다. 지원되는 가장 긴 기간은 2년입니다.  
  
 유틸리티 데이터 웨어하우스 구성 정보  
 다음 구성 설정은 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]릴리스에서 구성할 수 없습니다.  
  
-   UMDW 이름: Sysutility_mdw_\<GUID>_DATA.  
  
-   컬렉션 집합 업로드 빈도: 15분마다.  
  
 UMDW 디렉터리는 구성할 수 있으며 \<시스템 드라이브>:\Program Files\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\입니다. 여기서 \<시스템 드라이브>는 일반적으로 C:\ 드라이브입니다. 로그 파일 UMDW_\<GUID>_LOG는 같은 디렉터리에 있습니다.  
  
> **참고:** UMDW(sysutility_mdw) 파일 위치는 detach/attach 또는 ALTER DATABASE를 사용하여 변경할 수 있으며 ALTER DATABASE를 사용하는 것이 좋습니다. 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
 제품 기본값으로 돌아갑니다.  
 이 탭의 설정을 기본값으로 다시 설정하려면 **기본값 복원** 단추를 클릭하고 **적용**을 클릭합니다.  
 
  
## <a name="reference"></a>참조  
 [SQL Server 유틸리티 제어 지점 만들기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)  
  
 [SQL Server 유틸리티에 연결](../../relational-databases/manage/connect-to-a-sql-server-utility.md)  
  
 [SQL Server 인스턴스 등록&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)  
  
 [상태 정책 구성&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)  
  
 [SQL Server 유틸리티에서 SQL Server 인스턴스 모니터링](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [SQL Server 유틸리티 문제 해결](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
