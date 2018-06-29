---
title: '작업 2: Excel 열을 DQS 도메인에 매핑하고 | Microsoft Docs'
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
ms.assetid: f347cc92-950f-4021-b7af-393640dfe821
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ff48d56555d3eca2bbcb961d753a47d8db38c69e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185095"
---
# <a name="task-2-mapping-excel-columns-to-dqs-domains"></a>태스크 2: Excel 열을 DQS 도메인에 매핑
    
1.  **맵** 페이지에서 **데이터 원본** 에 대해 **Excel 파일**을 선택합니다.  
  
2.  클릭 **찾아보기**선택, **Suppliers.xlsx**를 클릭 하 고 **열려**합니다.  
  
3.  선택 **IncomingSuppliers$** 에 대 한는 **워크시트**합니다.  
  
4.  다음 표 및 스크린 샷에 표시된 대로 열을 매핑합니다. 에 대 한 매핑을 만들 때의 **상태** 도메인을 클릭 하 여 **열 매핑 추가** 목록 바로 위에 있는 도구 모음에서 단추를 합니다.  
  
    > [!TIP]  
    >  사용 하지 않는 **Supplier ID** 열/도메인에 대 한 정리 합니다. 사용 하 여는 **Supplier ID** 일치 작업의 뒷부분에 나오는 도메인입니다.  
  
    |Excel 열|DQS 도메인|  
    |------------------|----------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|Contact Email|  
    |Address Line|Address Line|  
    |City|City|  
    |State|State|  
    |국가 (클릭 **(열 매핑 추가) +** 행을 추가 하려면 도구 모음)|Country|  
    |Zip Code|Zip|  
  
     ![Excel 열에서 도메인으로의 매핑을](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-01.jpg "의 도메인을 Excel 열 매핑")  
  
5.  내 모든 개별 도메인을 매핑한 대로 **Address Validation** 복합 도메인을 복합 도메인 정리 프로세스에 자동으로 참여 합니다. 클릭 **복합 도메인 보기/선택** 단추에서 볼 수 있듯이 **Address Validation** 복합 도메인을 자동으로 선택 되며 클릭 **확인**합니다.  
  
     ![복합 도메인 보기/선택](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-02.jpg "보기/선택 복합 도메인 대화 상자")  
  
6.  클릭 **다음** 전환할 수는 **Cleanse** 페이지.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 3: 공급자 기술 자료에 대한 데이터 정리](../../2014/tutorials/task-3-cleansing-data-against-the-suppliers-knowledge-base.md)  
  
  