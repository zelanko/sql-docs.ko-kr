---
title: "Microsoft R Server(독립 실행형) 시작 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 16
---
# Microsoft R Server(독립 실행형) 시작
  Microsoft R Server(독립 실행형)는 고성능 분석 솔루션 및 기타 비즈니스 응용 프로그램과의 통합이 가능하도록 인기 있는 R 언어를 엔터프라이즈에서 사용할 수 있도록 도와줍니다.  
  
## Microsoft R Server란?  
 Microsoft R Server(독립 실행형)는 Revolution Analytics에서 개발한 고급 R 패키지를 포함하며 Hadoop, Teradata를 비롯한 다양한 데이터 원본에 대한 연결을 지원합니다. 독립 실행형 서버를 설치하면 복합적이고 확장 가능한 R 작업을 실행하는 서버 환경을 만들 수 있습니다.  
  
## Microsoft R 서버 (독립 실행형)를 사용할 경우의 이점  
 R은 세계에서 가장 강력한 통계 컴퓨팅, 기계 학습, 그래픽용 프로그래밍 언어이며 사용자, 개발자, 기여자들이 활발히 활동하는 글로벌 커뮤니티에서 지원되고 있습니다. 기존에 엔터프라이즈 환경에서 R을 사용할 경우 특히 데이터 볼륨이 증가하거나 운영 환경에 솔루션을 배포해야 할 때 문제가 있었습니다. Microsoft R Server는 R 코드의 배포 및 운영화 문제를 해결해줍니다.  
  
 Microsoft R 서버 모든 Windows 컴퓨터에 설치할 수와 모든 R 패키지 및 연결 도구 원격 계산 컨텍스트를 사용 하 고 확장 가능 하 고 병렬화 솔루션을 지원 하려면 포함 합니다.  
  
 Microsoft R 서버 (독립 실행형)는 이러한 시나리오를 지원합니다.  
  
-   **중앙 서버를 사용하여 R 솔루션 운영화**  
  
     독립 실행형 서버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 의존하지 않고 향상된 R 성능을 제공합니다. 복잡 하거나 리소스를 많이 사용 하는 계산 리소스 수 제한 하는 랩톱 또는 개발 컴퓨터 대신 서버에서 실행할 수 있습니다.  
  
     작업 또한 중앙화 할 수, 예를 들어 프로덕션 환경에서 예측 모델에 대 한 점수를 매길 하거나 사용 하려는 경우 R에 대 한 단일 연락 지점으로 R 서버 점도 예측 보고에 사용. 
     
     또한 자주 R SQL Server의 컨텍스트 외부에서 실행 해야 하는 경우 SQL Server 컴퓨터에 R 서버 (독립 실행형)을 설치 하는 것이 좋습니다.
  
-   **강력한 데이터 탐색 및 예측 모델링 지원**  
  
     데이터 과학자는 모든 클라이언트 워크스테이션과 R 개발 도구를 사용하여 R 솔루션을 빌드할 수 있습니다. 솔루션에서 RevoScaleR 패키지 API를 사용할 경우, 일반적으로 처리 성능이 훨씬 강력하고 메모리가 훨씬 큰 서버에서 연산을 수행할 수 있습니다. 따라서 훨씬 큰 데이터 집합에서 솔루션 작업이 가능하며, 다중 스레드, 다중 코어 및 다중 프로세스 연산을 활용할 수 있습니다.  
  
## 얻는 방법  
 설치 지침은 [Create a Standalone R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md)을(를) 참조하십시오. 모든 구성 요소를 사용 하 여 설치할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 합니다.  
  
## 추가 R 도구 설치  
 기본 R 개발 환경에 없는 경우 여러 옵션이 있습니다. 자세한 내용은 다음을 참조 하십시오. [설치 또는 R 도구 구성](../../advanced-analytics/r-services/setup-or-configure-r-tools.md)합니다. 
 
 Microsoft R 서버 또는 데이터 과학 워크스테이션에서 SQL Server R 서비스에 연결 하는 것에 대 한 무료 좋습니다 [Microsoft R 클라이언트](http://aka.ms/rclient/download) (다운로드).  
  
## Microsoft R 서버 (독립 실행형)에서 R 스크립트 실행  
 서버 구성 요소를 설정 하 여 즐겨 사용 하는 R IDE를 설치 후 RevoScaleR 패키지를 사용 하 여 솔루션 개발을 시작할 수 있습니다. 이 API를 사용하면 R 명령을 실행하도록 원격 서버에 보낼 수 있습니다.  
  
-   [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started): 높은 성능을 제공 하는 배포 가능한 분석 함수의이 컬렉션을 탐색 하 고 R 솔루션에 맞게 크기 조정 하 여 시작 합니다. 많은 k-평균 클러스터링, 의사 결정 트리 및 의사 결정 포리스트 및 데이터 조작 위한 도구와 같은 패키지를 모델링 하는 가장 인기 있는 R의 병렬화 버전이 포함 됩니다. 또한 사용자 고유의 병렬 알고리즘을 생성 하려면 HPC를 사용할 수 있습니다.  
    
-   [DeployR](https://msdn.microsoft.com/microsoft-r/deployr-about): 선택적이 프레임 워크는 타사 패키지와 함께 출력 R 분석 통합 하려면 Java, JavaScript 또는.Net을 사용 하 여 R 프로그래머를 위한 도구를 제공 합니다.  

다양 한 형식의 SAS, SPSS, Hadoop 및 텍스트 파일 등의 데이터를 작업할 수 있습니다. 현재 위치에서 데이터를 분석할 수도 있고.xdf 파일 형식을 사용 하 여 로컬 R 개발 환경으로 데이터를 효율적으로 이동할 수 있습니다.  
  
R 서버를 시작 하려면 MSDN Library에서이 가이드를 참조 하십시오.: [R Server-시작](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started)  
  
 ScaleR 패키지를 사용 하는 방법에 대 한 자세한 내용은 [25 함수에는 R 자습서](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#an-r-tutorial-in-25-functions-or-so)  
  
## 관련 항목:  
 [SQL Server R Services 시작하기](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  