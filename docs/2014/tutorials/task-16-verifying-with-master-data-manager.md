---
title: '작업 16: 마스터 데이터 관리자로 확인 | 마이크로 소프트 문서'
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
ms.openlocfilehash: d9828c02625ae2bc5a85859577a237b4c4fa99c5
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484683"
---
# <a name="task-16-verifying-with-master-data-manager"></a>태스크 16: 마스터 데이터 관리자에서 확인
  이 작업에서는 SSIS 패키지에서 제출된 일괄 처리 작업의 상태를 확인하고 마스터 데이터 관리자를 사용해서 MDS 서버에 데이터가 업로드되었는지 확인합니다.  
  
1.  마스터 데이터 관리자`http://localhost/MDS` **()를** 시작합니다. 이미 열려 있는 경우 상단의 **Microsoft SQL Server 마스터 데이터 서비스를** 클릭하여 홈 **페이지로**전환합니다.  
  
2.  **통합 관리를 클릭합니다.**  
  
3.  목록에 제출한 **EIMBatch라는** 일괄 처리가 있습니다. 다음 화면이 표시되지 않으면 메뉴 모음에서 **데이터 가져오기를** 클릭합니다.  
  
     ![EIM Batch](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "EIM Batch")  
  
4.  상단에 있는 SQL Server **2012 마스터 데이터 서비스를** 클릭하여 홈 페이지로 다시 전환합니다.  
  
5.  **공급자** 모델이 **모델에** 대해 선택되어 있고 **버전에** **VERSION_1** 선택되었는지 확인하고 **탐색기를**클릭합니다.  
  
6.  MDS로 가져온 데이터 SSIS 패키지를 볼 수 있습니다. 데이터를 정리해야 하며 중복 **코드** 값이 없어야 합니다(참고: Excel의 **SupplierID** 열은 MDS의 공급자 엔터티의 **코드** 특성에 해당함).  
  
## <a name="next-step"></a>다음 단계  
 [태스크 17: SSIS 패키지로 생성된 DQS 정리 프로젝트 검토](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
