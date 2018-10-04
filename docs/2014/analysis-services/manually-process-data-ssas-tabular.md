---
title: 데이터 (SSAS 테이블 형식)를 수동으로 처리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.datarefreshprogressdb.f1
ms.assetid: 0918c04c-c1e6-45b4-acfa-96fa578e684b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6f87cda5fb38fad586e5272d7d7c3ea255a478b7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189773"
---
# <a name="manually-process-data-ssas-tabular"></a>수동으로 데이터 처리(SSAS 테이블 형식)
  이 항목에서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 작업 영역 데이터를 수동으로 처리하는 방법에 대해 설명합니다.  
  
 외부 데이터를 사용하는 테이블 형식 모델을 제작할 때 처리 명령을 사용하여 데이터를 수동으로 새로 고칠 수 있습니다. 단일 테이블, 모델에 있는 모든 테이블 또는 하나 이상의 파티션을 처리할 수 있습니다. 데이터를 처리할 때마다 데이터를 다시 계산해야 할 수도 있습니다.  데이터 처리는 외부 원본에서 최신 데이터를 가져오는 것을 의미합니다. 다시 계산은 데이터를 사용하는 모든 수식의 결과를 업데이트하는 것을 의미합니다.  
  
 이 항목의 섹션:  
  
-   [수동으로 데이터 처리](#bkmk_mahually_process)  
  
-   [데이터 처리 진행률](#bkmk_data_process_progress)  
  
##  <a name="bkmk_mahually_process"></a> 수동으로 데이터 처리  
  
#### <a name="to-process-data-for-a-single-table-or-all-tables-in-a-model"></a>모델의 단일 테이블 또는 모든 테이블의 데이터를 처리하려면  
  
1.  모델 디자이너에서 처리할 테이블을 클릭합니다.  
  
2.  **모델** 메뉴를 클릭하고 **처리**를 클릭한 다음 **처리** 또는 **모두 처리**를 클릭합니다.  
  
#### <a name="to-process-data-for-all-tables-using-the-same-connection"></a>같은 연결을 사용하는 모든 테이블에 대한 데이터를 처리하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **기존 연결**을 클릭합니다.  
  
2.  **기존 연결** 대화 상자에서 연결을 선택한 다음 **처리**를 클릭합니다.  
  
#### <a name="to-process-data-for-one-or-more-partitions"></a>하나 이상의 파티션에 대한 데이터를 처리하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭하고 **처리**를 가리킨 다음 **파티션 처리**를 클릭합니다.  
  
2.  **파티션 처리** 대화 상자의 **모드**에서 다음 처리 모드 중 하나를 선택합니다.  
  
    |모드|Description|  
    |----------|-----------------|  
    |**기본값 처리**|파티션 개체의 처리 상태를 검색하고 필요한 처리를 수행하여 처리되지 않거나 부분적으로 처리된 파티션 개체를 완전히 처리된 상태로 전달합니다. 빈 테이블 및 파티션에 대한 데이터를 로드하고 계층, 계산 열 및 관계를 작성 또는 다시 작성합니다.|  
    |**전체 처리**|파티션 개체와 여기에 포함된 모든 개체를 처리합니다. 이미 처리된 개체에 대해 전체 처리를 실행하면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 개체의 모든 데이터를 삭제한 다음 개체를 처리합니다. 개체에 구조적 변경이 발생한 경우 이러한 종류의 처리가 필요합니다.|  
    |**데이터 처리**|계층 또는 관계를 다시 작성하거나 계산 열 및 측정값을 다시 계산하지 않고 파티션 또는 테이블에 데이터를 로드합니다.|  
    |**지우기 처리**|파티션에서 모든 데이터를 제거합니다.|  
    |**증분 처리**|새 데이터로 파티션을 증분 업데이트합니다.|  
  
3.  파티션 목록에서 처리할 파티션을 선택한 다음 **확인**을 클릭합니다.  
  
##  <a name="bkmk_data_process_progress"></a> 데이터 처리 진행률  
 **데이터 처리 진행률** 대화 상자를 사용하면 외부 원본에서 모델로 가져온 데이터의 처리 상태를 모니터링할 수 있습니다. 이 대화 상자에 액세스하려면 **모델** 메뉴를 클릭한 다음 **파티션 처리**, **테이블 처리** 또는 **모두 처리**를 클릭합니다.  
  
 **상태**  
 처리 작업의 성공 여부를 나타냅니다.  
  
 **세부 정보**  
 가져온 테이블 또는 뷰 목록, 가져온 행 수 정보, 문제 보고서에 대한 링크를 제공합니다.  
  
 **새로 고침 중지**  
 처리 작업을 중지하려면 클릭합니다. 이 옵션은 작업에 시간이 너무 많이 걸리거나 오류가 너무 많은 경우에 유용합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 처리 &#40;&AMP;#40;SSAS 테이블 형식&#41;](process-data-ssas-tabular.md)   
 [데이터 처리 문제 해결 &#40;&AMP;#40;SSAS 테이블 형식&#41;](troubleshoot-process-data-ssas-tabular.md)  
  
  
