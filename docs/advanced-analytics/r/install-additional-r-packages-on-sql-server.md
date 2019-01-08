---
title: 새 R 언어 패키지-SQL Server Machine Learning Services 설치
description: SQL Server 2016 R Services 또는 SQL Server 2017 Machine Learning Services (In-database)를 새 R 패키지를 추가 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 590dbcc08d433147b61678c2b865ba205a0e547d
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432806"
---
# <a name="install-new-r-packages-on-sql-server"></a>SQL Server에 새로운 R 패키지 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 machine learning이 사용 되는 SQL Server 인스턴스에 새로운 R 패키지를 설치 하는 방법을 설명 합니다. SQL server 버전에 있고 인터넷에 연결 되어 있는지에 따라 새 R 패키지를 설치 하는 방법은 여러 가지가 있습니다. 새 패키지 설치를 위한 다음 방법을 사용할 수 있습니다.

| 방법                           | 사용 권한               | 원격/로컬 |
|------------------------------------|---------------------------|--------------|
| [기존 R 패키지 관리자를 사용 합니다.](use-r-package-managers-on-sql-server.md)  | Admin | 로컬 |
| [RevoScaleR 사용](use-revoscaler-to-manage-r-packages.md) |  데이터베이스 역할 관리자 활성화 나중에 | both|
| [T-SQL (CREATE EXTERNAL LIBRARY) 사용](install-r-packages-tsql.md) | 데이터베이스 역할 관리자 활성화 나중에 | both 

## <a name="who-installs-permissions"></a>(사용 권한)를 설치 하는

R 패키지 라이브러리를 물리적으로 제한 된 액세스를 사용 하 여 안전한 폴더에서 SQL Server 인스턴스, Program Files 폴더에 있습니다. 이 위치에 쓰기는 관리자 권한이 필요합니다.

관리자가 아닌 패키지를 설치할 수 있지만 이렇게 하려면 addititional 구성 및 기능 초기 설치에서 사용할 수 없습니다. 관리자가 아닌 패키지 설치 하는 방법은 두 가지가 있습니다. RevoScaleR 버전 9.0.1 사용 하거나 나중에 CREATE EXTERNAL LIBRARY (SQL Server 2017에만 해당)를 사용 하 여 합니다. SQL Server 2017에서 **dbo_owner** 또는 현재 데이터베이스에 CREATE EXTERNAL LIBRARY 권한이 있는 사용자를 다른 R 패키지를 설치할 수 있습니다.

R 개발자가 익숙한 중앙에 위치한 라이브러리 쉽지 경우 필요한 패키지에 대 한 사용자 라이브러리 만들기. 이 방법은 SQL Server 데이터베이스 엔진 인스턴스를 실행 하는 R 코드에 대 한 문제가 됩니다. 해당 라이브러리는 동일한 컴퓨터의 경우에 SQL Server 외부 라이브러리에서 패키지를 로드할 수 없습니다. SQL Server에서 실행 되는 R 코드에서 인스턴스 라이브러리에서 패키지에만 사용할 수 있습니다.

파일 시스템 액세스가 서버에서 일반적으로 제한 되 고 서버의 사용자 문서 폴더에 관리자 권한 및 액세스를 해야 하는 경우에 SQL Server에서 실행 하는 외부 스크립트 런타임 기본 인스턴스 외부에 설치 된 모든 패키지에 액세스할 수 없습니다. 라이브러리입니다. 

## <a name="considerations-for-package-installation"></a>패키지 설치 시 고려 사항

새 패키지를 설치 하기 전에 지정 된 패키지에서 사용할 수 있는 기능 SQL Server 환경에 적합 한지를 고려 합니다. 확정 된 SQL Server 환경에서 다음을 방지 수 있습니다.

+ 네트워크 액세스 해야 하는 패키지
+ Java 또는 SQL Server 환경에서 사용 되지 일반적으로 다른 프레임 워크를 필요로 하는 패키지
+ 상승 된 파일 시스템 액세스를 필요로 하는 패키지
+ 웹 개발 또는 SQL Server 내에서 실행 하 여 활용 하지 하는 기타 작업에 대 한 패키지는

## <a name="offline-installation-no-internet-access"></a>오프 라인 설치 (인터넷 액세스 없음)

