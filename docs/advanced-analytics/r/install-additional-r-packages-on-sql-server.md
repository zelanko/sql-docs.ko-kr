---
title: SQL Server 컴퓨터 학습 서비스에 새 R 패키지 설치 | Microsoft Docs
description: SQL Server 2016 R Services 또는 SQL Server 2017 컴퓨터 학습 Services (In-database)에 새 R 패키지 추가
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e05842a8e8a5a1d2454dbbe500b4d5aa95fca660
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707081"
---
# <a name="install-new-r-packages-on-sql-server"></a>SQL Server에 새 R 패키지 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 기계 학습 사용 하도록 설정 하는 SQL Server 인스턴스에 새 R 패키지를 설치 하는 방법을 설명 합니다. SQL Server 버전에 있는 및 인터넷에 연결 되어 있는지에 따라 새 R 패키지를 설치 하기 위한 여러 메서드가 있습니다. 새 패키지를 설치 하기 위한 다음 방법이 될 수 있습니다.

| 방법                           | 사용 권한               | 원격/로컬 |
|------------------------------------|---------------------------|--------------|
| [기본 R 패키지 관리자를 사용 하 여](use-r-package-managers-on-sql-server.md)  | Admin | 로컬 |
| [RevoScaleR 사용](use-revoscaler-to-manage-r-packages.md) |  데이터베이스 역할 관리자 활성화 나중에 | both|
| [T-SQL (외부 라이브러리 만들기)를 사용 하 여](install-r-packages-tsql.md) | 데이터베이스 역할 관리자 활성화 나중에 | both 

## <a name="who-installs-permissions"></a>사용자 (사용 권한)를 설치 합니까

R 패키지 라이브러리는 해당 SQL Server 인스턴스의 액세스가 제한 된 보안 폴더에는 Program Files 폴더에 물리적으로 배치 됩니다. 이 위치에 대 한 관리자 권한이 필요합니다.

관리자가 아닌 패키지를 설치할 수 있지만 이렇게 하려면 addititional 구성 및 기능 초기 설치에서는 사용할 수 없습니다. 관리자가 아닌 패키지 설치의 경우에 두 가지: RevoScaleR 9.0.1 버전과 이상 또는 사용 하 여 외부 라이브러리 만들기 (SQL Server 2017에만 해당)를 사용 하 여 합니다. SQL Server 2017에 **dbo_owner** 또는 외부 라이브러리 만들기 권한이 있는 다른 사용자는 현재 데이터베이스에 R 패키지를 설치할 수 있습니다.

R 개발자 중앙에 위치한 라이브러리는 off-limits 경우 필요한 패키지에 대 한 사용자 라이브러리를 만들기에 익숙한 합니다. 이 방법은 SQL Server 데이터베이스 엔진 인스턴스에서 실행 하는 R 코드에 대 한 문제가 있는 것입니다. 해당 라이브러리를 동일한 컴퓨터에는 경우에 SQL Server 외부의 라이브러리에서 패키지를 로드할 수 없습니다. SQL Server에서 실행 되는 R 코드에서 인스턴스 라이브러리에서 패키지에만 사용할 수 있습니다.

서버에서 파일 시스템 액세스를 제한 일반적으로 되 고 서버에서 사용자 문서 폴더에 대 한 관리자 권한 및 액세스 해야 하는 경우에 SQL Server에서 실행 되는 외부 스크립트 런타임 인스턴스 외부의 기본 설치 된 모든 패키지에 액세스할 수 없습니다. 라이브러리입니다. 

## <a name="considerations-for-package-installation"></a>패키지 설치에 대 한 고려 사항

새 패키지를 설치 하기 전에 지정된 된 패키지에서 사용할 수 있는 기능 SQL Server 환경에 적합 한지 하는 것이 좋습니다. 강화 된 SQL Server 환경에서 다음을 방지 하기 위해 설정할 수 있습니다.

+ 네트워크에 액세스 해야 하는 패키지
+ Java 또는 SQL Server 환경에서 사용 하지 일반적으로 다른 프레임 워크를 필요로 하는 패키지
+ 승격 된 파일 시스템 액세스를 필요로 하는 패키지
+ 패키지를 사용 하 여 웹 개발 또는 SQL Server 내에서 실행 하 여 장점이 없는 다른 작업에 대 한

## <a name="offline-installation-no-internet-access"></a>오프 라인 설치 (인터넷 액세스 없음)

