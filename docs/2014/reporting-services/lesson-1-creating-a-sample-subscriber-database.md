---
title: '1단원: 샘플 구독자 데이터베이스 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 47a882b7-efe5-4ee6-bef4-06118eb56903
caps.latest.revision: 41
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: c1b01246166c6d7e75f1083fc23b9bd15502c731
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082008"
---
# <a name="lesson-1-creating-a-sample-subscriber-database"></a>1단원: 샘플 구독자 데이터베이스 만들기
  데이터 기반 구독을 정의하려면 먼저 구독 데이터를 제공하는 데이터 원본이 있어야 합니다. 이 단계에서는 이 자습서에 사용되는 구독 데이터를 저장할 소규모 데이터베이스를 만듭니다. 나중에 구독을 처리할 때 보고서 서버에서는 이 데이터를 검색하여 보고서 출력, 배달 옵션 및 보고서 표시 형식을 사용자 지정하는 데 사용합니다.  
  
 이 단원에서는 사용 하는 가정 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 만들려는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 데이터베이스입니다.  
  
### <a name="to-create-a-sample-subscriber-database"></a>예제 구독자 데이터베이스를 만들려면  
  
1.  [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]를 시작한 다음 [!INCLUDE[ssDE](../includes/ssde-md.md)]에 연결합니다.  
  
2.  데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터베이스...** 를 선택합니다.  
  
3.  새 데이터베이스 대화 상자의 데이터베이스 이름에서 입력 *구독자*합니다. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  도구 모음에서 **새 쿼리** 단추를 클릭합니다.  
  
5.  다음 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 빈 쿼리에 복사합니다.  
  
    ```  
    Use Subscribers  
    CREATE TABLE [dbo].[OrderInfo] (  
        [SubscriptionID] [int] NOT NULL PRIMARY KEY ,  
        [Order] [nvarchar] (20) NOT NULL,  
        [FileType] [bit],  
        [Format] [nvarchar] (20) NOT NULL ,  
    ) ON [PRIMARY]  
    GO  
  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('1', 'so43659', '1', 'IMAGE')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('2', 'so43664', '1', 'MHTML')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('3', 'so43668', '1', 'PDF')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('4', 'so71949', '1', 'Excel')  
    GO  
    ```  
  
6.  **! 실행**을 도구 모음에서 클릭합니다.  
  
7.  SELECT 문을 사용하여 세 개의 데이터 행이 있는지 확인합니다. 예를 들어 `select * from OrderInfo`  
  
## <a name="next-steps"></a>다음 단계  
 보고서 배포를 추진하고 구독자마다 보고서 출력을 다르게 할 구독 데이터를 만들었습니다. 다음 단원에서는 구독자에게 배포할 보고서의 데이터 원본 속성을 수정합니다. 데이터 원본 속성 수정은 데이터 기반 구독 배달에 사용할 보고서를 준비하기 위해 수행됩니다. 또한 구독에서 구독자 데이터와 함께 사용할 매개 변수를 포함하도록 보고서 디자인을 수정합니다. [2단원: 보고서 데이터 원본 속성 수정](lesson-2-modifying-the-report-data-source-properties.md).  
  
## <a name="see-also"></a>관련 항목  
 [데이터 기반 구독 만들기&#40;SSRS 자습서&#41;](create-a-data-driven-subscription-ssrs-tutorial.md)   
 [데이터베이스 만들기](../relational-databases/databases/create-a-database.md)   
 [기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;](create-a-basic-table-report-ssrs-tutorial.md)  
  
  