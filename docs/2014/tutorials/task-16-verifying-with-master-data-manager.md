---
title: '태스크 16: 마스터 데이터 관리자에서 확인 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 57ad9d3e-8f95-4df6-af01-c291ccf49164
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 36220f21f3e2e28d75ff546857fd87b1e71436f1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088499"
---
# <a name="task-16-verifying-with-master-data-manager"></a>태스크 16: 마스터 데이터 관리자에서 확인
  이 작업에서는 SSIS 패키지에서 제출된 일괄 처리 작업의 상태를 확인하고 마스터 데이터 관리자를 사용해서 MDS 서버에 데이터가 업로드되었는지 확인합니다.  
  
1.  시작 **마스터 데이터 관리자** ([http://localhost/MDS](http://localhost/MDS)). 이미 열려 있으면 클릭 **Microsoft SQL Server Master Data Services** 위쪽으로 전환 하는 **홈 페이지**합니다.  
  
2.  클릭 **통합 관리**합니다.  
  
3.  포함 된 일괄 처리는 명명 된 **EIMBatch** 목록에 제출 합니다. 클릭 **데이터 가져오기** 다음 화면이 표시 되지 않으면 메뉴 모음에서 합니다.  
  
     ![EIM 일괄 처리](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "EIM 일괄 처리")  
  
4.  클릭 하 여 홈 페이지로 전환 **SQL Server 2012 Master Data Services** 위쪽에 있습니다.  
  
5.  다음 사항을 확인 **Suppliers** 에 대 한 모델을 선택 **모델** 및 **VERSION_1** 에 대해 선택 된 **버전**를 클릭 하 고  **탐색기**합니다.  
  
6.  MDS로 가져온 데이터 SSIS 패키지를 볼 수 있습니다. 데이터 정리 되 고 중복 요소가 없어야 함 **코드** 값 (참고: **SupplierID** Excel의 열에 해당 **코드** MDS의 Supplier 엔터티에 특성).  
  
## <a name="next-step"></a>다음 단계  
 [태스크 17: SSIS 패키지로 생성된 DQS 정리 프로젝트 검토](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  