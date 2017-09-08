---
title: "사용자 라이브러리에 설치된 패키지 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ffd9b8-aa6d-4ac2-9840-4e66d0463978
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b4d5c7f3d1d0da5e1967140fcbdfcf60ba4571e7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="packages-installed-in-user-libraries"></a>사용자 라이브러리에 설치된 패키지

사용자에게 새 R 패키지가 필요하고 사용자가 관리자가 아니면 패키지는 기본 위치에 설치될 수 없고 기본적으로 전용 사용자 라이브러리에 설치됩니다. 

일반적인 R 개발 환경의 경우 코드에서 패키지를 참조하려면 사용자는 R 환경 변수 `libPath`에 위치를 추가하거나 다음과 같이 전체 패키지 경로를 참조해야 합니다.  
  
~~~~
library("c:/Users/<username>/R/win-library/packagename")  
~~~~

## <a name="problems-with-packages-in-user-libraries"></a>사용자 라이브러리의 패키지 관련 문제

하지만 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서 이 해결 방법은 지원되지 **않습니다**. 패키지는 기본 라이브러리에 설치되어야 합니다. 패키지가 기본 라이브러리에 설치되지 않으면 패키지를 호출하려고 할 때 이 오류가 발생할 수 있습니다.

*라이브러리의 오류(xxx): 'xxx'라는 패키지가 없음*
 

따라서 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 실행할 R 솔루션을 마이그레이션할 경우 다음을 수행해야 합니다.
+ 기본 라이브러리에 필요한 패키지를 설치합니다.
+ 코드를 편집하여 임시 디렉터리나 사용자 라이브러리가 아닌 기본 라이브러리에서 패키지가 로드되었는지 확인합니다.
+ 코드에 설치되지 않은 패키지에 대한 호출이 없는지 확인합니다.
+ 패키지를 동적으로 설치하는 모든 코드를 수정합니다.
 
패키지가 기본 라이브러리에 설치되면 다른 라이브러리가 R 코드에 지정되어 있어도 R 런타임이 기본 라이브러리에서 패키지를 로드합니다.

## <a name="see-also"></a>관련 항목:
