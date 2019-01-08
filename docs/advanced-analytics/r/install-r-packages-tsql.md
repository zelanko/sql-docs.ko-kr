---
title: T-SQL (CREATE EXTERNAL LIBRARY)을 사용 하 여 R 패키지-SQL Server Machine Learning Services를 설치 합니다.
description: SQL Server 2016 R Services 또는 SQL Server 2017 Machine Learning Services (In-database)에 새 R 패키지를 추가 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6e910f1c3b29522b11f1faa83db890d399bf3680
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645052"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server"></a>T-SQL (CREATE EXTERNAL LIBRARY)를 사용 하 여 SQL Server에서 R 패키지 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 machine learning이 사용 되는 SQL Server 인스턴스에 새로운 R 패키지를 설치 하는 방법에 설명 합니다. 선택 하는 방법은 여러 가지가 있습니다. T-SQL을 사용 하 여 적합 한 다양 한 서버 관리자에 게 익숙하지 R.

**적용 대상:**  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) Python 코드를 직접 또는 문을 사용 하면 R을 실행 하지 않고 인스턴스 또는 특정 데이터베이스에 패키지 또는 패키지의 집합을 추가할 수 있습니다. 그러나이 메서드는 패키지 준비 및 추가 데이터베이스 권한이 필요합니다.

+ 모든 패키지는 인터넷에서 필요에 따라 다운로드 하는 대신 로컬 압축 된 파일로 사용할 수 있어야 합니다.

+ 모든 종속성 이름 및 버전을 식별 하 고 zip 파일에 포함 해야 합니다. 문이 필요한 패키지를 다운스트림 패키지 종속성을 포함 하 여 사용할 수 없는 경우 실패 합니다. 

+ 해야 **db_owner** 데이터베이스 역할에 대 한 CREATE EXTERNAL LIBRARY 권한이 있습니다. 자세한 내용은 참조 하세요 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)합니다.

## <a name="download-packages-in-archive-format"></a>보관 파일 형식으로 패키지를 다운로드 합니다.

단일 패키지를 설치 하는 경우 압축 된 형식으로 패키지를 다운로드 합니다.

것이 더 일반적 패키지 종속성으로 인해 여러 패키지를 설치 합니다. 패키지가 다른 패키지에 필요한 경우 모두에 설치 하는 동안 서로 액세스할 수 있는지 확인 해야 합니다. 것이 좋습니다 [로컬 리포지토리를 만드는](create-a-local-package-repository-using-minicran.md) 사용 하 여 [miniCRAN](https://andrie.github.io/miniCRAN/) 패키지의 전체 컬렉션을 조합 하 뿐만 [igraph](https://igraph.org/r/) 패키지 종속성을 분석 합니다. 잘못 된 버전의 패키지를 설치 하거나 패키지 종속성을 생략 하면 실패 하는 CREATE EXTERNAL LIBRARY 문을 발생할 수 있습니다. 

## <a name="copy-the-file-to-a-local-folder"></a>로컬 폴더에 파일 복사

서버의 로컬 폴더에 모든 패키지가 포함 된 zip 파일을 복사 합니다. 서버의 파일 시스템에 액세스할 수 없으면 전달할 수도 있습니다 전체 패키지 된 변수로 이진 형식을 사용 하 여 합니다. 자세한 내용은 [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)합니다.

## <a name="run-the-statement-to-upload-packages"></a>패키지를 업로드 하는 문을 실행합니다

엽니다는 **쿼리** 창에서 관리자 권한이 있는 계정으로 합니다.

T-SQL 문을 실행 `CREATE EXTERNAL LIBRARY` 압축 된 패키지 컬렉션 데이터베이스에 업로드 합니다.

예를 들어 다음 문은 이름이 패키지 원본으로 포함 하는 miniCRAN 리포지토리를 **randomForest** 종속 항목과 함께 패키지 합니다. 

```sql
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

임의의 이름을; 사용할 수 없습니다. 외부 라이브러리 이름에는 로드 또는 패키지를 호출할 때 사용 되는 이름이 있어야 합니다.

## <a name="verify-package-installation"></a>패키지 설치를 확인 합니다.

라이브러리를 성공적으로 만들어진 경우에 저장된 프로시저 내에서 호출 하 여 SQL Server에서 패키지를 실행할 수 있습니다.
    
```sql
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>참고자료

+ [패키지 정보 가져오기](determine-which-packages-are-installed-on-sql-server.md)
+ [R 자습서](../tutorials/sql-server-r-tutorials.md)
+ [방법 가이드](sql-server-machine-learning-tasks.md)