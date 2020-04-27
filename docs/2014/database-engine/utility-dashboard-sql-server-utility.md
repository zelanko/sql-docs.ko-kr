---
title: 유틸리티 대시보드 (SQL Server 유틸리티) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 999eb741-4a60-43f6-ab37-2df7dce845c1
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5f0eb497499eafe16756becfb9607b925add08e9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62773815"
---
# <a name="utility-dashboard-sql-server-utility"></a>유틸리티 대시보드(SQL Server 유틸리티)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티 대시보드에서 데이터를 보려면 "Utility<UCP_Name>\\(ComputerName\UCP)"라고 표시된 유틸리티 탐색기 트리의 최상위 노드를 선택합니다. 대시보드에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티의 모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 관리되는 인스턴스와 데이터 계층 애플리케이션의 요약과 세부 데이터가 포함됩니다. 대시보드의 데이터를 새로 고치려면 유틸리티 탐색기 트리에서 최상위 노드를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택합니다.  
  
 유틸리티 제어 지점을 만드는 방법은 [SQL Server 유틸리티 제어 지점 만들기&#40;SQL Server 유틸리티&#41;](../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)을 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 추가하는 방법은 [SQL Server 인스턴스 등록&#40;SQL Server 유틸리티&#41;](../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)을 참조하세요.  
  
## <a name="uielement-list"></a>UIElement 목록  
 관리되는 인스턴스 상태  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 관리되는 인스턴스 상태는 유틸리티 탐색기 내용 창에서 왼쪽에 표시됩니다.  
  
 관리되는 인스턴스 상태 매개 변수는 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스의 CPU 사용  
  
-   데이터베이스 파일 사용  
  
-   스토리지 볼륨 공간 사용  
  
-   컴퓨터에 대한 CPU 사용  
  
-   각 매개 변수의 상태는 세 범주로 나뉩니다.  
  
-   충분히 사용됨 – 리소스 사용 정책을 위반하지 않는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 관리되는 인스턴스 수입니다.  
  
-   사용 미달 - 리소스 사용 미달 정책을 위반하는 관리 리소스의 수입니다.  
  
-   사용 과다 - 리소스 사용 과다 정책을 위반하는 관리 리소스의 수입니다.  
  
-   사용 가능한 데이터 없음 - SQL Server 인스턴스가 방금 등록되어 첫 번째 데이터 컬렉션 작업이 아직 완료되지 않았거나 SQL Server의 관리되는 인스턴스 수집 및 UCP로 데이터 업로드 작업에 문제가 발생하여 SQL Server의 관리되는 인스턴스에 대한 사용 가능한 데이터가 없습니다.  
  
 각 상태 매개 변수에 대한 자세한 상태는 슬라이딩 표시기에 나열됩니다. 슬라이딩 표시기의 오른쪽 부분에는 각 상태 범주에 얼마나 많은 관리되는 인스턴스가 해당되는지 표시됩니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 관리되는 인스턴스 또는 데이터 계층 애플리케이션에 대한 필터링된 뷰를 만들려면 유틸리티 대시보드에서 해당 슬라이딩 표시기 옆에 있는 사용 범주 링크를 클릭합니다. 예를 들어 **유틸리티 탐색기 내용** 창에서 **초과 사용 인스턴스 CPU**를 클릭할 경우, SSMS에서는 현재 정책 설정을 기반으로 CPU가 초과 사용된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 관리되는 인스턴스에 대한 필터링된 목록 뷰를 만듭니다.  
  
 사용 범주 링크를 클릭할 때 유틸리티 탐색기 탐색 창의 해당 노드에 **(필터링됨)** 이 추가됩니다. 즉, **관리되는 인스턴스** 레이블이 **관리되는 인스턴스(필터링됨)** 로 바뀝니다. 필터 설정을 보려면 탐색 창의 노드를 마우스 오른쪽 단추로 클릭하고 **필터**를 선택한 다음 **필터 설정**을 클릭합니다. 필터 설정을 지우려면 탐색 창의 노드를 마우스 오른쪽 단추로 클릭하고 **필터**를 선택한 다음 **필터 제거**를 클릭합니다.  
  
 개별 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스의 상태를 보는 방법과 정책 구성 설정을 보거나 변경하는 방법은 [관리되는 인스턴스 세부 정보 &#40;SQL Server 유틸리티 &#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md)를 참조하세요.  
  
 유틸리티 요약  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티에서 관리되는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 관리되는 인스턴스 수와 데이터 계층 애플리케이션의 수를 표시합니다.  
  
 데이터 계층 애플리케이션 상태  
 데이터 계층 애플리케이션의 상태는 유틸리티 탐색기 내용 창에서 오른쪽에 표시됩니다.  
  
 데이터 계층 애플리케이션 상태 매개 변수는 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스의 CPU 사용  
  
-   데이터베이스 파일 사용  
  
-   스토리지 볼륨 공간 사용  
  
-   컴퓨터에 대한 CPU 사용  
  
 각 매개 변수의 상태는 세 범주로 나뉩니다.  
  
-   충분히 사용됨 - 리소스 사용 정책을 위반하지 않는 데이터 계층 애플리케이션의 수 입니다.  
  
-   사용 과다 - 리소스 사용 과다 정책을 위반하지 않는 데이터 계층 애플리케이션의 수 입니다.  
  
-   사용 미달 - 리소스 사용 미달 정책을 위반하지 않는 데이터 계층 애플리케이션의 수 입니다.  
  
-   사용 가능한 데이터 없음 - 데이터 계층 애플리케이션을 포함하는 SQL Server의 관리되는 인스턴스가 데이터를 보고하지 않기 때문에 데이터 계층 애플리케이션에 대한 사용 가능한 데이터가 없습니다.  
  
 각 상태 매개 변수에 대한 자세한 상태는 슬라이딩 표시기에 나열됩니다. 슬라이딩 표시기의 오른쪽 부분에는 각 상태 범주에 얼마나 많은 데이터 계층 애플리케이션이 해당되는지 표시됩니다. 개별 데이터 계층 애플리케이션의 상태를 보는 방법과 정책 구성 설정을 보거나 변경하는 방법은 [배포된 데이터 계층 애플리케이션 세부 정보&#40;SQL Server 유틸리티&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)를 참조하세요.  
  
 유틸리티 스토리지 사용 기록  
 사용 기록은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티 대시보드 아래쪽의 시간 그래프에 표시됩니다. 시간 데이터는 datetime 데이터 형식을 사용하여 UCP 로컬 날짜 및 시간을 보여 줍니다. 자세한 내용은 SQL Server 온라인 설명서의 [datetime(Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) 을 참조하세요. 유틸리티 개체 모델을 사용할 때는 SSMS가 datetimeoffset 데이터 형식을 사용합니다. 자세한 내용은 SQL Server 온라인 설명서의 [datetimeoffset(Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) 을 참조하세요.  
  
 표시 영역 왼쪽에 있는 라디오 단추를 사용하여 그래프의 보고 기간을 변경할 수 있습니다.  
  
 보고 기간 옵션은 다음과 같습니다.  
  
-   1일, 15분 간격으로 표시  
  
-   1주, 1일 간격으로 표시  
  
-   1개월, 1주 간격으로 표시  
  
-   1년, 1개월 간격으로 표시  
  
 보고 간격을 변경하면 자동으로 데이터가 새로 고쳐집니다.  
  
 유틸리티 스토리지 사용  
 대시보드 오른쪽 아래에 있는 스토리지 사용 원형 차트는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 관리되는 인스턴스를 포함하는 컴퓨터의 볼륨에서 사용된 공간과 사용 가능한 공간의 비율을 표시합니다. 여기에 표시되는 데이터는 15분마다 새로 고쳐집니다.  
  
## <a name="see-also"></a>참고 항목  
 [유틸리티 탐색기를 사용 하 여 SQL Server 유틸리티 관리](../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [SQL Server 유틸리티 &#40;SQL Server 인스턴스를 등록&#41;](../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)   
 [리소스 상태 정책 정의 수정&#40;SQL Server 유틸리티&#41;](../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)  
  
  
