---
title: 사용자 라이브러리-SQL Server Machine Learning Services에에서 설치 된 R 패키지를 사용 하기 위한 팁
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: ee5dc9dc8b1730f26bada915d739f164a884801d
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510780"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>SQL Server에서 R 패키지를 사용 하기 위한 팁
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에 익숙하지 않으며 R 및 SQL Server 인스턴스에 대 한 알 수 없는 패키지는 숙련 된 R 개발자와 Dba를 위한 별도 섹션이 있습니다.

## <a name="new-to-r"></a>R을 처음 사용

R 설치 관리자 권한으로 R 패키지 관리에 대 한 몇 가지 기본 사항 도움이 알고 있으면 처음으로 패키지 시작 하세요.

### <a name="package-dependencies"></a>패키지 종속성

자주 R 패키지 중 일부는 못할 인스턴스에서 사용 하는 기본 R 라이브러리에 다른 여러 패키지에 따라 달라 집니다. 경우에 따라 패키지를 이미 설치 되어 있는 종속 패키지의 다른 버전을 필요 합니다. 패키지 종속성 패키지에 포함 된 설명 파일에 명시 되어 있지만 때로는 완전 하지 않습니다. 라는 패키지를 사용할 수 있습니다 [iGraph](https://igraph.org/r/) 완전히 종속성 그래프를 구체화할 수 있습니다.

여러 패키지를 설치 하거나 올바른 패키지 유형 및 버전을 조직의 모든 사용자가 확인 해야 할 경우 사용 하는 것이 좋습니다 합니다 [miniCRAN](https://mran.microsoft.com/package/miniCRAN) 전체 종속성 체인을 분석 하는 패키지입니다. minicRAN 여러 사용자 또는 컴퓨터 사이에서 공유할 수 있는 로컬 리포지토리를 만듭니다. 자세한 내용은 [miniCRAN을 사용 하 여 로컬 패키지 리포지토리 만들기](create-a-local-package-repository-using-minicran.md)합니다.

### <a name="package-sources-versions-and-formats"></a>패키지 원본, 버전 및 형식

와 같은 여러 소스 R 패키지에 대 한 가지 [CRAN](https://cran.r-project.org/) 하 고 [Bioconductor](https://www.bioconductor.org/)합니다. R 언어 공식 사이트 (<https://www.r-project.org/>) 많은이 리소스를 나열 합니다. Microsoft 제공 [MRAN](https://mran.microsoft.com/) 오픈 소스 R의 해당 배포에 대 한 ([MRO](https://mran.microsoft.com/open)) 및 기타 패키지 있습니다. 많은 패키지 개발자가 소스 코드를 얻을 수 있는 GitHub에 게시 됩니다.

R 패키지는 여러 컴퓨팅 플랫폼에서 실행합니다. 설치한 버전 Windows 이진 파일에는 확인 해야 합니다.

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>설치 중인 및 이미 설치 된 패키지는 라이브러리를 알고 있습니다.

모든 항목을 설치 하기 전에 컴퓨터의 R 환경을 수정한 이전에, 경우 확인 하는 R 환경 변수 `.libPath` 하나의 경로 사용 합니다.

이 경로 인스턴스에 대 한 R_SERVICES 폴더를 가리켜야 합니다. 이미 설치 된 패키지를 확인 하는 방법을 비롯 한 자세한 내용은 참조 하세요. [SQL Server의 기본 R 및 Python 패키지](installing-and-managing-r-packages.md)합니다.

## <a name="new-to-sql-server"></a>새 SQL server

SQL Server에서 실행 되는 코드에서 작업 하는 R 개발자로 서 서버를 보호 하 여 보안 정책을 R 환경을 제어 하는 능력을 제한 합니다.

### <a name="r-user-libraries-not-supported-on-sql-server"></a>R 사용자 라이브러리: SQL Server에서 지원 되지 않습니다

새 R 패키지를 설치 하는 R 개발자 익숙한 부과 패키지를 설치 하려면 기본 라이브러리를 사용할 수 없을 때마다 또는 개발자 컴퓨터의 관리자가 아닌 경우 개인, 사용자 라이브러리를 사용 하 여 합니다. 예를 들어, 일반적인 R 개발 환경에서 사용자는 패키지의 위치에 추가 R 환경 변수 `libPath`, 또는 이와 같은 전체 패키지 경로 참조 합니다.

```R
library("c:/Users/<username>/R/win-library/packagename")
```

작동 하지 않으면 SQL Server에서 R 솔루션을 실행 하는 경우 인스턴스와 연결 된 특정 기본 라이브러리에 R 패키지를 설치할 수 있어야 합니다. 기본 라이브러리에 패키지를 사용할 수 없는 경우 패키지를 호출 하려고 할 때이 오류가 발생 하면:

*라이브러리에 대 한 오류: ' 패키지 이름 ' 라는 패키지가 없음*

### <a name="avoid-package-not-found-errors"></a>"패키지를 찾을 수 없음" 오류를 방지

+ 사용자 라이브러리에 대 한 종속성을 제거 합니다. 

    것이 사용자 라이브러리에 필요한 R 패키지를 설치 하는 잘못 된 개발 사례 솔루션 라이브러리 위치에 대 한 액세스를 갖고 있지 않은 다른 사용자로 실행 되 면 오류가 발생할 수 있습니다.

    또한 패키지를 기본 라이브러리에 설치 되어 있으면 R 런타임 패키지를 로드 기본 라이브러리에서 R 코드에서 다른 버전을 지정 하는 경우에 합니다.

+ 공유 환경에서 실행 하도록 코드를 수정 합니다.

+ 솔루션의 일부로 패키지를 설치 하지 마세요. 패키지를 설치할 수 있는 권한이 없으면 코드는 실패 합니다. 수행할 권한이 있는 패키지를 설치 하는 경우에 해야 하므로 별도로 실행 하려는 다른 코드에서.

+ 코드에 설치되지 않은 패키지에 대한 호출이 없는지 확인합니다.

+ R 패키지 또는 R 라이브러리에 대 한 경로에 대 한 직접 참조를 제거 하도록 코드를 업데이트 합니다. 

+ 패키지 라이브러리는 인스턴스와 관련 된 것입니다. 자세한 내용은 [SQL Server의 기본 R 및 Python 패키지](installing-and-managing-r-packages.md)합니다.

## <a name="see-also"></a>참고자료

+ [새 R 패키지 설치](install-additional-r-packages-on-sql-server.md)
+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [자습서, 샘플, 솔루션](../tutorials/machine-learning-services-tutorials.md)