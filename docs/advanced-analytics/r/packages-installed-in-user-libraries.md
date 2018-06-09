---
title: SQL Server의 사용자 라이브러리에 설치 된 R 패키지를 사용 하기 위한 팁 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e52a6f4a9a3830aab01e54819804785a7069c9d2
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34708471"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>SQL Server에서 R 패키지를 사용 하기 위한 팁
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 R 및 SQL Server 인스턴스의 생소 한 패키지 액세스는 숙련 된 R 개발자에 게 Dba에 대 한 별도 섹션에 있습니다.

## <a name="new-to-r"></a>R를 처음 사용

R 설치 관리자 권한으로 R 패키지 관리에 대 한 몇 가지 기본 사항 수를 알고 있으면 처음으로 패키지를 시작 하세요.

### <a name="package-dependencies"></a>패키지 종속 파일

R 패키지는 자주 중 일부는 사용 하지 못할 인스턴스에서 사용 하는 기본 R 라이브러리에서 다른 여러 패키지에 따라 다릅니다. 경우에 따라 패키지에 이미 설치 되어 있는 종속 패키지의 다른 버전이 필요 합니다. 패키지 종속 파일 패키지에 포함 된 설명 파일에서 확인할 수 있지만 때로는 완전 하지 않습니다. 호출 하는 패키지를 사용할 수 있습니다 [iGraph](http://igraph.org/r/) 완전히 종속성 그래프를 구체화할 수 있습니다.

올바른 패키지 유형 및 버전을 갖게 조직의 모든 사용자를 또는 여러 패키지를 설치 해야 할 경우 사용 하는 것이 좋습니다는 [miniCRAN](https://mran.microsoft.com/package/miniCRAN) 전체 종속성 체인을 분석 하는 패키지입니다. minicRAN 여러 사용자 또는 컴퓨터 간에 공유할 수 있는 한 로컬 저장소를 만듭니다. 자세한 내용은 참조 [miniCRAN를 사용 하 여 로컬 패키지 리포지토리를 만들](create-a-local-package-repository-using-minicran.md)합니다.

### <a name="package-sources-versions-and-formats"></a>패키지 소스, 버전 및 형식

여러 R 패키지 소스와 같은 [CRAN](https://cran.r-project.org/) 및 [Bioconductor](https://www.bioconductor.org/)합니다. R 언어에 대 한 공식 사이트 (<https://www.r-project.org/>) 많은이 리소스를 나열 합니다. Microsoft는 [MRAN](https://mran.microsoft.com/) 오픈 소스 R의 해당 배포에 대 한 ([MRO](https://mran.microsoft.com/open)) 및 기타 패키지 합니다. 많은 패키지 개발자가 소스 코드를 가져올 수 있는 GitHub에 게시 됩니다.

R 패키지는 여러 컴퓨팅 플랫폼에서 실행 합니다. 설치한 버전 Windows 이진 지 수 있습니다.

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>설치 하 고 어떤 패키지가 이미 설치 되어 있는 라이브러리를 알고 있습니다.

모든 항목을 설치 하기 전에 이전에 컴퓨터의 R 환경을 수정 하는 경우 확인 R 환경 변수 `.libPath` 하나의 경로 사용 합니다.

이 경로 인스턴스에 대 한 R_SERVICES 폴더를 가리켜야 합니다. 이미 설치 되어 있는 패키지를 확인 하는 방법을 비롯 한 자세한 내용은 참조 하십시오. [SQL Server에 기본 R 및 Python 패키지](installing-and-managing-r-packages.md)합니다.

## <a name="new-to-sql-server"></a>SQL Server를 처음 사용

R 개발자, SQL Server에서 실행 되는 코드에서 작업 하는 서버를 보호 하는 보안 정책은 R 환경을 제어 하는 기능을 제한 합니다.

### <a name="r-user-libraries-not-supported-on-sql-server"></a>R 사용자 라이브러리: SQL Server에서 지원 되지 않습니다

새 R 패키지를 설치 해야 하는 R 개발자에 익숙한가 패키지를 설치 하는 기본 라이브러리를 사용할 수 없을 때마다 또는 개발자 컴퓨터에서 관리자가 아닌 경우 개인, 사용자 라이브러리를 사용 하 여 합니다. 예를 들어 일반적인 R 개발 환경에서 사용자가 패키지의 위치에 추가 R 환경 변수 `libPath`, 또는 다음과 같이 전체 패키지 경로 참조 합니다.

```R
library("c:/Users/<username>/R/win-library/packagename")
```

작동 하지 않으면 SQL Server에서 R 솔루션을 실행 하는 경우 R 패키지는 인스턴스와 연결 된 특정 기본 라이브러리를 설치 해야 하기 때문에 있습니다. 패키지를 사용할 수 없는 기본 라이브러리에서 패키지를 호출 하려고 할 때이 오류가 발생:

*Library(xxx)의 오류: ' 패키지 name ' 없는 패키지는*

### <a name="avoid-package-not-found-errors"></a>"패키지를 찾을 수 없음" 오류 방지

+ 사용자 라이브러리에 대 한 종속성을 제거 합니다. 

    좋습니다 잘못 된 개발 사용자 지정 사용자 라이브러리에 필요한 R 패키지를 설치 하는 솔루션 라이브러리 위치에 대 한 액세스 권한이 없는 다른 사용자로 실행 되 면 오류가 발생할 수 있습니다.

    또한 패키지는 기본 라이브러리에서 설치 된 경우 R 런타임 패키지를 로드는 기본 라이브러리에서 R 코드에서 다른 버전을 지정 하는 경우에 합니다.

+ 공유 환경에서 실행 하도록 코드를 수정 합니다.

+ 솔루션의 일부분으로 패키지를 설치 하지 않습니다. 패키지를 설치할 수 있는 권한이 없는 경우에 코드는 실패 합니다. 사용자에 게 패키지를 설치 하는 권한이, 경우에 실행 하려는 다른 코드에서 있으므로 별도로 수행 해야 합니다.

+ 코드에 설치되지 않은 패키지에 대한 호출이 없는지 확인합니다.

+ R 패키지 또는 R 라이브러리에 대 한 경로에 대 한 직접 참조 하도록 코드를 업데이트 합니다. 

+ 상위 패키지 라이브러리는 인스턴스와 연결 된 알아야 합니다. 자세한 내용은 참조 [SQL Server에 기본 R 및 Python 패키지](installing-and-managing-r-packages.md)합니다.

## <a name="see-also"></a>참고자료

+ [새 R 패키지 설치](install-additional-r-packages-on-sql-server.md)
+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [자습서, 샘플, 솔루션](../tutorials/machine-learning-services-tutorials.md)