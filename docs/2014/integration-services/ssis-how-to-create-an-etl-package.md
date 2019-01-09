---
title: 'SSIS 자습서: 간단한 ETL 패키지 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS, tutorials
- packages [Integration Services], tutorials
- Integration Services, tutorials
- SQL Server Integration Services, tutorials
- logs [Integration Services], tutorials
- walkthroughs [Integration Services]
ms.assetid: d6d5bb1f-4cb1-4605-9cd6-f60b858382c4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2a99169168eb21f0a7d42f133e7e882141c776e6
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53357908"
---
# <a name="ssis-tutorial-creating-a-simple-etl-package"></a>SSIS 자습서: 간단한 ETL 패키지 만들기
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS)는 고성능 데이터 통합 솔루션을 추출, 변환 및 데이터 웨어하우징을 위한 ETL (로드) 패키지를 포함 하 여 빌드하기 위한 플랫폼입니다. SSIS에는 패키지를 빌드하고 디버깅하기 위한 그래픽 도구 및 마법사, FTP 작업과 같은 워크플로 함수를 수행하고 SQL 문을 실행하며 전자 메일 메시지를 보내기 위한 태스크, 데이터 추출 및 로드를 위한 데이터 원본과 대상, 데이터 삭제, 집계, 병합 및 복사를 위한 변환, 패키지 실행 및 저장을 관리하기 위한 관리 서비스인 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개체 모델 프로그래밍을 위한 API(애플리케이션 프로그래밍 인터페이스)가 포함됩니다.  
  
 이 자습서에서는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너를 사용하여 간단한 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 만드는 방법을 배웁니다. 사용자가 만든 패키지는 플랫 파일로부터 데이터를 가져와서 데이터 형식을 바꾼 다음 바뀐 데이터를 팩트 테이블에 삽입합니다. 다음 단원에서는 패키지를 확장하여 루핑, 패키지 구성, 로깅 및 오류 흐름을 보여 줍니다.  
  
 자습서에서 사용하는 예제 데이터를 설치하면 자습서의 각 단원에서 만들 패키지의 완성된 버전도 함께 설치됩니다. 원하는 경우 단원을 건너뛰고 완성된 패키지를 사용하여 이후 단원에서 자습서를 시작할 수 있습니다. 패키지 또는 새 개발 환경 작업을 처음으로 수행하는 경우에는 1단원부터 시작하는 것이 좋습니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 사용할 수 있는 새 도구, 컨트롤 및 기능에 익숙해지는 가장 좋은 방법은 실제로 사용해 보는 것입니다. 이 자습서에서는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너를 사용하여 루핑, 구성, 오류 흐름 논리 및 로깅을 포함하는 간단한 ETL 패키지를 만드는 과정을 안내합니다.  
  
## <a name="requirements"></a>요구 사항  
 이 자습서는 기본적인 데이터베이스 작업에는 익숙하지만 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]의 새 기능은 많이 접해 보지 못한 사용자를 위한 것입니다.  
  
 이 자습서를 사용하려면 시스템에 다음 구성 요소가 설치되어 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] AdventureWorksDW2012 **데이터베이스가 있는** . 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다. **AdventureWorksDW2012** 데이터베이스를 다운로드하려면 [SQL Server 2012용 Adventure Works](https://go.microsoft.com/fwlink/?LinkId=275026)를 참조하십시오.  
  
    > [!IMPORTANT]  
    >  데이터베이스(\*.mdf 파일)에 연결할 때 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서 기본적으로 .ldf 파일을 검색합니다. **데이터베이스 연결** 대화 상자에서 확인을 클릭하기 전에 .ldf 파일을 수동으로 제거해야 합니다.  
    >   
    >  데이터베이스 연결에 대한 자세한 내용은 [Attach a Database](../relational-databases/databases/attach-a-database.md)을 참조하십시오.  
  
-   데이터 샘플링 예제 데이터는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 단원 패키지에 포함되어 있습니다. 예제 데이터 및 단원 패키지를 다운로드하려면 다음을 수행합니다.  
  
    1.   [Integration Services 제품 예제](https://go.microsoft.com/fwlink/?LinkId=275027)로 이동합니다.  
  
    2.  **DOWNLOADS** 탭을 클릭합니다.  
  
    3.  SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 파일을 클릭합니다.  
  
## <a name="lessons-in-this-tutorial"></a>이 자습서의 단원  
 [1 단원: 프로젝트 및 기본 패키지 만들기](lesson-1-create-a-project-and-basic-package-with-ssis.md)  
 이 단원에서는 단일 플랫 파일에서 데이터를 추출하고, 조회 변환을 사용하여 데이터를 변환하고, 마지막으로 결과를 팩트 테이블 대상에 로드하는 간단한 ETL 패키지를 만듭니다.  
  
 [2단원: 루핑 추가](lesson-2-adding-looping-with-ssis.md)  
 이 단원에서는 1단원에서 만든 패키지를 확장하여 새 루핑 기능을 활용함으로써 여러 플랫 파일을 단일 데이터 흐름 프로세스로 추출합니다.  
  
 [3 단원: 로깅 추가](lesson-3-add-logging-with-ssis.md)  
 이 단원에서는 2단원에서 만든 패키지를 확장하여 새 로깅 기능을 활용합니다.  
  
 [4 단원: 오류 흐름 리디렉션 추가](lesson-4-add-error-flow-redirection-with-ssis.md)  
 이 단원에서는 3단원에서 만든 패키지를 확장하여 새 오류 출력 구성을 활용합니다.  
  
 [5 단원: 패키지 배포 모델을 위한 패키지 구성 추가](lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
 이 단원에서는 4단원에서 만든 패키지를 확장하여 새 패키지 구성 옵션을 활용합니다.  
  
 [6 단원: 매개 변수를 사용 하 여 프로젝트 배포 모델을 사용 하 여](lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
 이 단원에서는 5단원에서 만든 패키지를 확장하여 프로젝트 배포 모델에서 새 매개 변수 사용을 활용할 수 있습니다.  
  
  
