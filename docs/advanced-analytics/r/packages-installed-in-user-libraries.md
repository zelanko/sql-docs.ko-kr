---
title: 사용자 라이브러리에 설치 된 R 패키지 사용에 대 한 팁
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 07993b982b5c79e3814aa29730fb1849075f5667
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470081"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>SQL Server에서 R 패키지를 사용 하기 위한 팁
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에는 SQL Server 인스턴스의 패키지 액세스에 익숙하지 않은 R 및 숙련 된 R 개발자에 게 익숙하지 않은 Dba를 위한 별도의 섹션이 포함 되어 있습니다.

## <a name="new-to-r"></a>R에 새로 만들기

처음으로 R 패키지를 설치 하는 관리자는 R 패키지 관리에 대 한 몇 가지 기본 사항을 알면 시작 하는 데 도움이 될 수 있습니다.

### <a name="package-dependencies"></a>패키지 종속성

R 패키지는 여러 다른 패키지에 종속 되는 경우가 많으며, 그 중 일부는 인스턴스에 사용 되는 기본 R 라이브러리에서 사용 하지 못할 수도 있습니다. 패키지에 이미 설치 되어 있는 종속 패키지의 다른 버전이 필요한 경우도 있습니다. 패키지 종속성은 패키지에 포함 된 설명 파일에 기록 되지만 때로는 불완전 합니다. [Igraph](https://igraph.org/r/) 라는 패키지를 사용 하 여 종속성 그래프를 완전히 구체화할 수 있습니다.

여러 패키지를 설치 해야 하거나 조직의 모든 사용자가 올바른 패키지 유형 및 버전을 확보 하도록 하려면 [miniCRAN](https://mran.microsoft.com/package/miniCRAN) 패키지를 사용 하 여 완전 한 종속성 체인을 분석 하는 것이 좋습니다. minicRAN 여러 사용자 또는 컴퓨터 간에 공유할 수 있는 로컬 리포지토리를 만듭니다. 자세한 내용은 [miniCRAN를 사용 하 여 로컬 패키지 리포지토리 만들기](create-a-local-package-repository-using-minicran.md)를 참조 하세요.

### <a name="package-sources-versions-and-formats"></a>패키지 소스, 버전 및 형식

[Cran](https://cran.r-project.org/) 및 [Bioconductor](https://www.bioconductor.org/)와 같은 R 패키지에 대 한 여러 소스가 있습니다. R 언어 (<https://www.r-project.org/>)의 공식 사이트에는 이러한 많은 리소스가 나열 됩니다. Microsoft는 [Mran](https://mran.microsoft.com/open) (오픈 소스 R) 및 기타 패키지를배포 하기 위해 [mran](https://mran.microsoft.com/) 을 제공 합니다. 개발자가 소스 코드를 가져올 수 있는 많은 패키지가 GitHub에 게시 됩니다.

R 패키지는 여러 컴퓨팅 플랫폼에서 실행 됩니다. 설치한 버전은 Windows 이진 파일 이어야 합니다.

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>설치 하려는 라이브러리 및 이미 설치 된 패키지를 확인 합니다.

컴퓨터에서 이전에 r 환경을 수정한 경우, 항목을 설치 하기 전에 r 환경 변수가 `.libPath` 하나의 경로만 사용 하는지 확인 합니다.

이 경로는 인스턴스에 대 한 R_SERVICES 폴더를 가리켜야 합니다. 이미 설치 된 패키지를 확인 하는 방법을 비롯 한 자세한 내용은 [SQL Server의 기본 R 및 Python 패키지](../package-management/default-packages.md)를 참조 하십시오.

## <a name="new-to-sql-server"></a>SQL Server의 새로운

SQL Server에서 실행 되는 코드에 대해 작업을 수행 하는 R 개발자는 서버를 보호 하는 보안 정책에 따라 R 환경을 제어할 수 있는 기능이 제한 됩니다.

### <a name="r-user-libraries-not-supported-on-sql-server"></a>R 사용자 라이브러리: SQL Server에서 지원 되지 않음

새 R 패키지를 설치 해야 하는 r 개발자는 기본 라이브러리를 사용할 수 없거나 개발자가 컴퓨터의 관리자가 아닌 경우 언제 든 지 개인, 사용자 라이브러리를 사용 하 여 패키지를 설치 하는 데 익숙할 것입니다. 예를 들어 일반적인 r 개발 환경에서 사용자는 r 환경 변수에 `libPath`패키지의 위치를 추가 하거나 다음과 같이 전체 패키지 경로를 참조 합니다.

```R
library("c:/Users/<username>/R/win-library/packagename")
```

R 패키지를 인스턴스와 연결 된 특정 기본 라이브러리에 설치 해야 하기 때문에 SQL Server에서 R 솔루션을 실행 하는 경우에는이 작업이 수행 되지 않습니다. 패키지를 기본 라이브러리에서 사용할 수 없는 경우에는 패키지를 호출 하려고 할 때이 오류가 발생 합니다.

*라이브러리에 오류가 있습니다. (xxx): ' package-name ' 이라는 패키지가 없습니다.*

### <a name="avoid-package-not-found-errors"></a>"패키지를 찾을 수 없음" 오류 방지

+ 사용자 라이브러리에 대 한 종속성을 제거 합니다. 

    라이브러리 위치에 대 한 액세스 권한이 없는 다른 사용자가 솔루션을 실행 하는 경우 오류가 발생할 수 있으므로 사용자 지정 사용자 라이브러리에 필수 R 패키지를 설치 하는 것은 잘못 된 개발 습관입니다.

    또한 패키지를 기본 라이브러리에 설치 하는 경우 r 코드에서 다른 버전을 지정 하더라도 R 런타임은 패키지를 기본 라이브러리에서 로드 합니다.

+ 공유 환경에서 실행 되도록 코드를 수정 합니다.

+ 패키지를 솔루션의 일부로 설치 하지 마십시오. 패키지를 설치할 수 있는 권한이 없는 경우에는 코드가 실패 합니다. 패키지를 설치할 수 있는 권한이 있는 경우에도 실행 하려는 다른 코드와 별도로이 작업을 수행 해야 합니다.

+ 코드에 설치되지 않은 패키지에 대한 호출이 없는지 확인합니다.

+ R 패키지 또는 R 라이브러리의 경로에 대 한 직접 참조를 제거 하도록 코드를 업데이트 합니다. 

+ 인스턴스와 연결 된 패키지 라이브러리를 확인 합니다. 자세한 내용은 [SQL Server의 기본 R 및 Python 패키지](../package-management/default-packages.md)를 참조 하세요.

## <a name="see-also"></a>참조

+ [새 R 패키지 설치](install-additional-r-packages-on-sql-server.md)
+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [자습서, 샘플, 솔루션](../tutorials/machine-learning-services-tutorials.md)