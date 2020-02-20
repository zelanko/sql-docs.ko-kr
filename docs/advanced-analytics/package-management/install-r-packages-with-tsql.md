---
title: T-SQL(CREATE EXTERNAL LIBRARY)을 사용하여 R 패키지 설치
description: SQL Server 2016 R Services 또는 SQL Server Machine Learning Services(데이터베이스 내)에 새 R 패키지를 추가합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/20/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: =sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: b19b2df1b39bcc88332d60f1389be12b32d7b921
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74485268"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server"></a>T-SQL(CREATE EXTERNAL LIBRARY)을 사용하여 SQL Server에 R 패키지 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 기계 학습이 사용되는 SQL Server 인스턴스에 새 R 패키지를 설치하는 방법을 설명합니다. 여러 가지 방법 중에서 선택할 수 있습니다. T-SQL을 사용하는 것은 R에 익숙하지 않은 서버 관리자에게 가장 적합합니다.

**적용 대상:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 문을 사용하면 R 또는 Python 코드를 직접 실행하지 않고도 패키지 또는 패키지 집합을 인스턴스 또는 특정 데이터베이스에 추가할 수 있습니다. 그러나 이 방법에는 패키지 준비와 추가 데이터베이스 권한이 필요합니다.

+ 모든 패키지는 인터넷에서 요청 시 다운로드되는 것이 아니라 로컬 압축 파일로 사용할 수 있어야 합니다.

+ 모든 종속성은 이름 및 버전으로 식별되고 zip 파일에 포함되어야 합니다. 다운스트림 패키지 종속성을 포함하여 필요한 패키지를 사용할 수 없는 경우 문이 실패합니다. 

+ **db_owner**이거나 데이터베이스 역할에서 CREATE EXTERNAL LIBRARY 권한이 있어야 합니다. 자세한 내용은 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)를 참조하세요.

## <a name="download-packages-in-archive-format"></a>보관 형식으로 패키지 다운로드

단일 패키지를 설치하는 경우 패키지를 압축 형식으로 다운로드합니다.

패키지 종속성 때문에 여러 패키지를 설치하는 것이 더 일반적입니다. 패키지에 다른 패키지가 필요한 경우 설치하는 동안 각 패키지에 모두 액세스할 수 있는지 확인해야 합니다. [miniCRAN](https://andrie.github.io/miniCRAN/)을 사용해 전체 패키지 컬렉션을 어셈블하여 [로컬 리포지토리를 만들고](create-a-local-package-repository-using-minicran.md) 패키지 종속성 분석을 위해 [igraph](https://igraph.org/r/)를 사용하는 것이 좋습니다. 잘못된 버전의 패키지를 설치하거나 패키지 종속성을 생략하면 CREATE EXTERNAL LIBRARY 문이 실패할 수 있습니다. 

## <a name="copy-the-file-to-a-local-folder"></a>로컬 폴더에 파일 복사

모든 패키지가 포함된 압축 파일을 서버의 로컬 폴더에 복사합니다. 서버의 파일 시스템에 대한 액세스 권한이 없는 경우 이진 형식을 사용하여 전체 패키지를 변수로 전달할 수도 있습니다. 자세한 내용은 [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)를 참조하세요.

## <a name="run-the-statement-to-upload-packages"></a>문을 실행하여 패키지 업로드

관리자 권한이 있는 계정을 사용하여 **쿼리** 창을 엽니다.

`CREATE EXTERNAL LIBRARY` T-SQL 문을 실행하여 압축된 패키지 컬렉션을 데이터베이스에 업로드합니다.

예를 들어 다음 문은 **randomForest** 패키지 및 해당 종속성을 포함하는 miniCRAN 리포지토리를 패키지 원본으로 명명합니다. 

```sql
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

임의의 이름을 사용할 수 없습니다. 외부 라이브러리 이름은 패키지를 로드하거나 호출할 때 사용할 이름과 같아야 합니다.

## <a name="verify-package-installation"></a>패키지 설치 확인

라이브러리가 성공적으로 만들어지면 저장 프로시저 내에서 호출하여 SQL Server에서 패키지를 실행할 수 있습니다.
    
```sql
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>참고 항목

+ [R 패키지 정보 가져오기](r-package-information.md)
+ [R 자습서](../tutorials/sql-server-r-tutorials.md)