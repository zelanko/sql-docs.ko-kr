---
title: "Microsoft R Server(독립 실행형) 시작 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fc7874c6900474c7c2f3d927183616b2f5e69699
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="getting-started-with-microsoft-r-server-standalone"></a>Microsoft R Server(독립 실행형) 시작
  Microsoft R Server(독립 실행형)는 고성능 분석 솔루션 및 기타 비즈니스 응용 프로그램과의 통합이 가능하도록 인기 있는 R 언어를 엔터프라이즈에서 사용할 수 있도록 도와줍니다.  

  
## <a name="install-microsoft-r-server"></a>Microsoft R Server 설치 

Microsoft R Server를 설치하는 방법은 응용 프로그램에서 SQL Server 데이터를 사용해야 하는지 여부에 따라 달라집니다. 이 경우 SQL Server 설치 프로그램을 사용하여 설치해야 합니다. SQL Server 데이터를 사용하지 않거나 데이터베이스에서 R 코드를 실행할 필요가 없는 경우 SQL Server 설치 프로그램 또는 새 독립 실행형 설치 관리자 중 하나를 사용할 수 있습니다.
 
 
+ SQL Server 설치 프로그램에서 Microsoft R Server(독립 실행형)를 설치합니다. R Server에 대해 R 이진 파일의 별도 인스턴스가 생성되고 SQL Server Enterprise Edition 지원 정책을 통해 사용이 허가됩니다. 자세한 내용은 [독립 실행형 R 서버 만들기](../../advanced-analytics/r-services/create-a-standalone-r-server.md)를 참조하세요.  

+ 새 독립 실행형 Windows Installer를 통해 Microsoft 최신 소프트웨어 수명 주기 지원 정책을 사용하는 Microsoft R Server의 새 인스턴스를 만듭니다. 자세한 내용은 [Windows용 Microsoft R Server 실행](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)을 참조하세요.

+ 업그레이드하려는 R Server(독립 실행형) 또는 R Services의 기존 인스턴스가 있는 경우 해당 업데이트에 대한 Windows 기반 설치 관리자도 다운로드하여 실행해야 합니다. 자세한 내용은 [Windows용 Microsoft R Server 실행](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)을 참조하세요.
  
## <a name="install-additional-r-tools"></a>추가 R 도구 설치  

 무료 [Microsoft R Client](http://aka.ms/rclient/download)(다운로드)를 사용하는 것이 좋습니다.  

 기본 R 개발 환경을 사용하여 SQL Server R Services 또는 Microsoft R Server에 대한 솔루션을 개발할 수도 있습니다. 자세한 내용은 [R 도구 설치 또는 구성](../../advanced-analytics/r-services/setup-or-configure-r-tools.md)을 참조하세요. 
 

### <a name="location-of-r-server-binaries"></a>R Server 이진 파일의 위치

Microsoft R Server 설치에 사용하는 방법에 따라 기본 위치가 달라집니다. 원하는 개발 환경을 사용하기 전에 R 라이브러리를 설치한 위치를 확인합니다.

+ 새 Windows Installer를 사용하여 설치된 Microsoft R Server

  `C:\Program Files\Microsoft\R Server\R_SERVER`

+ SQL Server 설치 프로그램을 통해 설치된 R Server(독립 실행형)

  `C:\Program Files\Microsoft SQL Server\130\R_SERVER`

+ R Services(In-Database)

  `C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`
      
## <a name="start-using-r-on-microsoft-r-server"></a>Microsoft R Server에서 R 사용 시작  

 서버 구성 요소를 설치하고 R Server 이진 파일을 사용하도록 IDE를 구성한 후 RevoScaleR 패키지, MicrosoftML, olapR 등의 새로운 API를 사용하여 솔루션 개발을 시작할 수 있습니다.
    
R Server를 시작하려면 MSDN 라이브러리에서 [R Server - 시작](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) 가이드를 참조하세요.   
  
-   [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started): R 솔루션에 고성능 및 확장성을 제공하는 이 배포 가능한 분석 함수 컬렉션을 탐색합니다. K-means 클러스터링, 의사 결정 트리, 의사 결정 포리스트, 데이터 조작 도구 등 가장 많이 사용되는 R 모델링 패키지의 병렬 처리 버전을 포함합니다. 자세한 내용은 [Explore R and ScaleR in 25 Functions](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started-tutorial)(25개 함수에서 R 및 ScaleR 알아보기)를 참조하세요.  
    
- [MicrosoftML](https://msdn.microsoft.com/library/mt790482.aspx): MicrosoftML 패키지는 Microsoft에서 개발된 빠르고 확장 가능한 새로운 기계 학습 알고리즘 및 변환 집합입니다. 자세한 내용은 [MicrosoftML 함수](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)를 참조하세요.
  


  
## <a name="see-also"></a>참고 항목  
 [SQL Server R Services 시작](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  

