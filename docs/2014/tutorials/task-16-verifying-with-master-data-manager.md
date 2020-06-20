---
title: '작업 16: 마스터 데이터 관리자을 사용 하 여 확인 Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 57ad9d3e-8f95-4df6-af01-c291ccf49164
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d1649582f97e9e08691726745e4ba14b2f8226bd
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061079"
---
# <a name="task-16-verifying-with-master-data-manager"></a>태스크 16: 마스터 데이터 관리자에서 확인
  이 작업에서는 SSIS 패키지에서 제출된 일괄 처리 작업의 상태를 확인하고 마스터 데이터 관리자를 사용해서 MDS 서버에 데이터가 업로드되었는지 확인합니다.  
  
1.  **마스터 데이터 관리자** ()를 시작 `http://localhost/MDS` 합니다. 이미 열려 있는 경우 맨 위에 있는 **Microsoft SQL Server MDS(Master Data Services)** 를 클릭 하 여 **홈 페이지로**전환 합니다.  
  
2.  **Integration Management**를 클릭 합니다.  
  
3.  목록에서 제출한 **Eimbatch** 라는 이름의 일괄 처리가 있습니다. 다음 화면이 표시 되지 않으면 메뉴 모음에서 **데이터 가져오기** 를 클릭 합니다.  
  
     ![EIM Batch](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "EIM Batch")  
  
4.  맨 위에 있는 **SQL Server 2012 MDS(Master Data Services)** 를 클릭 하 여 홈 페이지로 다시 전환 합니다.  
  
5.  **모델** 에 대해 **Suppliers** 모델을 선택 하 고 **버전**에 대해 **VERSION_1** 를 선택 했는지 확인 하 고 **탐색기**를 클릭 합니다.  
  
6.  MDS로 가져온 데이터 SSIS 패키지를 볼 수 있습니다. 데이터를 정리 하 고 중복 된 **코드** 값을 포함 하지 않아야 합니다 ( **참고: Excel의 공급자 열** 은 MDS의 공급자 엔터티에 대 한 **Code** 특성에 해당).  
  
## <a name="next-step"></a>다음 단계  
 [태스크 17: SSIS 패키지로 생성된 DQS 정리 프로젝트 검토](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
