---
title: "사용자 라이브러리에 설치 된 R 패키지에서 오류를 방지 | Microsoft Docs"
ms.custom: 
ms.date: 09/29/2017
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 0de06ebee16d903b4b00c9d8e4673bf450c485d1
ms.contentlocale: ko-kr
ms.lasthandoff: 10/10/2017

---
# <a name="avoiding-errors-on-r-packages-installed-in-user-libraries"></a>사용자 라이브러리에 설치 된 R 패키지에서 오류를 방지 합니다.

숙련 된 R 사용자가 차단 되거나 사용할 수 없는 기본 라이브러리는 때마다 사용자 라이브러리에서 R 패키지를 설치 하는 데 익숙한 합니다. 그러나이 방법은 SQL Server에서 지원 되지 않습니다 및 "패키지를 찾을 수 없음" 오류 일반적으로 끝나는 사용자 라이브러리를 설치 합니다.

이 항목에서는이 오류를 방지할 수 있도록 해결 방법을 제공 합니다. R 코드를 수정 하는 방법에 대해 설명 하 고 SQL Server 인스턴스에서 R 패키지를 사용 하기 위한 올바른 R 패키지 설치 프로세스를 제안 합니다.

## <a name="why-r-user-libraries-cannot-be-accessed-from-sql-server"></a>SQL Server에서 R 사용자 라이브러리 액세스할 수 없는 이유

새 R 패키지를 설치 해야 하는 R 개발자가 패키지를 설치 하 고 기본 라이브러리를 사용할 수 없을 때마다 또는 개발자 컴퓨터에서 관리자가 아닌 경우 개인 사용자 라이브러리를 사용 하 여에 익숙한 합니다.

예를 들어 일반적인 R 개발 환경에서 사용자가 패키지의 위치에 추가 R 환경 변수 `libPath`, 또는 다음과 같이 전체 패키지 경로 참조 합니다.

```R
library("c:/Users/<username>/R/win-library/packagename")  
```

그러나이 수 작동 하지 않습니다 SQL Server에서 R 솔루션을 실행 하는 경우 R 패키지는 인스턴스와 연결 된 특정 기본 라이브러리를 설치 해야 하기 때문에 있습니다.

패키지가 기본 라이브러리에 설치되지 않으면 패키지를 호출하려고 할 때 이 오류가 발생할 수 있습니다.

*Library(xxx)의 오류: ' 패키지 name ' 없는 패키지는*

오류를 일으킬 수 있는 솔루션 라이브러리 위치에 대 한 액세스 권한이 없는 다른 사용자가 실행 되는 경우 처럼 사용자 지정 사용자 라이브러리에 필요한 R 패키지를 설치 하는 잘못 된 개발 좋습니다 이기도 합니다.

## <a name="how-to-install-r-packages-to-an-accessible-library"></a>액세스할 수 있는 라이브러리에 R 패키지를 설치 하는 방법

**SQL Server 2016에 대 한**

인스턴스와 연결 된 패키지 라이브러리를 사용 합니다. 자세한 내용은 참조 [SQL Server와 함께 설치 된 R 패키지](installing-and-managing-r-packages.md)

**SQL server 2017**

SQL Server는 여러 패키지 버전을 관리 하 고 사용자가 파일 시스템 액세스를 요구 하지 않고 개별 패키지에 대 한 사용자 권한을 부여 하는 데 유용한 기능을 제공 합니다.

패키지 공유 라이브러리를 설정 하 고 사용자 역할에 할당 하는 방법에 대 한 세부 정보를 참조 하십시오. [SQL Server에 대 한 R 패키지 관리](r-package-management-for-sql-server-r-services.md)합니다.

데이터베이스 역할에 따라 패키지 관리 방법을 사용 하는 경우 다른 사용자 디렉터리에는 동일한 패키지의 여러 복사본을 설치할 필요는 없습니다. 필요 하 고 인증 된 사용자와 공유 하는 패키지의 단일 복사본을 설치 합니다. 데이터베이스 수준에서 패키지를 관리 하기 때문에 패키지 및 데이터베이스 간에 관련 된 사용 권한의 그룹을 복사할 수도 있습니다.

## <a name="tips-for-avoiding-package-not-found-errors"></a>"패키지를 찾을 수 없음" 오류를 방지 하기 위한 팁

+ 사용자 라이브러리에 대 한 종속성을 제거 하는 코드를 수정 합니다. 실행할 R 솔루션을 마이그레이션할 때 [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)], 것이 중요에서 다음을 수행 합니다.

    + 인스턴스와 연결 된 기본 라이브러리에 필요한 모든 패키지를 설치 합니다.

    + 임시 디렉터리 또는 사용자 라이브러리에서가 아니라 기본 라이브러리에서 패키지를 로드 했는지 확인 하는 코드를 편집 합니다.

+ 솔루션의 일부로 임시 패키지를 설치를 하지 마십시오. 또는 설치 되지 않은 패키지를 동적으로 패키지를 설치 하는 코드에 대 한 호출 없는지 확인 하도록 코드를 확인 합니다. 권한이 없는 경우 코드가 실패 하 고 권한이 없는 경우 별도로 설치 해야 패키지를 실행 하려는 다른 코드에서.

+ R 패키지 라이브러리에 직접 경로 수정 합니다. 패키지가 기본 라이브러리에 설치되면 다른 라이브러리가 R 코드에 지정되어 있어도 R 런타임이 기본 라이브러리에서 패키지를 로드합니다.

