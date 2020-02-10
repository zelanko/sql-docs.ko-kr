---
title: '태스크 2: Excel 열을 DQS 도메인에 매핑 | Microsoft Docs'
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484701"
---
# <a name="task-2-mapping-excel-columns-to-dqs-domains"></a>태스크 2: Excel 열을 DQS 도메인에 매핑
    
1.  
  **맵** 페이지에서 **데이터 원본** 에 대해 **Excel 파일**을 선택합니다.  
  
2.  **찾아보기**를 클릭 하 고 **Suppliers .xlsx**를 선택 하 고 **열기**를 클릭 합니다.  
  
3.  **워크시트**에 대해 **IncomingSuppliers $** 를 선택 합니다.  
  
4.  다음 표 및 스크린 샷에 표시된 대로 열을 매핑합니다. **상태** 도메인에 대 한 매핑을 만들 때 목록 바로 위에 있는 도구 모음에서 **열 매핑 추가** 단추를 클릭 합니다.  
  
    > [!TIP]  
    >  정리에 **공급자 ID** 열/도메인을 사용 하지 않습니다. 나중에 일치 작업에서 **공급자 ID** 도메인을 사용 합니다.  
  
    |Excel 열|DQS 도메인|  
    |------------------|----------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|담당자 이메일|  
    |Address Line|Address Line|  
    |City|City|  
    |시스템 상태|시스템 상태|  
    |Country ( **+ (열 매핑 추가)** 도구 모음을 클릭 하 여 행 추가)|국가|  
    |Zip Code|Zip|  
  
     ![Excel 열에서 도메인으로 매핑](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-01.jpg "Excel 열에서 도메인으로 매핑")  
  
5.  **주소 유효성 검사** 복합 도메인 내의 개별 도메인을 모두 매핑한 경우 복합 도메인은 정리 프로세스에 자동으로 참여 합니다. **복합 도메인 보기/선택** 단추를 클릭 하 여 **주소 유효성 검사** 복합 도메인이 자동으로 선택 되어 있는지 확인 한 다음 **확인**을 클릭 합니다.  
  
     ![복합 도메인 보기/선택 대화 상자](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-02.jpg "복합 도메인 보기/선택 대화 상자")  
  
6.  **다음** 을 클릭 하 여 **정리** 페이지로 전환 합니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 3: 공급자 기술 자료에 대한 데이터 정리](../../2014/tutorials/task-3-cleansing-data-against-the-suppliers-knowledge-base.md)  
  
  
