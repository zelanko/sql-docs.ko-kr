---
title: "데이터 과학 클라이언트 설정 | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d15ee956-918f-40e0-b986-2bf929ef303a
caps.latest.revision: 14
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# 데이터 과학 클라이언트 설정
  **R Services(In-Database)**를 설치하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스를 구성한 후에는 원격 실행 및 배포를 위해 서버에 연결할 수 있는 R 개발 환경을 설정하는 것이 좋습니다. 
  
  클라이언트 환경에는 SQL Server에서 R의 분산 실행을 지원하는 추가 RevoScaleR 패키지 및 Microsoft R Open이 포함되어 있어야 합니다.  여러 가지 방법으로 이러한 패키지를 설치할 수 있습니다.
  
+ [Microsoft R Client](http://aka.ms/rclient/download)를 설치합니다.
+ Microsoft R Server를 설치합니다. SQL Server 설치 프로그램 또는 독립 실행형 설치 관리자에서 Microsoft R Server를 가져올 수 있습니다. 자세한 내용은 [독립 실행형 R 서버 만들기](../../advanced-analytics/r-services/create-a-standalone-r-server.md) 또는 [R 서버 소개](https://msdnstage.redmond.corp.microsoft.com/en-us/microsoft-r/rserver?branch=r-server-nov16-dev)를 참조하세요.

 Microsoft R Client를 사용하여 ScaleR 패키지로 SQL Server에 연결하는 방법에 대한 자세한 내용은 [ScaleR 시작](https://msdn.microsoft.com/microsoft-r/scaler-getting-started#)을 참조하세요.  
  
 R 코드 원격 실행을 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 방법을 확인할 수 있는 자세한 연습은 [데이터 과학 심층 분석: RevoScaleR 패키지 사용](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md) 자습서를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server R Services&#40;In-Database&#41; 설치](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  