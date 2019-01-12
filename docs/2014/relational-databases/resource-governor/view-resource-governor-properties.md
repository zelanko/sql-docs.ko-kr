---
title: 리소스 관리자 속성 보기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql12.swb.rg.properties.f1
helpviewer_keywords:
- Resource Governor, properties
ms.assetid: de3510df-f792-4a9d-80fa-f198fd36cdc8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 35d4720a8fe8b8c1b404a97e27b36896f36dd5f7
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100798"
---
# <a name="view-resource-governor-properties"></a>리소스 관리자 속성 보기
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 리소스 관리자 속성 페이지를 사용하여 리소스 풀, 작업 그룹과 같은 리소스 관리자 엔터티를 만들거나 구성할 수 있습니다.  
  
1.  **시작하기 전 주의 사항:**  [Permissions](#Permissions)  
  
2.  **리소스 관리자 속성을 보려면:**  [Resource Governor 속성 페이지](#ViewRGProp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
 리소스 관리자 엔터티 속성을 보는 것 이외에도, **리소스 관리자 속성** 페이지를 사용하여 몇 가지 구성 작업을 수행할 수 있습니다. 자세한 내용은 다음 항목을 참조하세요.  
  
-   [리소스 관리자 사용](enable-resource-governor.md)  
  
-   [리소스 관리자 사용 안 함](disable-resource-governor.md)  
  
-   [리소스 풀 만들기](create-a-resource-pool.md)  
  
-   [작업 그룹 만들기](create-a-workload-group.md)  
  
-   [리소스 풀 설정 변경](change-resource-pool-settings.md)  
  
-   [작업 그룹 설정 변경](change-workload-group-settings.md)  
  
-   [작업 그룹 이동](move-a-workload-group.md)  
  
 작업 그룹 또는 리소스 풀을 추가, 삭제 또는 이동한 후에 **확인** 을 클릭하면 ALTER RESOURCE GOVERNOR RECONFIGURE 문이 실행됩니다.  
  
 리소스 풀이나 작업 그룹의 생성 또는 재구성 작업이 실패하면 속성 페이지의 제목 아래에 요약 오류 메시지가 표시됩니다. 자세한 오류 메시지를 보려면 오류 메시지에 있는 아래쪽 화살표를 클릭하세요.  
  
 [sys.dm_resource_governor_configuration](/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql) 동적 관리 뷰를 쿼리해 is_configuration_pending의 현재 상태를 가져와서 보류 중인 구성이 있는지 여부를 확인할 수 있습니다.  
  
###  <a name="Permissions"></a> Permissions  
 리소스 관리자 속성을 보려면 VIEW SERVER STATER 권한이 필요합니다. 리소스 관리자 구성 작업을 하려면 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="ViewRGProp"></a> Resource Governor 속성 페이지 보기  
 **Resource Governor 속성 페이지를 사용하여 Resource Governor 속성을 보려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 열고 **리소스 관리자** 까지 **관리**노드를 계속 확장합니다.  
  
2.  **Resource Governor** 를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 그러면 **Resource Governor** 페이지가 열립니다.  
  
3.  이 페이지의 필드에 대한 설명을 보려면 [리소스 관리자 속성](#RGProp)을 참조하세요.  
  
4.  변경 사항을 저장하려면 **확인**을 클릭합니다.  
  
##  <a name="RGProp"></a> 리소스 관리자 속성  
 **분류자 함수 이름**  
 분류자 함수를 목록에서 선택하여 지정합니다.  
  
 **리소스 관리자 사용**  
 확인란을 선택하거나 선택 취소하여 리소스 관리자를 사용하거나 사용하지 않습니다.  
  
 **리소스 풀**  
 제공된 표를 사용하여 리소스 풀 구성을 만들거나 변경합니다. 이 표는 미리 정의된 내부 풀 및 기본 풀에 대한 정보로 채워집니다. 풀의 행에 있는 첫 번째 열을 클릭하여 작업할 풀을 선택합니다. 새 리소스 풀을 만들려면 접두사로 별표는 행을 클릭 합니다 (**&#42;**).  
  
 **이름**  
 리소스 풀의 이름을 지정합니다.  
  
 **최소 CPU(%)**  
 CPU 충돌이 있을 때 리소스 풀의 모든 요청에 대해 보장되는 평균 CPU 대역폭을 지정합니다. 범위는 0에서 100까지입니다.  
  
 **최대 CPU(%)**  
 CPU 충돌이 있을 때 이 리소스 풀의 모든 요청이 받는 최대 평균 CPU 대역폭을 지정합니다. 범위는 0에서 100까지입니다. 기본 설정은 100입니다.  
  
 **최소 메모리(%)**  
 다른 리소스 풀과 공유할 수 없으며 이 리소스 풀에 예약된 최소 메모리 양을 지정합니다. 범위는 0에서 100까지입니다.  
  
 **최대 메모리(%)**  
 이 리소스 풀의 요청에서 사용할 수 있는 총 서버 메모리를 지정합니다. 범위는 0에서 100까지입니다. 기본 설정은 100입니다.  
  
 자세한 내용은 [CREATE RESOURCE POOL &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql)합니다.  
  
 **리소스 풀의 작업 그룹**  
 제공된 표를 사용하여 작업 그룹 구성을 만들거나 변경합니다. 이 표는 미리 정의된 내부 그룹 및 기본 그룹에 대한 정보로 채워집니다. 풀의 행에 있는 첫 번째 열을 클릭하여 작업할 그룹을 선택합니다. 새 작업 그룹을 만들려면 접두사로 별표는 행을 클릭 합니다 (**&#42;**).  
  
 **이름**  
 작업 그룹의 이름을 지정합니다.  
  
 **중요도**  
 작업 그룹에 있는 요청의 상대적 중요도를 지정합니다. 사용 가능한 설정은 낮음, 보통 및 높음입니다.  
  
 **최대 요청 수**  
 작업 그룹에서 실행할 수 있는 최대 동시 요청 수를 지정합니다. 0 또는 양의 정수여야 합니다.  
  
 **CPU 시간(초)**  
 요청이 사용할 수 있는 최대 CPU 시간을 지정합니다. 0 또는 양의 정수여야 합니다. 0이면 시간에 제한이 없습니다.  
  
 **메모리 부여(%)**  
 단일 요청이 풀에서 사용할 수 있는 최대 메모리 양을 지정합니다. 범위는 0에서 100까지입니다.  
  
 **부여 제한 시간(초)**  
 쿼리가 실패하기 전에 리소스를 사용할 수 있을 때까지 쿼리가 대기할 수 있는 최대 시간을 지정합니다. 0 또는 양의 정수여야 합니다.  
  
 **병렬 처리 수준**  
 병렬 요청의 최대 DOP(병렬 처리 수준)를 지정합니다. 범위는 0에서 64까지입니다.  
  
 자세한 내용은 [CREATE WORKLOAD GROUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-workload-group-transact-sql)를 참조하세요.  
  
## <a name="view-resource-governor-properties-by-using-transact-sql"></a>Transact-SQL을 사용하여 리소스 관리자 속성 보기  
 **Transact-SQL을 사용하여 리소스 관리자 속성 보기**  
  
1.  Resource Governor 엔터티의 정의를 보려면 [Resource Governor 카탈로그 뷰&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql)를 사용하세요.  
  
2.  Resource Governor 엔터티의 현재 구성을 보려면 [Resource Governor 관련 동적 관리 뷰&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql)를 사용하세요.  
  
## <a name="see-also"></a>관련 항목  
 [리소스 관리자](resource-governor.md)   
 [리소스 관리자 사용](enable-resource-governor.md)   
 [리소스 관리자 리소스 풀](resource-governor-resource-pool.md)   
 [리소스 관리자 작업 그룹](resource-governor-workload-group.md)   
 [리소스 관리자 분류자 함수](resource-governor-classifier-function.md)  
  
  
