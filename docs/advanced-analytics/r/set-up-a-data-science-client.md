---
title: "데이터 과학 클라이언트 설정 | Microsoft 문서"
ms.custom: 
ms.date: 02/10/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d15ee956-918f-40e0-b986-2bf929ef303a
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0661b2fcf9b23d3c81cb0d80f0424d87dbde7ef8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="set-up--a-data-science-client"></a>데이터 과학 클라이언트 설정
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] R Services(In-Database) **를 설치하여**인스턴스를 구성한 후에는 원격 실행 및 배포를 위해 서버에 연결할 수 있는 R 개발 환경을 설정하는 것이 좋습니다. 
  
  이 환경에는 ScaleR 패키지가 포함되어야 하고 선택적으로 클라이언트 개발 환경이 포함될 수 있습니다.
  
 ## <a name="where-to-get-scaler"></a>ScaleR을 가져올 위치 
  
  클라이언트 환경에는 SQL Server에서 R의 분산 실행을 지원하는 추가 RevoScaleR 패키지 및 Microsoft R Open이 포함되어 있어야 합니다.  여러 가지 방법으로 이러한 패키지를 설치할 수 있습니다.
  
+ [Microsoft R Client](http://aka.ms/rclient/download)를 설치합니다. 추가 설치 지침은 [Get Started with Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-get-started)(Microsoft R Client 시작)를 참조하세요.
+ Microsoft R Server를 설치합니다. Microsoft R Server는 SQL Server 설치 프로그램에서 가져오거나 새 독립 실행형 Windows Installer를 사용하여 가져올 수 있습니다. 자세한 내용은 [독립 실행형 R 서버 만들기](../../advanced-analytics/r-services/create-a-standalone-r-server.md) 및 [Introduction to R Server](https://msdn.microsoft.com/microsoft-r/rserver)(R Server 소개)를 참조하세요.

R Server 라이선싱 계약이 있는 경우 Microsoft R Server(독립 실행형)를 사용하여 R 처리 스레드 및 메모리 내 데이터에 대한 제한을 피하는 것이 좋습니다.


## <a name="how-to-set-up-the-r-development-environment"></a>R 개발 환경을 설치하는 방법

Windows와 호환되는 선택한 R 개발 환경을 사용할 수 있습니다. 

+ R Tools for Visual Studio를 Microsoft R Open과 통합할 수 있습니다.
+ RStudio는 많이 사용되는 무료 환경입니다.  

설치한 후 Microsoft R Open 라이브러리를 기본적으로 사용하도록 환경을 다시 구성해야 합니다. 그렇지 않으면 ScaleR 라이브러리에 액세스할 수 없습니다. 자세한 내용은 [Getting Started with Microsoft R Client](http://msdn.microsoft.com/microsoft-r/r-client-get-started)(Microsoft R Client 시작)를 참조하세요.
 
## <a name="more-resources"></a>추가 리소스
  
 R 코드 원격 실행을 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 방법을 확인할 수 있는 자세한 연습은 [데이터 과학 심층 분석: RevoScaleR 패키지 사용](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)자습서를 참조하세요.  
 

SQL Server와 함께 Microsoft R Client 및 ScaleR 패키지 사용을 시작하려면 [ScaleR Getting Started](https://msdn.microsoft.com/microsoft-r/scaler-getting-started#)(ScaleR 시작)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server R Services&#40;In-Database&#41; 설치](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  

