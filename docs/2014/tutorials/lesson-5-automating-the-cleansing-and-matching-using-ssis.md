---
title: '5 단원: 정리 및 SSIS를 사용 하 여 일치를 자동화 | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f068d4db-2d56-41b1-bed2-0cffa3ca411d
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 00dff9ac204e5e1b86feafc51da643222bce1758
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080552"
---
# <a name="lesson-5-automating-the-cleansing-and-matching-using-ssis"></a>5단원: SSIS를 사용하여 정리 및 일치 자동화
  1 단원에서는 Suppliers 기술 자료를 작성 하 고이 2 단원에서에서 데이터를 정리 및 데이터 도구를 사용 하는 3 단원에서에서 일치 사용 **DQS 클라이언트**합니다. 실제 시나리오에서를 사용할 필요 없이 원본에 DQS에서 지원 하지 않거나 자동화 된 정리 및 일치 프로세스에서 데이터를 가져올 할 수는 **DQS 클라이언트** 도구입니다. SQL Server Integration Services (SSIS)에 다양 한 이기종 원본 으로부터 데이터를 통합 하는 데 사용할 수 있는 구성 요소가 및 **[하이퍼링크 "http://msdn.microsoft.com/library/ee677619.aspx" \t "_blank" DQS 정리 변환](http://msdn.microsoft.com/library/ee677619.aspx)** DQS에 의해 노출 되는 정리 기능을 호출 하는 구성 요소입니다. 현재, DQS를 사용 하려면 SSIS에 대 한 일치 하는 기능을 노출 하지 않습니다. 하지만 사용할 수 있습니다는 **[유사 항목 그룹화 변환](http://msdn.microsoft.com/library/ms141764.aspx)** 데이터의 중복을 식별 하 합니다.  
  
 사용 하 여 MDS에 데이터를 업로드할 수는 **엔터티 기반 준비 기능**합니다. MDS에서 엔터티를 만들면 해당 준비 테이블 및 저장 프로시저가 자동으로 생성됩니다. 예를 들어 Supplier 엔터티를 만들 때의 **stg.supplier_Leaf** 테이블 및 **stg.udp_Supplier_Leaf** 자동으로 생성 된 저장된 프로시저입니다. 준비 테이블 및 프로시저를 사용하여 엔터티 멤버를 만들고, 업데이트 및 삭제합니다. 이 단원에서는 Supplier 엔터티에 대해 새로운 엔터티 멤버를 만듭니다. 데이터를 MDS 서버에 로드하기 위해 SSIS 패키지는 먼저 데이터를 stg.supplier_Leaf 준비 테이블에 로드한 후 연관된 저장 프로시저인 stg.udp_Supplier_Leaf를 트리거합니다. 참조 [데이터 가져오기](http://msdn.microsoft.com/library/ee633726.aspx) 내용을 확인 합니다.  
  
 이 단원에서는 다음 작업을 수행합니다.  
  
1.  MDS에서 공급자 데이터를 제거합니다(이전 4개 단원을 모두 수행한 경우). 이 단원에서 만드는 SSIS 패키지는 데이터를 MDS에 자동으로 업로드합니다. 이전에는 DQS 클라이언트를 사용해서 MDS 서버에 정리 및 일치된 공급자 데이터를 수동으로 업로드했습니다.  
  
2.  Supplier 엔터티의 데이터를 다른 응용 프로그램에 노출하기 위해 Supplier 엔티터에 구독 뷰를 만듭니다. 이 작업을 수행하면 SQL Server Management Studio를 사용해서 확인할 수 있는 SQL 뷰가 생성됩니다. 이 버전의 자습서에서는 이 뷰를 사용하지 않습니다.  
  
3.  만들기 및 사용 하 여 SSIS 프로젝트를 실행 **SQL Server Data Tools**합니다. 프로젝트에서는 **데이터 정리** DQS 서버에 정리 요청을 제출 하는 변환입니다. 사용 하도록 DQS 일치 기능을 아직 노출 하지 않습니다 **유사 항목 그룹화** 중복을 식별 하는 변환입니다.  
  
4.  마스터 데이터 관리자를 사용해서 MDS에 데이터가 생성되었는지 확인합니다.  
  
5.  SSIS 패키지로 생성된 DQS 정리 프로젝트에서 결과를 검토하고 필요에 따라 대화형 정리를 수행해서 기술 자료를 추가로 작성합니다.  
  
## <a name="next-step"></a>다음 단계  
 [작업 1 &#40;필수&#41;: MDS에서 공급자 데이터 제거](../../2014/tutorials/task-1-prerequisite-removing-supplier-data-in-mds.md)  
  
  