일반적으로 프로덕션 데이터베이스를 호스팅하는 서버는 인터넷 연결을 차단 합니다. 이러한 환경에 새 R, Python 패키지 설치 패키지 및 종속성을 사전에 준비할 오프 라인 설치에 대 한 서버에 있는 폴더에 파일을 복사 하 필요 합니다.

모든 종속성을 식별 복잡해 집니다. R을 사용 하는 권장 [로컬 저장소를 만드는 miniCRAN](create-a-local-package-repository-using-minicran.md) 다음 격리 된 SQL Server 인스턴스를 완전히 정의 된 리포지토리를 전송 합니다.

Alternativley를 사용 하면이 단계를 수동으로 수행할 수 있습니다.:

1. 모든 패키지 종속 파일을 식별 합니다. 
2. 필요한 패키지는 서버에 이미 설치 되어 있는지 확인 합니다. 패키지가 설치 되어 있는 경우 버전이 올바른지 확인 합니다.
3. 별도 컴퓨터에 패키지 및 모든 종속성을 다운로드 합니다.
4. 서버에서 액세스할 수 있는 폴더에 파일을 이동 합니다.
5. 인스턴스 라이브러리에 패키지를 설치 하려면 지원 되는 설치 명령이 나 DDL 문을 실행 합니다.

### <a name="download-the-package-as-a-zipped-file"></a>패키지를 압축 된 파일로 다운로드

인터넷 연결 되지 않은 서버에서 설치에 대 한 오프 라인 설치에 대 한 압축된 된 파일 형식으로 패키지의 복사본을 다운로드 해야 합니다. **패키지를 압축을 풉니다지 않습니다.**

다음 절차의 올바른 버전을 설명 하는 예를 들어는 [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) 패키지는 컴퓨터가 인터넷에 액세스 하는 것으로 가정 Bioconductor에서 합니다.

1.  **패키지 보관** 목록에서 **Windows 이진** 버전을 찾습니다.

2.  에 대 한 링크를 마우스 오른쪽 단추로 클릭는 합니다. ZIP 파일을 선택 **으로 대상 저장**합니다.

3.  압축 된 패키지를 저장 된와 클릭 로컬 폴더로 이동 **저장**합니다.

    이 프로세스는 패키지의 로컬 복사본을 만듭니다. 

4. 다운로드 오류가 발생 하면 다른 미러 사이트를 시도 합니다.

5. 패키지 보관을 다운로드 한 후 패키지를 설치 하거나 인터넷에 연결 하지 않은 서버에 압축된 된 패키지를 복사 수 있습니다.

> [!TIP]
> 실수로 이진 파일을 다운로드 하는 대신 패키지를 설치 하면 다운로드 된 압축된 파일의 복사본은 컴퓨터에도 저장 됩니다. 파일 위치를 확인할 패키지가 설치 되어 상태 메시지를 감시 합니다. 인터넷에 연결 하지 않은 서버에는 압축 된 파일을 복사할 수 있습니다.
> 
> 그러나이 메서드를 사용 하 여 패키지를 얻을 때 종속성 포함 되지 않습니다. 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>독립 실행형 R 또는 Python 서버-side-by-side 설치

R 및 Python 기능 중 일부는 같은 컴퓨터에 공존할 수 하는 여러 Microsoft 제품에 포함 됩니다.

컴퓨터에 별도 데이터베이스에서 분석 (SQL Server 2017 컴퓨터 학습 서비스 및 SQL Server 2016 R Services) 외에도 SQL Server 2017 Microsoft 컴퓨터 학습 서버 (독립 실행형) 또는 SQL Server 2016 R 서버 (독립 실행형)를 설치한 경우 중복 항목을 모든 R 도구 및 라이브러리의 각 항목에 대해 R 설치입니다.

R_SERVER 라이브러리에 설치 된 패키지는 독립 실행형 서버 에서만 사용 되 고 (In-database) SQL Server 인스턴스를 통해 액세스할 수 없습니다. 항상 사용 하는 `R_SERVICES` 라이브러리 데이터베이스에서 SQL Server를 사용 하려는 패키지를 설치할 때. 경로 대 한 자세한 내용은 참조 [패키지 라이브러리 위치](installing-and-managing-r-packages.md#package-library-location)합니다.


## <a name="see-also"></a>참고자료

+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [자습서, 샘플, 솔루션](../tutorials/machine-learning-services-tutorials.md)