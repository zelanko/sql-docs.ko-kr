---
title: T-sql (CREATE EXTERNAL LIBRARY)을 사용 하 여 R 패키지 설치
description: SQL Server 2016 R Services 또는 SQL Server 2017 Machine Learning Services (데이터베이스 내)에 새 R 패키지를 추가 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/12/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: f681634b9f57a5fd459e3f6452c04aba024bd297
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345308"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server"></a>T-sql (CREATE EXTERNAL LIBRARY)을 사용 하 여 SQL Server에 R 패키지 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 machine learning이 사용 되는 SQL Server 인스턴스에 새 R 패키지를 설치 하는 방법을 설명 합니다. 여러 가지 방법 중에서 선택할 수 있습니다. T-sql을 사용 하는 것은 R에 익숙하지 않은 서버 관리자에 게 가장 적합 합니다.

**적용 대상:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]  [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 문을 사용 하면 R 또는 Python 코드를 직접 실행 하지 않고도 인스턴스 또는 특정 데이터베이스에 패키지 또는 패키지 집합을 추가할 수 있습니다. 그러나이 방법에는 패키지 준비와 추가 데이터베이스 권한이 필요 합니다.

+ 모든 패키지는 인터넷에서 요청 시 다운로드 되는 것이 아니라 로컬 압축 파일로 사용할 수 있어야 합니다.

+ 모든 종속성은 이름 및 버전으로 식별 되 고 zip 파일에 포함 되어야 합니다. 다운스트림 패키지 종속성을 포함 하 여 필요한 패키지를 사용할 수 없는 경우 문이 실패 합니다. 

+ **Db_owner** 이거나 데이터베이스 역할에 대 한 CREATE EXTERNAL LIBRARY 권한이 있어야 합니다. 자세한 내용은 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)를 참조 하세요.

## <a name="download-packages-in-archive-format"></a>보관 형식으로 패키지 다운로드

단일 패키지를 설치 하는 경우 패키지를 압축 형식으로 다운로드 합니다.

패키지 종속성으로 인해 여러 패키지를 설치 하는 것이 더 일반적입니다. 패키지에 다른 패키지가 필요한 경우 설치 하는 동안 해당 패키지에 모두 액세스할 수 있는지 확인 해야 합니다. [MiniCRAN](https://andrie.github.io/miniCRAN/) 를 사용 하 여 패키지 종속성을 분석 하는 [igraph](https://igraph.org/r/) 뿐만 아니라 전체 패키지 컬렉션을 조합 하는 [로컬 리포지토리를 만드는](create-a-local-package-repository-using-minicran.md) 것이 좋습니다. 잘못 된 버전의 패키지를 설치 하거나 패키지 종속성을 생략 하면 CREATE EXTERNAL LIBRARY 문이 실패할 수 있습니다. 

## <a name="copy-the-file-to-a-local-folder"></a>로컬 폴더에 파일을 복사 합니다.

모든 패키지가 포함 된 압축 파일을 서버의 로컬 폴더에 복사 합니다. 서버의 파일 시스템에 대 한 액세스 권한이 없는 경우 이진 형식을 사용 하 여 전체 패키지를 변수로 전달할 수도 있습니다. 자세한 내용은 [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)를 참조 하세요.

## <a name="run-the-statement-to-upload-packages"></a>문을 실행 하 여 패키지 업로드

관리자 권한이 있는 계정을 사용 하 여 **쿼리** 창을 엽니다.

T-sql 문을 `CREATE EXTERNAL LIBRARY` 실행 하 여 압축 된 패키지 컬렉션을 데이터베이스에 업로드 합니다.

예를 들어 다음 문은 패키지 원본으로 **randomForest** 패키지를 포함 하는 miniCRAN 리포지토리와 해당 종속성을 포함 합니다. 

```sql
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

임의의 이름을 사용할 수 없습니다. 외부 라이브러리 이름은 패키지를 로드 하거나 호출할 때 사용할 것으로 간주 되는 이름과 같아야 합니다.

## <a name="verify-package-installation"></a>패키지 설치 확인

라이브러리가 성공적으로 만들어지면 저장 프로시저 내에서 호출 하 여 SQL Server에서 패키지를 실행할 수 있습니다.
    
```sql
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>참조

+ [패키지 정보 가져오기](../package-management/installed-package-information.md)
+ [R 자습서](../tutorials/sql-server-r-tutorials.md)
