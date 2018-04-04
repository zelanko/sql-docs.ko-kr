---
title: 사용자 라이브러리에 설치 된 R 패키지에서 오류를 방지 | Microsoft Docs
titleSuffix: SQL Server
ms.custom: ''
ms.date: 02/20/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: a3498ca0940384dacf9f67ac916d78eee939f829
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="avoiding-errors-on-r-packages-installed-in-user-libraries"></a>사용자 라이브러리에 설치 된 R 패키지에서 오류를 방지 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

숙련 된 R 사용자가 차단 되거나 사용할 수 없는 기본 라이브러리는 때마다 사용자 라이브러리에서 R 패키지를 설치 하는 데 익숙한 합니다. 그러나이 방법은 SQL Server에서 지원 되지 않습니다 및 "패키지를 찾을 수 없음" 오류 일반적으로 끝나는 사용자 라이브러리를 설치 합니다.

이 문서에서는이 오류를 방지할 수 있도록 해결 방법을 설명 합니다. R 코드를 수정 하는 방법에 대해 설명 하 고 SQL Server 인스턴스에서 R 패키지를 사용 하기 위한 올바른 R 패키지 설치 프로세스를 제안 합니다.

## <a name="why-r-user-libraries-cannot-be-accessed-from-sql-server"></a>SQL Server에서 R 사용자 라이브러리 액세스할 수 없는 이유

새 R 패키지를 설치 해야 하는 R 개발자에 익숙한가 패키지를 설치 하는 기본 라이브러리를 사용할 수 없을 때마다 또는 개발자 컴퓨터에서 관리자가 아닌 경우 개인, 사용자 라이브러리를 사용 하 여 합니다.

예를 들어 일반적인 R 개발 환경에서 사용자가 패키지의 위치에 추가 R 환경 변수 `libPath`, 또는 다음과 같이 전체 패키지 경로 참조 합니다.

```R
library("c:/Users/<username>/R/win-library/packagename")
```

작동 하지 않으면 SQL Server에서 R 솔루션을 실행 하는 경우 R 패키지는 인스턴스와 연결 된 특정 기본 라이브러리를 설치 해야 하기 때문에 있습니다. 패키지를 사용할 수 없는 기본 라이브러리에서 패키지를 호출 하려고 할 때이 오류가 발생:

*Library(xxx)의 오류: ' 패키지 name ' 없는 패키지는*

## <a name="how-to-avoid-package-not-found-errors"></a>"패키지를 찾을 수 없음" 오류를 방지 하는 방법

+ 사용자 라이브러리에 대 한 종속성을 제거 합니다. 

    좋습니다 잘못 된 개발 사용자 지정 사용자 라이브러리에 필요한 R 패키지를 설치 하는 솔루션 라이브러리 위치에 대 한 액세스 권한이 없는 다른 사용자로 실행 되 면 오류가 발생할 수 있습니다.

    또한 패키지는 기본 라이브러리에서 설치 된 경우 R 런타임 패키지를 로드는 기본 라이브러리에서 R 코드에서 다른 버전을 지정 하는 경우에 합니다.

+ 공유 환경에서 실행 하도록 코드를 수정 합니다.

+ 솔루션의 일부분으로 패키지를 설치 하지 않습니다. 패키지를 설치할 수 있는 권한이 없는 경우에 코드는 실패 합니다. 사용자에 게 패키지를 설치 하는 권한이, 경우에 실행 하려는 다른 코드에서 있으므로 별도로 수행 해야 합니다.

+ 코드에 설치되지 않은 패키지에 대한 호출이 없는지 확인합니다.

+ R 패키지 또는 R 라이브러리에 대 한 경로에 대 한 직접 참조 하도록 코드를 업데이트 합니다. 

+ 상위 패키지 라이브러리는 인스턴스와 연결 된 알아야 합니다. 자세한 내용은 참조 [SQL Server와 함께 설치 된 R 패키지](installing-and-managing-r-packages.md)
