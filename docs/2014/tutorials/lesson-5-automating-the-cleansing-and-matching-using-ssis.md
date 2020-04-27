---
title: '5 단원: SSIS를 사용 하 여 정리 및 일치 자동화 | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f068d4db-2d56-41b1-bed2-0cffa3ca411d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ec6f347cdbc6d14e8f621466a1708b8ee9fe7d36
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489750"
---
# <a name="lesson-5-automating-the-cleansing-and-matching-using-ssis"></a>5단원: SSIS를 사용하여 정리 및 일치 자동화
  1 단원에서는 Suppliers 기술 자료를 작성 하 고이를 사용 하 여 2 단원에서 데이터를 정리 하 고 도구 **DQS 클라이언트**를 사용 하 여 3 단원에서 데이터를 일치 시킵니다. 실제 시나리오에서는 dqs가 지원 하지 않는 소스에서 데이터를 끌어오거나 **Dqs 클라이언트** 도구를 사용 하지 않고도 정리 및 일치 프로세스를 자동화 해야 할 수 있습니다. SSIS (SQL Server Integration Services)에는 다양 한 유형의 원본과 **[Dqs 정리 변환](https://msdn.microsoft.com/library/ee677619.aspx)** 구성 요소의 데이터를 통합 하 여 dqs에서 노출 하는 정리 기능을 호출 하는 데 사용할 수 있는 구성 요소가 있습니다. 현재 DQS는 사용할 SSIS에 대해 일치 하는 기능을 제공 하지 않지만 **[유사 항목 그룹화 변환을](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)** 사용 하 여 데이터에서 중복 항목을 식별할 수 있습니다.  
  
 **엔터티 기반 준비 기능**을 사용 하 여 MDS에 데이터를 업로드할 수 있습니다. MDS에서 엔터티를 만들면 해당 준비 테이블 및 저장 프로시저가 자동으로 생성됩니다. 예를 들어 공급자 엔터티를 만들 때 **supplier_Leaf** 테이블과 **stg. udp_Supplier_Leaf** 저장 프로시저가 자동으로 생성 됩니다. 준비 테이블 및 프로시저를 사용하여 엔터티 멤버를 만들고, 업데이트 및 삭제합니다. 이 단원에서는 Supplier 엔터티에 대해 새로운 엔터티 멤버를 만듭니다. 데이터를 MDS 서버에 로드하기 위해 SSIS 패키지는 먼저 데이터를 stg.supplier_Leaf 준비 테이블에 로드한 후 연관된 저장 프로시저인 stg.udp_Supplier_Leaf를 트리거합니다. 자세한 내용은 [데이터 가져오기](../master-data-services/overview-importing-data-from-tables-master-data-services.md) 를 참조 하세요.  
  
 이 단원에서는 다음 작업을 수행합니다.  
  
1.  MDS에서 공급자 데이터를 제거합니다(이전 4개 단원을 모두 수행한 경우). 이 단원에서 만드는 SSIS 패키지는 데이터를 MDS에 자동으로 업로드합니다. 이전에는 DQS 클라이언트를 사용해서 MDS 서버에 정리 및 일치된 공급자 데이터를 수동으로 업로드했습니다.  
  
2.  Supplier 엔터티의 데이터를 다른 애플리케이션에 노출하기 위해 Supplier 엔티터에 구독 뷰를 만듭니다. 이 작업을 수행하면 SQL Server Management Studio를 사용해서 확인할 수 있는 SQL 뷰가 생성됩니다. 이 버전의 자습서에서는 이 뷰를 사용하지 않습니다.  
  
3.  **SQL Server Data Tools**를 사용 하 여 SSIS 프로젝트를 만들고 실행 합니다. 프로젝트는 **데이터 정리** 변환을 사용 하 여 dqs 서버에 정리 요청을 제출 합니다. DQS에서는 일치 기능이 아직 노출 되지 않으므로 **유사 항목 그룹화** 변환을 사용 하 여 중복 항목을 식별 합니다.  
  
4.  마스터 데이터 관리자를 사용해서 MDS에 데이터가 생성되었는지 확인합니다.  
  
5.  SSIS 패키지로 생성된 DQS 정리 프로젝트에서 결과를 검토하고 필요에 따라 대화형 정리를 수행해서 기술 자료를 추가로 작성합니다.  
  
## <a name="next-step"></a>다음 단계  
 [작업 1 &#40;필수 구성 요소&#41;: MDS에서 공급자 데이터 제거](../../2014/tutorials/task-1-prerequisite-removing-supplier-data-in-mds.md)  
  
  
