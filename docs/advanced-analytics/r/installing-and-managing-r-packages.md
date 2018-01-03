---
title: "SQL Server와 함께 설치 된 R 패키지 | Microsoft Docs"
ms.custom: 
ms.date: 09/29/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 070e1776f0a9760742e933064be569818fe200b2
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="r-packages-installed-with-sql-server"></a>SQL Server와 함께 설치 된 R 패키지

이 문서는 SQL Server와 함께 설치 된 R 패키지에 설명 하 고 관리 하 고 기존 패키지를 확인 하는 방법에 대 한 정보를 제공 합니다.

이 문서에는 또한 SQL Server와 함께 사용 하기 위해 새 패키지를 추가 하는 방법에 대 한 정보 링크를 제공 합니다.

**적용 대상:** SQL Server 2017 컴퓨터 학습 Services (In-database), SQL Server 2016 R Services (In-database)

## <a name="what-is-the-instance-library-and-where-is-it"></a>인스턴스 라이브러리 무엇 이며 여기서 입니까?

SQL Server에서 실행 되는 모든 R 솔루션 인스턴스와 연결 된 기본 R 라이브러리에 설치 된 패키지에만 사용할 수 있습니다.

SQL Server에서 R 기능을 설치 하는 경우 R 패키지 라이브러리 인스턴스 폴더에 있습니다.

+ 기본 인스턴스 *MSSQLSERVER* 

    SQL Server 2017:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` 
    
    SQL Server 2016의 경우:`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`

+ 명명 된 인스턴스 *인스턴스 MyNamedInstance* 

    SQL Server 2017:`C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` 
    
    SQL Server 2016의 경우:`C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library`

다음 문을 실행하여 R의 현재 인스턴스에 대한 기본 라이브러리를 확인할 수 있습니다.

```SQL
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```
## <a name="r-packages-installed-with-sql-server"></a>SQL Server와 함께 설치 된 R 패키지

R 기본적으로 SQL Server에서 R 언어를 설치 하는 경우 **기본** 패키지도 설치 합니다. 과 같은 패키지에서 제공 하는 핵심 기능을 포함 하는 기본 패키지 `stats` 및 `utils`합니다.

SQL Server 2016 및 SQL Server 2017에서 R의 설치도 포함 되어는 **RevoScaleR** 패키지 및 관련된 향상 된 패키지 및 공급자가 원격 계산 컨텍스트를 지 원하는 스트리밍, 병렬 rx 함수를 실행 하 고 다른 여러 기능이 있습니다.

+ 향상된 된 R 기능 개요를 참조 하세요. [컴퓨터 학습 서버에 대 한](https://docs.microsoft.com/r-server/what-is-microsoft-r-server)

+ 설치 하는 클라이언트 컴퓨터로 RevoScaleR 라이브러리를 다운로드 하려면 [Microsoft R Client](https://docs.microsoft.com/r-server/r-client/what-is-microsoft-r-client)

## <a name="permissions-required-for-installing-r-packages"></a>R 패키지를 설치에 필요한 사용 권한

SQL Server 2016에서 관리자는 인스턴스 전체에서 새 R 패키지를 설치 해야 했습니다. SQL Server 2017 년 1에서 데이터베이스 관리자 선택 된 사용자에 대 한 패키지 관리를 위임 하는 기능을 제공 하는 새 데이터베이스 기능 추가 되었습니다.

이 섹션에서는 설치 하 고 버전 당 패키지를 관리 하는 데 필요한 사용 권한을 설명 합니다.

+ SQL Server 2016 R Services (In-database)

    실행 중인 컴퓨터에 새 R 패키지를 설치 하려면 [!INCLUDE [ssCurrent](..\..\includes\sscurrent-md.md)], 컴퓨터에 대 한 관리 권한이 있어야 합니다. 필요한 모든 패키지에 설치 되어 있는지 확인 하려면 데이터베이스 관리자 또는 서버에서 다른 관리자의 작업은 [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] 인스턴스.

    하지 않은 경우 관리자 권한이 컴퓨터에 호스트 하는 [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] 인스턴스 있습니다 수 R 패키지를 설치 하는 방법에 대 한 관리자 정보를 제공 및 보안 패키지 저장소에 액세스할 수 있는 패키지 요청한 사용자가 얻을 수 있습니다.

+ SQL Server 2017 Machine Learning Services

    이 릴리스에서 데이터베이스 관리자가 선택한 사용자에 게 패키지 설치 권한을 위임할 수 있도록 패키지 관리 함수를 포함 합니다. 이 기능을 사용 하는 경우 데이터베이스 관리자가 새 패키지 역할 중 하나를 있습니다 추가 요청 합니다. 자세한 내용은 참조 [SQL Server에 대 한 R 패키지 관리](r-package-management-for-sql-server-r-services.md)합니다.

    SQL Server 인스턴스의 관리자 인 경우에 새 패키지를 설치할 수 있습니다. 방금 인스턴스와 연결 된 기본 라이브러리를 사용 해야 합니다. 다른 위치에 설치 된 패키지에는 저장된 프로시저에서 호출 될 때 실행할 수 없습니다. 사용 하 여 SQL Server 계산 컨텍스트도도 실행 되는 R 코드는 인스턴스 라이브러리의 패키지 사용할 수 있어야 합니다.

+ R Server (Standalone)

    새 R 패키지를 설치 하는 컴퓨터에 대 한 관리 권한을 해야 합니다.

+ 다른 클라이언트 환경

    R 워크스테이션으로 사용 되는 컴퓨터에 새 R 패키지를 설치 하는 한 컴퓨터에서는 **하지** 인스턴스가 [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] 설치 보내야 하는 컴퓨터에 관리 권한을 패키지를 설치 합니다. 패키지를 설치한 후 로컬 컴퓨터에서 실행할 수 있습니다.

## <a name="managing-or-viewing-installed-packages"></a>설치 된 패키지를 관리 또는 보기

현재 설치 된 패키지의 전체 목록을 얻을 수 있는 여러 가지가 있습니다. 자세한 내용은 참조 [패키지는 SQL Server에 설치 된 확인](determine-which-packages-are-installed-on-sql-server.md)합니다.
