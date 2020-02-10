---
title: '작업 3: 일치에 대 한 데이터 품질 프로젝트 만들기 및 실행 | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6260e911-ea8b-4c69-a39d-d1bccd565a32
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ca7c735f00f4fa5c7baf102b26edb6634f57b90f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489236"
---
# <a name="task-3-creating-and-running-a-data-quality-project-for-matching"></a>태스크 3: 일치에 대한 데이터 품질 프로젝트 만들기 및 실행
  이 작업에서는 일치 작업을 위한 데이터 품질 프로젝트를 만들고 정리된 공급자 데이터에서 일치 프로세스를 실행하여 데이터에 있는 모든 중복 항목을 제거합니다.  
  
1.  
  **DQS 클라이언트**의 기본 페이지에서 **새 데이터 품질 프로젝트**를 클릭합니다.  
  
2.  
  **프로젝트 이름** 에서 **Remove Supplier Duplicates**를 입력합니다.  
  
3.  
  **기술 자료 사용** 필드의 KB 목록에서 **Suppliers** 를 선택합니다. 이 기술 자료의 일치 정책은 이전 단원에서 만들었습니다.  
  
4.  오른쪽 하단 창의 **작업 목록** 에서 **일치** 를 선택합니다.  
  
     ![새 데이터 품질 프로젝트 - 선택한 일치하는 항목](../../2014/tutorials/media/et-creatingandrunningadqpformatching.jpg "새 데이터 품질 프로젝트 - 선택한 일치하는 항목")  
  
5.  **다음**을 클릭합니다.  
  
6.  
  **맵** 페이지에서 **데이터 원본** 에 대해 **Excel 파일**을 선택합니다.  
  
7.  
  **찾아보기** 를 클릭하고 정리 작업의 출력 파일인 **Cleansed Supplier List.xls**를 선택합니다.  
  
8.  
  **SupplierID** 원본 열을 **Supplier ID** 도메인에 매핑하고, **Supplier Name** 열을 **Supplier Name** 도메인에 매핑하고, **ContactEmailAddress** 열을 **Contact Email** 도메인에 매핑합니다.  
  
9. 
  **다음** 을 클릭하여 **일치** 페이지로 전환합니다.  
  
10. 
  **시작** 을 클릭하여 일치 프로세스를 시작합니다. 일치 정책을 정의할 때와 동일한 입력 파일이 사용되었으므로 이전 작업과 비슷한 결과가 표시됩니다.  
  
11. 모든 일치 레코드 및 일치 점수를 목록 상자에서 검토합니다. 결과는 이전 작업에서 표시된 것과 동일해야 합니다. 이 일치 작업의 결과를 분석하려면 이전 작업의 단계를 참조하십시오.  
  
12. 
  **다음** 을 클릭하여 **내보내기** 페이지로 전환합니다.  
  
## <a name="next-step"></a>다음 단계  
 [작업 4: 일치 작업의 결과를 Excel 파일로 내보내기](../../2014/tutorials/task-4-exporting-the-results-from-matching-activity-to-an-excel-file.md)  
  
  
