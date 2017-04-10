---
title: "1단원: 샘플 구독자 데이터베이스 만들기 | Microsoft Docs"
ms.custom: ""
ms.date: "05/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 47a882b7-efe5-4ee6-bef4-06118eb56903
caps.latest.revision: 45
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 45
---
# 1단원: 샘플 구독자 데이터베이스 만들기
이 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 자습서 단원에서는 작은 "구독자" 데이터베이스를 만들어 데이터 기반 구독에서 사용할 구독 데이터를 저장합니다. 구독을 처리할 때 보고서 서버에서는 이 데이터를 검색하여 보고서 출력을 사용자 지정하는 데 사용합니다. 예를 들어 데이터 행에 필터에서 사용할 특정 주문 번호가 있고 보고서를 생성한 파일 형식이 보고서를 만들 때 포함됩니다.  
  
이 단원에서는 [!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)]를 사용하여 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 데이터베이스를 만든다고 가정합니다.  
  
### 예제 구독자 데이터베이스를 만들려면  
  
1.  [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]를 시작한 다음 [!INCLUDE[ssDEnoversion_md](../includes/ssdenoversion-md.md)] 인스턴스에 대한 연결을 엽니다.  
  
2.  데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터베이스...**를 선택합니다.  
  
3.  새 데이터베이스 대화 상자의 **데이터베이스 이름**에 *Subscribers*를 입력합니다. 
4. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  도구 모음에서 **새 쿼리** 단추를 클릭합니다.  
  
6.  다음 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 빈 쿼리에 복사합니다.  
  
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
  
7.  **! 실행**을 도구 모음에서 클릭합니다.  
  
8.  SELECT 문을 사용하여 세 개의 데이터 행이 있는지 확인합니다. 예를 들어 `select * from OrderInfo`  
  
## 다음 단계  
+ 보고서 배포를 추진하고 구독자마다 보고서 출력을 다르게 할 구독 데이터를 만들었습니다. 
+ 다음에는 저장된 자격 증명을 사용하도록 보고서의 데이터 원본 속성을 수정합니다. 
+ 또한 구독에서 구독자 데이터와 함께 사용할 매개 변수를 포함하도록 보고서 디자인을 수정합니다. [2단원: 보고서 데이터 원본 속성 수정](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md).  
  
## 참고 항목  
[데이터 기반 구독 만들기&#40;SSRS 자습서&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
[데이터베이스 만들기](../relational-databases/databases/create-a-database.md)  
[기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  
  
  