일반적으로 프로덕션 데이터베이스를 호스팅하는 서버는 인터넷 연결을 차단 합니다. 이러한 환경에서 새 R 또는 Python 패키지 설치 패키지 및 종속성을 미리 준비 하는 오프 라인 설치에 대 한 서버의 폴더로 파일을 복사 해야 합니다.

모든 종속성을 식별 복잡해 집니다. R을 사용 하는 권장 [로컬 리포지토리를 만드는 miniCRAN](create-a-local-package-repository-using-minicran.md) 다음 격리 된 SQL Server 인스턴스를 완전히 정의 된 리포지토리를 전송 합니다.

Alternativley를 사용 하면이 단계를 수동으로 수행할 수 있습니다.:

1. 모든 패키지 종속성을 식별 합니다. 
2. 모든 필요한 패키지를 서버에 이미 설치 되어 있는지 여부를 확인 합니다. 패키지를 설치 하는 경우 버전이 올바른지 확인 합니다.
3. 별도 컴퓨터에 패키지 및 모든 종속성을 다운로드 합니다.
4. 파일 서버에서 액세스할 수 있는 폴더를 이동 합니다.
5. 인스턴스 라이브러리에 패키지를 설치 하려면 지원 되는 설치 명령 또는 DDL 문을 실행 합니다.

### <a name="download-the-package-as-a-zipped-file"></a>패키지를 압축 된 파일로 다운로드

인터넷 액세스 없이 서버에서 설치에 대 한 오프 라인 설치에 대 한 압축 된 파일의 형식으로 패키지의 복사본을 다운로드 해야 합니다. **패키지를 압축을 풉니다지 않습니다.**

다음 절차의 올바른 버전을 가져오려면 하려면 지금 설명 하는 예를 들어 합니다 [FISHalyseR](https://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) Bioconductor, 컴퓨터가 인터넷에 액세스 하는 것으로 가정에서 패키지 합니다.

1.  **패키지 보관** 목록에서 **Windows 이진** 버전을 찾습니다.

2.  에 대 한 링크를 마우스 오른쪽 단추로 클릭 합니다. ZIP 파일을 선택한 **다른 이름으로 대상 저장**합니다.

3.  압축 된 패키지가 저장 됩니다 하 고 클릭 있는 로컬 폴더로 이동할 **저장할**합니다.

    이 프로세스는 패키지의 로컬 복사본을 만듭니다. 

4. 다운로드 오류가 발생할 경우 다른 미러 사이트를 시도 합니다.

5. 패키지 보관 파일을 다운로드 한 후 패키지를 설치할 수도 있고 인터넷 액세스가 없는 서버에 압축된 된 패키지를 복사할 수 있습니다.

> [!TIP]
> 이진 파일을 다운로드 하는 대신 패키지를 설치한 실수로 경우 다운로드 한 zip 파일의 복사본은 컴퓨터에도 저장 됩니다. 패키지 파일 위치를 확인 하려면 설치 되어 상태 메시지를 확인 합니다. 인터넷 액세스가 없는 서버에는 압축 된 파일을 복사할 수 있습니다.
> 
> 그러나이 메서드를 사용 하 여 패키지를 얻을 때 종속성 포함 되지 않습니다. 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>독립 실행형 R 또는 Python 서버를 사용 하 여 side-by-side-설치

R 및 Python 기능 모두 동일한 컴퓨터에 공존할 수 여러 Microsoft 제품에 포함 됩니다.

컴퓨터에 별도 데이터베이스 내 분석 (SQL Server 2017의 Machine Learning Services 및 SQL Server 2016 R Services) 외에도 SQL Server 2017 Microsoft Machine Learning Server (독립 실행형) 또는 SQL Server 2016 R Server (독립 실행형)를 설치한 경우 모든 R 도구 및 라이브러리의 중복 항목 각각에 대 한 R 설치입니다.

R_SERVER 라이브러리에 설치 된 패키지를 독립 실행형 서버 에서만 사용 되 고 (In-database) SQL Server 인스턴스에서 액세스할 수 없습니다. 항상 사용은 `R_SERVICES` 라이브러리 데이터베이스에서 SQL Server를 사용 하려는 패키지를 설치 하는 경우. 경로 대 한 자세한 내용은 참조 하세요. [패키지 라이브러리 위치](installing-and-managing-r-packages.md#package-library-location)합니다.


## <a name="see-also"></a>참고자료

+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [자습서, 샘플, 솔루션](../tutorials/machine-learning-services-tutorials.md)