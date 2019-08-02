---
title: 새 R 언어 패키지 설치
description: SQL Server 2016 R Services 또는 SQL Server Machine Learning Services에 새 R 패키지 추가 (데이터베이스 내)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1048dc6ef0a43c5fa41dd5398a5b3dced4a5ebe8
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715100"
---
# <a name="install-new-r-packages-on-sql-server"></a>SQL Server에 새 R 패키지 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 machine learning을 사용 하는 SQL Server 인스턴스에 새 R 패키지를 설치 하는 방법을 설명 합니다. 새 R 패키지를 설치 하는 방법에는 여러 가지가 있으며, 해당 SQL Server 버전에 따라 서버에 인터넷 연결이 있는지 여부가 결정 됩니다. 새 패키지를 설치 하는 다음과 같은 방법을 사용할 수 있습니다.

| 접근 방식                           | 사용 권한               | 원격/로컬 |
|------------------------------------|---------------------------|--------------|
| [기존 R 패키지 관리자 사용](use-r-package-managers-on-sql-server.md)  | Admin | 로컬 |
| [RevoScaleR 사용](use-revoscaler-to-manage-r-packages.md) |  이후에 관리자 사용, 데이터베이스 역할 | both|
| [T-sql 사용 (외부 라이브러리 만들기)](install-r-packages-tsql.md) | 이후에 관리자 사용, 데이터베이스 역할 | both 

## <a name="who-installs-permissions"></a>설치 (권한)

R 패키지 라이브러리는 실제로 SQL Server 인스턴스의 Program Files 폴더에 있는 액세스 권한이 제한 된 보안 폴더에 있습니다. 이 위치에 쓰려면 관리자 권한이 필요 합니다.

관리자가 아닌 관리자는 패키지를 설치할 수 있지만 이렇게 하려면 초기 설치에서 사용할 수 없는 추가 구성 및 기능이 필요 합니다. 관리자가 아닌 패키지를 설치 하는 방법에는 두 가지가 있습니다. RevoScaleR는 9.0.1 이상 버전을 사용 하거나 CREATE EXTERNAL LIBRARY (SQL Server 2017에만 해당)를 사용 합니다. SQL Server 2017에서 **dbo_owner** 또는 CREATE EXTERNAL LIBRARY 권한이 있는 다른 사용자는 R 패키지를 현재 데이터베이스에 설치할 수 있습니다.

R 개발자는 중앙에서 찾은 라이브러리의 제한이 없는 경우 필요한 패키지용 사용자 라이브러리를 만드는 데 익숙합니다. 이 방법은 SQL Server 데이터베이스 엔진 인스턴스에서 R 코드를 실행 하는 데 문제가 있습니다. 라이브러리는 동일한 컴퓨터에 있는 경우에도 외부 라이브러리에서 패키지를 로드할 수 SQL Server. SQL Server에서 실행 되는 R 코드에서 인스턴스 라이브러리의 패키지만 사용할 수 있습니다.

파일 시스템 액세스는 일반적으로 서버에서 제한 되며, 서버의 사용자 문서 폴더에 대 한 관리자 권한 및 액세스 권한이 있는 경우에도 SQL Server에서 실행 되는 외부 스크립트 런타임이 기본 인스턴스 외부에 설치 된 패키지에 액세스할 수 없습니다. 라이브러리. 

## <a name="considerations-for-package-installation"></a>패키지 설치 시 고려 사항

새 패키지를 설치 하기 전에 지정 된 패키지에서 사용 하도록 설정 된 기능이 SQL Server 환경에 적합 한지 여부를 고려 합니다. 강화 된 SQL Server 환경에서는 다음을 방지 해야 할 수 있습니다.

+ 네트워크 액세스가 필요한 패키지
+ 관리자 권한으로 파일 시스템에 액세스 해야 하는 패키지
+ 패키지는 웹 개발 또는 내부에서 실행 하 여 이점을 얻지 못하는 기타 작업에 사용 됩니다 SQL Server

## <a name="offline-installation-no-internet-access"></a>오프 라인 설치 (인터넷 액세스 없음)

일반적으로 프로덕션 데이터베이스를 호스트 하는 서버는 인터넷 연결을 차단 합니다. 이러한 환경에서 새로운 R 또는 Python 패키지를 설치 하려면 패키지와 종속성을 미리 준비 하 고 오프 라인 설치를 위해 서버의 폴더에 파일을 복사 해야 합니다.

