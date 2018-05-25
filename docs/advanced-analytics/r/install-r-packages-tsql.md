---
title: T-SQL (외부 라이브러리 만들기)를 사용 하 여 SQL Server 컴퓨터 학습 서비스에서 R 패키지를 설치 하려면 | Microsoft Docs
description: SQL Server 2017 컴퓨터 학습 Services (In-database)에 새 R 패키지를 추가 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/20/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: bbc1adf4868cbfbd02afe5cae3a38fd6223e2d4d
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server-2017-machine-learning-services"></a>T-SQL (외부 라이브러리 만들기)를 사용 하 여 SQL Server 2017 컴퓨터 학습 서비스에서 R 패키지를 설치 하려면
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 기계 학습 사용 하도록 설정 하는 SQL Server 인스턴스에 새 R 패키지를 설치 하는 방법을 설명 합니다. 선택 하는 방법은 여러 가지가 있습니다. 이 방법은 가장 오른쪽에 익숙하지 않은 하는 서버 관리자 작동

**적용 대상:**  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

[외부 라이브러리 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) Python 코드를 직접 또는 문을 사용 하면 R을 실행 하지 않고 인스턴스 또는 특정 데이터베이스 또는 패키지의 패키지 집합을 추가할 수 있습니다. 그러나이 메서드는 패키지 준비 및 추가 데이터베이스 사용 권한이 필요 합니다.

+ 모든 패키지는 인터넷에서 필요에 따라 다운로드할 대신 로컬 압축 된 파일 사용 가능 해야 합니다.

+ 모든 종속성 이름 및 버전을 식별 하 고 zip 파일에 포함 해야 합니다. 문이 필요한 패키지를 다운스트림 패키지 종속 파일을 포함 하 여를 사용할 수 없는 경우 실패 합니다. 

+ 데이터베이스에 필요한 권한이 있어야 합니다. 자세한 내용은 참조 [외부 라이브러리 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)합니다.

## <a name="download-packages-in-archive-format"></a>보관 파일 형식에서 패키지를 다운로드 합니다.

단일 패키지를 설치 하는 경우 압축 된 형식의 패키지를에서 다운로드 합니다.

패키지는 다른 패키지에 필요한 경우 필요한 패키지를 사용할 수 있는지 확인 해야 합니다. 대상 패키지를 분석 하 고 모든 해당 종속성을 확인할 miniCRAN를 사용할 수 있습니다. 사용 하는 것이 좋습니다 [ **miniCRAN** ](create-a-local-package-repository-using-minicran.md) 또는 [ **igraph** ](http://igraph.org/r/) 패키지 종속성을 분석에 대 한 합니다. 잘못 된 버전의 패키지 또는 패키지 종속성을 설치 하는 문이 실패 발생할 수 있습니다. 

## <a name="copy-the-file-to-a-local-folder"></a>파일을 로컬 폴더에 복사

서버에서 로컬 폴더에 모든 패키지가 포함 된 압축된 파일을 복사 합니다. 서버에서 파일 시스템에 액세스할 수 없는 경우 전달할 수도 있습니다는 완전 한 패키지 변수를 이진 형식을 사용 하 여 합니다. 자세한 내용은 참조 [외부 라이브러리 만들기](../../t-sql/statements/create-external-library-transact-sql.md)합니다.

## <a name="run-the-statement-to-upload-packages"></a>문을 실행 하 고 패키지 업로드

열기는 **쿼리** 창에서 관리자 권한을 가진 계정을 사용 합니다.

T-SQL 문 실행 `CREATE EXTERNAL LIBRARY` 압축 된 패키지 컬렉션 데이터베이스에 업로드 합니다.

    For example, the following statement names as the package source a miniCRAN repository containing the **randomForest** package, together with its dependencies. 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    You cannot use an arbitrary name; the external library name must have the same name that you expect to use when loading or calling the package.

## <a name="verify-package-installation"></a>패키지 설치 확인

라이브러리 정상적으로 작성 하는 경우에 저장 프로시저 호출 하 여 SQL Server에서 패키지를 실행할 수 있습니다.
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    library(randomForest)'
    ```

