---
title: "복제된 테이블의 차이점 비교(복제 프로그래밍) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "tablediff 유틸리티"
  - "복제된 테이블 비교"
ms.assetid: cd253a17-0c85-42b4-912c-690169ebe799
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 복제된 테이블의 차이점 비교(복제 프로그래밍)
  아티클 유효성 검사는 게시자 및 구독자에서 테이블 아티클의 게시된 데이터가 일치하지 않는지 여부를 확인하는 데 사용됩니다. 자세한 내용은 참조 [복제 된 데이터의 유효성을 검사](../../../relational-databases/replication/validate-replicated-data.md)합니다. 그러나 유효성 검사를 통해서는 성공 또는 실패 정보만 반환되고 원본 테이블과 대상 테이블의 차이점에 대한 정보는 제공되지 않습니다. **tablediff** 명령 프롬프트 유틸리티는 두 테이블 간의 세부 차이점 정보를 반환하며 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트를 생성하여 구독이 게시자의 데이터와 일치하게 할 수도 있습니다.  
  
> [!NOTE]  
>   **tablediff** 유틸리티는에 대 한 지원만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서버입니다.  
  
### tablediff를 사용하여 복제된 테이블의 차이점을 비교하려면  
  
1.  복제 토폴로지에 있는 서버의 명령 프롬프트에서 [tablediff Utility](../../../tools/tablediff-utility.md)를 실행합니다. 다음 매개 변수를 지정합니다.  
  
    -   **-sourceserver** -올바른 것으로 알려진 데이터를 일반적으로 게시자 서버의 이름입니다.  
  
    -   **-sourcedatabase** -올바른 데이터를 포함 하는 데이터베이스의 이름입니다.  
  
    -   **-sourcetable** -비교할 아티클의 원본 테이블의 이름입니다.  
  
    -   (선택 사항) **-sourceschema** -기본 스키마 그렇지 않으면 원본 테이블의 스키마 소유자입니다.  
  
    -   (선택 사항) **-sourceuser** 및 **-sourcepassword** SQL Server 인증을 사용 하 여 게시자에 연결할 때.  
  
        > [!IMPORTANT]  
        >  가능하면 Windows 인증을 사용하세요. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용해야 하는 경우에는 런타임에 사용자에게 보안 자격 증명을 지정하라는 메시지가 표시되도록 하십시오. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
    -   **-destinationserver** -서버에 데이터를 비교 되 고, 일반적으로 구독자의 이름입니다.  
  
    -   **-destinationdatabase** -의 이름에 비교할 데이터베이스입니다.  
  
    -   **-destinationtable** -비교할 테이블의 이름입니다.  
  
    -   (선택 사항) **-destinationschema** -대상 테이블 그렇지 않은 경우 기본 스키마의 스키마 소유자입니다.  
  
    -   (선택 사항) **-destinationuser** 및 **-destinationpassword** 사용 하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 하는 구독자에 연결 합니다.  
  
        > [!IMPORTANT]  
        >  가능하면 Windows 인증을 사용하세요. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용해야 하는 경우에는 런타임에 사용자에게 보안 자격 증명을 지정하라는 메시지가 표시되도록 하십시오. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
    -   (선택 사항) 사용 하 여 **-c** 열 수준 비교를 수행 합니다.  
  
    -   (선택 사항) 사용 하 여 **-q** 행 개수 및 스키마 전용 비교를 수행 하 합니다.  
  
    -   (선택 사항) 파일 이름 및 경로를 지정 **-o** 결과 파일에 출력 합니다.  
  
    -   (선택 사항) 에 대 한 결과를 구독 데이터베이스에서 테이블을 지정 **-et**합니다. 테이블이 이미 있는 경우 지정 **-dt** 를 먼저 테이블을 삭제 합니다.  
  
    -   (선택 사항) 사용 하 여 **-f** 생성 하는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 파일을 게시자의 데이터 일치 하도록 구독자에서 데이터를 수정 합니다. 사용 하 여 **-df** 의 수를 지정 하려면 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 각 파일에 있습니다.  
  
    -   (선택 사항) 사용 하 여 **-rc** 및 **-ri** 작업을 다시 시도 간격을 다시 시도 횟수를 지정할 수 있습니다.  
  
    -   (선택 사항) 사용 하 여 **-엄격한** 원본 테이블과 대상 테이블 간의 엄격한 스키마 비교를 적용 하 합니다.  
  
## 참고 항목  
 [구독자에서 데이터 유효성 검사](../../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  