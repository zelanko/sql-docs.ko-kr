---
title: R 패키지 사용 팁
titleSuffix: SQL machine learning
description: R 또는 SQL Server를 처음 접하는 사용자를 위해 제공되는 SQL Server에서 R 패키지를 사용하는 방법에 대한 유용한 팁을 알아보세요.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/06/2019
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: c43c5e252c016d8d2094dc2b26d6e87fe3f05749
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869963"
---
# <a name="tips-for-using-r-packages"></a>R 패키지 사용 팁

[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

이 문서에서는 SQL Server에서 R 패키지를 사용하는 방법에 대한 유용한 팁을 제공합니다. 이러한 팁은 R에 익숙하지 않은 DBA와 SQL Server 인스턴스의 패키지 액세스에 익숙하지 않은 숙련된 R 개발자를 위한 것입니다.

## <a name="if-youre-new-to-r"></a>R을 처음 접하는 경우

처음으로 R 패키지를 설치하는 관리자는 R 패키지 관리에 대한 몇 가지 기본 사항을 알면 시작하는 데 도움이 될 수 있습니다.

### <a name="package-dependencies"></a>패키지 종속성

R 패키지는 여러 다른 패키지에 종속되는 경우가 많으며, 그중 일부를 인스턴스에 사용되는 기본 R 라이브러리에서 사용하지 못할 수도 있습니다. 패키지에 이미 설치된 것과 다른 버전의 종속성 패키지가 필요한 경우도 있습니다. 패키지 종속성은 패키지에 포함된 설명 파일에 명시되어 있지만 때로는 불완전합니다. [iGraph](https://igraph.org/r/)라는 패키지를 사용하여 종속성 그래프를 완전히 구체화할 수 있습니다.

여러 패키지를 설치해야 하거나 조직의 모든 사용자가 올바른 패키지 유형 및 버전을 확보하도록 하려면 [miniCRAN](https://mran.microsoft.com/package/miniCRAN) 패키지를 사용하여 완전한 종속성 체인을 분석하는 것이 좋습니다. minicRAN은 여러 사용자 또는 컴퓨터 간에 공유할 수 있는 로컬 리포지토리를 만듭니다. 자세한 내용은 [miniCRAN을 사용하여 로컬 패키지 리포지토리 만들기](create-a-local-package-repository-using-minicran.md)를 참조하세요.

### <a name="package-sources-versions-and-formats"></a>패키지 원본, 버전 및 형식

R 패키지에 대해 [CRAN](https://cran.r-project.org/) 및 [Bioconductor](https://www.bioconductor.org/)와 같은 여러 출처가 있습니다. R 언어 공식 사이트(<https://www.r-project.org/>)에 다양한 리소스가 나와 있습니다. Microsoft는 오픈 소스 R([MRAN](https://mran.microsoft.com/)) 및 기타 패키지의 배포판에 대해 [MRAN](https://mran.microsoft.com/open)을 제공합니다. 많은 패키지는 개발자가 소스 코드를 볼 수 있는 GitHub에도 게시됩니다.

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
R 패키지는 여러 컴퓨팅 플랫폼에서 실행됩니다. 설치한 버전은 Windows 이진 파일이어야 합니다.
::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
R 패키지는 여러 컴퓨팅 플랫폼에서 실행됩니다. 설치한 버전은 Linux 이진 파일이어야 합니다.
::: moniker-end

### <a name="know-which-library-youre-installing-to-and-which-packages-are-already-installed"></a>설치하려는 라이브러리 및 이미 설치한 패키지를 확인합니다.

이전에 컴퓨터의 R 환경을 수정한 경우 설치를 진행하기 전에 R 환경 변수 `.libPath`에서 경로를 하나만 사용하는지 확인합니다.

이 경로는 인스턴스에 대한 R_SERVICES 폴더를 가리켜야 합니다. 이미 설치된 패키지를 확인하는 방법을 비롯한 자세한 내용은 [R 패키지 정보 가져오기](../package-management/r-package-information.md)를 참조하세요.

## <a name="if-youre-new-to-sql-server"></a>SQL Server를 처음 접하는 경우

SQL Server에서 실행되는 코드 작업을 수행하는 R 개발자는 서버를 보호하는 보안 정책 때문에 R 환경을 제어하는 기능이 제한됩니다. 다음 팁에서는 일반적인 상황을 설명하고 이 환경에서 작업할 때 유용한 지침을 제안합니다.

### <a name="r-user-libraries-not-supported-on-sql-server"></a>R 사용자 라이브러리: SQL Server에서 지원되지 않음

새 R 패키지를 설치해야 하는 R 개발자는 기본 라이브러리를 사용할 수 없거나 개발자가 컴퓨터의 관리자가 아닌 경우, 프라이빗, 사용자 라이브러리를 사용하여 패키지를 설치하는 데 익숙할 것입니다. 예를 들어, 일반적인 R 개발 환경의 경우 사용자는 R 환경 변수 `libPath`에 패키지의 위치를 추가하거나 다음과 같이 전체 패키지 경로를 참조합니다.

```R
library("c:/Users/<username>/R/win-library/packagename")
```

R 패키지를 인스턴스와 연결된 특정 기본 라이브러리에 설치해야 하기 때문에 SQL Server에서 R 솔루션을 실행하는 경우에는 이 작업이 수행되지 않습니다. 패키지가 기본 라이브러리에 설치되지 않으면 패키지를 호출하려고 할 때 다음 오류가 발생합니다.

*라이브러리의 오류(xxx): 'package-name'(이)라는 패키지가 없음*

SQL Server에서 R 패키지를 설치하는 방법에 대한 내용은 [SQL Server Machine Learning Services 또는 SQL Server R Services에서 새 R 패키지 설치](install-additional-r-packages-on-sql-server.md)를 참조하세요.

### <a name="how-to-avoid-package-not-found-errors"></a>"패키지를 찾을 수 없음" 오류를 방지하는 방법

다음 지침을 사용하여 "패키지를 찾을 수 없음" 오류를 방지할 수 있습니다.

+ 사용자 라이브러리에 대한 종속성을 제거합니다.

    필수 R 패키지를 사용자 지정 사용자 라이브러리에 설치하는 것은 잘못된 개발 방식입니다. 라이브러리 위치에 대한 액세스 권한이 없는 다른 사용자가 솔루션을 실행하는 경우 이로 인해 오류가 발생할 수 있습니다.

    또한 패키지가 기본 라이브러리에 설치되면 R 코드에 다른 라이브러리를 지정하더라도 R 런타임이 기본 라이브러리에서 패키지를 로드합니다.

+ 공유 환경에서 코드를 실행할 수 있는지 확인합니다.

+ 패키지를 솔루션의 일부로 설치하지 않도록 합니다. 패키지를 설치할 수 있는 권한이 없는 경우에는 코드가 실패합니다. 패키지를 설치할 수 있는 권한이 있는 경우에도 실행하려는 다른 코드와는 별도로이 작업을 수행해야 합니다.

+ 코드에 설치되지 않은 패키지에 대한 호출이 없는지 확인합니다.

+ R 패키지 또는 R 라이브러리의 경로에 대한 직접 참조를 제거하도록 코드를 업데이트합니다.

+ 인스턴스와 연결된 패키지 라이브러리를 확인합니다. 자세한 내용은 [R 패키지 정보 가져오기](../package-management/r-package-information.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

::: moniker range="<=sql-server-2017||=sqlallproducts-allversions"
+ [R 도구를 사용하여 패키지 설치](install-r-packages-standard-tools.md)
::: moniker-end
::: moniker range=">sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"
+ [sqlmlutils를 사용하여 새 R 패키지 설치](install-additional-r-packages-on-sql-server.md)
::: moniker-end
