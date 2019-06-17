---
title: '태스크 2: Excel 열을 DQS 도메인 매핑 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f347cc92-950f-4021-b7af-393640dfe821
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 29d45e06dcd3e67af3abbc6b356d44877e40f46b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484701"
---
# <a name="task-2-mapping-excel-columns-to-dqs-domains"></a>태스크 2: Excel 열을 DQS 도메인으로 매핑
    
1.  **맵** 페이지에서 **데이터 원본** 에 대해 **Excel 파일**을 선택합니다.  
  
2.  클릭 **찾아보기**를 선택 **Suppliers.xlsx**를 클릭 하 고 **열기**합니다.  
  
3.  선택 **IncomingSuppliers$** 에 대 한 합니다 **워크시트**합니다.  
  
4.  다음 표 및 스크린 샷에 표시된 대로 열을 매핑합니다. 에 대 한 매핑을 만들 때는 합니다 **상태** 도메인 클릭 **열 매핑 추가** 목록 바로 위에 있는 도구 모음 단추입니다.  
  
    > [!TIP]  
    >  사용 하지 않는 **Supplier ID** 열/도메인에 대 한 정리 합니다. 사용 합니다 **Supplier ID** 일치 작업에서 나중에 도메인입니다.  
  
    |Excel 열|DQS 도메인|  
    |------------------|----------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|Contact Email|  
    |Address Line|Address Line|  
    |City|City|  
    |State|State|  
    |국가 (클릭 **(열 매핑 추가) +** 행을 추가 하려면 도구 모음)|Country|  
    |Zip Code|Zip|  
  
     ![Excel 열에서 도메인으로의 매핑을](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-01.jpg "Excel 열에서 도메인으로의 매핑")  
  
5.  내 모든 개별 도메인을 매핑 했으므로 합니다 **Address Validation** 복합 도메인을 복합 도메인 정리 프로세스에 자동으로 참여 합니다. 클릭 **복합 도메인 보기/선택** 에서 볼 수 있듯이 단추를 **Address Validation** 복합 도메인은 자동으로 선택 및 클릭 **확인**합니다.  
  
     ![복합 도메인 보기/선택 상자](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-02.jpg "복합 도메인 보기/선택 상자")  
  
6.  클릭 **다음** 으로 전환 합니다 **정리** 페이지입니다.  
  
## <a name="next-step"></a>다음 단계  
 [작업 3: Suppliers 기술 자료에 대해 데이터 정리](../../2014/tutorials/task-3-cleansing-data-against-the-suppliers-knowledge-base.md)  
  
  
