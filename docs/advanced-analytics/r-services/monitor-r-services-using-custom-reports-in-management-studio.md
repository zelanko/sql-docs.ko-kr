---
title: "Management Studio의 사용자 지정 보고서를 사용하여 R Services 모니터링 | Microsoft Docs"
ms.custom: ""
ms.date: "02/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5933c72c-ba63-4966-b882-75719ef8428e
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 9
---
# Management Studio의 사용자 지정 보고서를 사용하여 R Services 모니터링
SQL Server R Services를 손쉽게 관리할 수 있도록 제품 팀에서 SQL Server Management Studio에 추가할 수 있는 사용자 지정 보고서 샘플을 여러 개 제공하고 있습니다. 이 보고서를 사용하여 다음과 같은 R Service 세부 정보를 볼 수 있습니다.

- 활성 R 세션의 목록
- 현재 인스턴스의 R 구성
- R 런타임에 대한 실행 통계
- R Services에 대한 확장된 이벤트 목록
- 현재 인스턴스에 설치된 R 패키지의 목록

이 항목에서는 보고서를 설치하고 사용하는 방법을 설명합니다. Management Studio의 사용자 지정 보고서에 대한 자세한 내용은 [Management Studio의 사용자 지정 보고서](../../ssms/object/custom-reports-in-management-studio.md)를 참조하세요.

## <a name="how-to-install-the-reports"></a>보고서를 설치하는 방법

보고서는 SQL Server Reporting Services를 사용하여 만듭니다. 하지만 Reporting Services가 인스턴스에서 설치되어 있지 않더라도 SQL Server Management Studio에서 바로 보고서를 사용할 수도 있습니다. 

이러한 보고서를 사용하려면:

* SQL Server 제품 샘플용 GitHub 리포지토리에서 RDL 파일을 다운로드합니다.
* SQL Server Management Studio에 사용되는 사용자 지정 보고서 폴더에 파일을 추가합니다.
* SQL Server Management Studio에서 보고서를 엽니다.


### <a name="step-1-download-the-reports"></a>1단계. 보고서 다운로드

1. 샘플 데이터베이스를 비롯한 모든 SQL Server 제품 샘플이 들어 있는 GitHub 리포지토리를 엽니다. 
   + [Microsoft/sql-server-samples](https://github.com/Microsoft/sql-server-samples)
   + [SSMS 사용자 지정 보고서](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/SSMS-Custom-Reports)
      
2. 샘플을 다운로드하려면 GitHub에 로그인하고 샘플의 로컬 분기를 만들면 됩니다. 

### <a name="step-2-copy-the-reports-to-management-studio"></a>2단계. Management Studio에 보고서 복사

3. SQL Server Management Studio에 사용되는 사용자 지정 보고서 폴더를 찾습니다. 기본적으로 사용자 지정 보고서는 이 폴더에 저장됩니다.
    
   `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

   그러나 다른 폴더를 지정하거나 하위 폴더를 만들 수 있습니다.

4. *.RDL 파일을 사용자 지정 보고서 폴더에 복사합니다.


### <a name="step-3-run-the-reports"></a>3단계. 보고서 실행

5. 보고서를 실행할 인스턴스의 **데이터베이스** 노드를 Management Studio에서 마우스 오른쪽 단추로 클릭합니다.
6. **보고서**를 클릭하고 **사용자 지정 보고서**를 클릭합니다. 
7. **파일 열기** 대화 상자에서 사용자 지정 보고서 폴더를 찾습니다.
8. 다운로드한 RDL 파일 중 하나를 선택한 다음 **열기**를 클릭합니다.

> [!IMPORTANT] 일부 컴퓨터에서는 이러한 보고서를 사용할 수 없습니다. 예를 들면 DPI가 높거나 해상도가 1080p보다 큰 디스플레이 장치가 있는 컴퓨터입니다. SSMS의 보고서 뷰어 컨트롤에는 보고서와 충돌하는 버그가 있습니다.  


## <a name="report-list"></a>보고서 목록

현재 GitHub의 제품 샘플 리포지토리에는 SQL Server R Services에 대한 다음과 같은 보고서가 있습니다.

+ **R Services - 활성 세션**

  이 보고서를 사용하면 SQL 인스턴스에 현재 연결되어 R 작업을 실행 중인 사용자를 볼 수 있습니다. 
  
+ **R Services - 구성**

  이 보고서를 사용하면 R 런타임의 속성과 R Services의 구성을 볼 수 있습니다. 보고서는 다시 시작이 필요한지 표시하고 필요한 네트워크 프로토콜을 확인합니다. 
  
  SQL 계산 컨텍스트에서 R을 실행하려면 묵시적 인증이 필요합니다. 보고서는 묵시적 인증이 가능한지 확인하기 위해 데이터베이스가 그룹 SQLRUserGroup에 로그인할 수 있는지 확인합니다.

  > [!NOTE] 이러한 필드에 대한 자세한 내용은 Hadley Wickam의 [패키지 메타데이터](http://r-pkgs.had.co.nz/description.html)를 참조하세요. 예를 들어 릴리스를 쉽게 구별할 수 있도록 R 런타임에 *애칭* 필드를 도입했습니다. 

 + **R Services - 인스턴스 구성** 

   이 보고서는 설치 후 R Services를 쉽게 구성할 수 있도록 만든 것입니다. R Services를 올바르게 구성하지 않은 경우 이전 보고서에서 실행할 수 있습니다.
 
+ **R Services - 실행 통계**

  이 보고서를 사용하면 R Services의 실행 통계를 볼 수 있습니다. 예를 들어 실행한 R 스크립트의 총 개수, 병렬 실행 개수, 가장 자주 사용한 RevoScaleR 함수 정보를 알 수 있습니다.
  이 보고서는 현재 RevoScaleR 패키지 함수의 통계만 모니터링합니다.
  **View SQL Script**(SQL 스크립트 보기)를 클릭하여 이 보고서의 T-SQL 코드를 가져올 수 있습니다. 

+ **R Services - 확장 이벤트**

  이 보고서를 사용하여 R 스크립트 실행을 모니터링하는 데 사용할 수 있는 확장된 이벤트 목록을 볼 수 있습니다. 
  **View SQL Script**(SQL 스크립트 보기)를 클릭하여 이 보고서의 T-SQL 코드를 가져올 수 있습니다.

+ **R Services - 패키지**

  이 보고서를 사용하여 SQL Server 인스턴스에 설치된 R 패키지 목록을 볼 수 있습니다. 현재 이 보고서에는 다음 패키지 속성이 들어 있습니다. 
  + 패키지 이름
  + 버전 
  + 개체
  + 라이선스
  + 기본 제공
  + Lib 경로

+ **R Services - 리소스 사용량**

  이 보고서를 사용하여 SQL Server R 스크립트 실행으로 인한 CPU, 메모리 및 I/O 리소스 사용량을 확인할 수 있습니다. 또한 외부 리소스 풀의 메모리 설정도 볼 수 있습니다. 


## <a name="see-also"></a>참고 항목

[R Services 모니터링](../../advanced-analytics/r-services/monitoring-r-services.md)

[R Services에 대한 확장된 이벤트](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)