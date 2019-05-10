---
title: '태스크 16: 마스터 데이터 관리자에서 확인 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 57ad9d3e-8f95-4df6-af01-c291ccf49164
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 35dd2da7f6cf6598918cd9d109b97f3d314556d1
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65484696"
---
# <a name="task-16-verifying-with-master-data-manager"></a>태스크 16: 마스터 데이터 관리자에서 확인
  이 작업에서는 SSIS 패키지에서 제출된 일괄 처리 작업의 상태를 확인하고 마스터 데이터 관리자를 사용해서 MDS 서버에 데이터가 업로드되었는지 확인합니다.  
  
1.  시작할 **마스터 데이터 관리자** ([http://localhost/MDS](http://localhost/MDS)). 이미 열려 있으면 클릭 **Microsoft SQL Server Master Data Services** 전환 하려면 위쪽의 **홈페이지**합니다.  
  
2.  클릭 **통합 관리**합니다.  
  
3.  사용 하 여 일괄 처리는 명명 된 **EIMBatch** 목록에 전송 합니다. 클릭 **데이터 가져오기** 다음과 같은 화면이 표시 되지 않으면 메뉴 모음에서.  
  
     ![EIM 일괄](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "EIM 일괄 처리")  
  
4.  클릭 하 여 홈 페이지로 다시 전환 **SQL Server 2012 Master Data Services** 맨 위에 있는 합니다.  
  
5.  했는지 **공급 업체** 에 대 한 모델을 선택한 **모델** 및 **VERSION_1** 가 선택 **버전**를 클릭 하 고  **탐색기**합니다.  
  
6.  MDS로 가져온 데이터 SSIS 패키지를 볼 수 있습니다. 데이터를 정리할 해야 하 고 중복 요소가 없어야 **코드** 값 (참고: **SupplierID** Excel의 열에 해당 **코드** MDS의 Supplier 엔터티에 특성).  
  
## <a name="next-step"></a>다음 단계  
 [태스크 17: SSIS 패키지에서 프로젝트 생성 된 DQS 정리를 검토합니다.](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