모든 종속성을 식별 하는 것은 복잡 합니다. R의 경우 [miniCRAN를 사용 하 여 로컬 리포지토리를 만든](create-a-local-package-repository-using-minicran.md) 다음 완전히 정의 된 리포지토리를 격리 된 SQL Server 인스턴스로 전송 하는 것이 좋습니다.

또는 이러한 단계를 수동으로 수행할 수 있습니다.

1. 모든 패키지 종속성을 식별 합니다. 
2. 필요한 패키지가 서버에 이미 설치 되어 있는지 확인 합니다. 패키지가 설치 되어 있으면 버전이 올바른지 확인 합니다.
3. 패키지 및 모든 종속성을 별도의 컴퓨터에 다운로드 합니다.
4. 서버에서 액세스할 수 있는 폴더로 파일을 이동 합니다.
5. 지원 되는 설치 명령 또는 DDL 문을 실행 하 여 인스턴스 라이브러리에 패키지를 설치 합니다.

### <a name="download-the-package-as-a-zipped-file"></a>압축 파일로 패키지 다운로드

인터넷에 연결 되지 않은 서버에 설치 하는 경우 오프 라인 설치를 위해 압축 된 파일 형식으로 패키지의 복사본을 다운로드 해야 합니다. **패키지의 압축을 풀어야 합니다.**

예를 들어 다음 절차에서는 컴퓨터에서 인터넷에 액세스할 수 있다고 가정 하 여 Bioconductor에서 [FISHalyseR](https://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) 패키지의 올바른 버전을 가져오는 방법을 설명 합니다.

1.  **패키지 보관** 목록에서 **Windows 이진** 버전을 찾습니다.

2.  에 대 한 링크를 마우스 오른쪽 단추로 클릭 합니다. ZIP 파일을 선택 하 고 **다른 이름으로 대상 저장**을 선택 합니다.

3.  압축 된 패키지가 저장 된 로컬 폴더로 이동 하 고 **저장**을 클릭 합니다.

    이 프로세스는 패키지의 로컬 복사본을 만듭니다. 

4. 다운로드 오류가 발생 하면 다른 미러 사이트를 사용해 보세요.

5. 패키지 보관 파일을 다운로드 한 후에는 패키지를 설치 하거나, 인터넷에 액세스할 수 없는 서버에 압축 된 패키지를 복사할 수 있습니다.

> [!TIP]
> 실수로 이진 파일을 다운로드 하는 대신 패키지를 설치 하면 다운로드 한 압축 파일의 복사본도 컴퓨터에 저장 됩니다. 패키지를 설치할 때 상태 메시지를 보고 파일 위치를 확인 합니다. 인터넷에 액세스할 수 없는 서버에 압축 된 파일을 복사할 수 있습니다.
> 
> 그러나이 메서드를 사용 하 여 패키지를 가져오는 경우 종속성이 포함 되지 않습니다. 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>독립 실행형 R 또는 Python 서버와 함께 설치

R 및 Python 기능은 여러 Microsoft 제품에 포함 되어 있으며, 모두 동일한 컴퓨터에 공존할 수 있습니다.

SQL Server 2017 Microsoft Machine Learning Server (독립 실행형) 또는 SQL Server 2016 R 서버 (독립 실행형) 외에도 데이터베이스 내 분석 (SQL Server Machine Learning Services 및 SQL Server 2016 R 서비스)을 설치한 경우 컴퓨터에는 별도의 모든 R 도구 및 라이브러리의 중복 항목을 포함 하 여 각에 대 한 R 설치

R_SERVER 라이브러리에 설치 된 패키지는 독립 실행형 서버 에서만 사용 되며 SQL Server (데이터베이스 내) 인스턴스에서는 액세스할 수 없습니다. SQL Server에서 데이터베이스 `R_SERVICES` 내에 사용할 패키지를 설치할 때 항상 라이브러리를 사용 합니다. 경로에 대 한 자세한 내용은 [패키지 라이브러리 위치](../package-management/default-packages.md)를 참조 하세요.

## <a name="see-also"></a>참조

+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [자습서, 샘플, 솔루션](../tutorials/machine-learning-services-tutorials.md)
