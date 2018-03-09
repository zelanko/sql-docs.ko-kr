---
title: "설치 하 고 SQL Server의 컴퓨터 학습 패키지 관리 | Microsoft Docs"
ms.custom: 
ms.date: 02/19/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 0fd96240581203d9f948372dfbe98cac80a3b906
ms.sourcegitcommit: c08d665754f274e6a85bb385adf135c9eec702eb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2018
---
# <a name="installing-and-managing-machine-learning-packages-in-sql-server"></a>설치 하 고 SQL Server의 컴퓨터 학습 패키지 관리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server 2016 및 SQL Server 2017에 새 R, Python 패키지를 설치할 수 방법을 설명 합니다. 또한 제한 SQL Server에 설치할 수 있는 패키지에 설명 합니다.

## <a name="overview-of-package-management-methods-and-requirements"></a>패키지 관리 방법 및 요구 사항 개요

일반적인 R, Python 개발 달리 SQL Server에서 사용 되는 패키지 관리 제어 아래의 폴더에 설치 되어야 합니다. 단일 위치에 패키지를 최소화 하기 위해서는 많은 이점이 있습니다.

+ 서버 관리자 추가 된 새 파일 및 라이브러리 서버에서를 모니터링 하 고 패키지 라이브러리에서 사용 되는 파일의 증가 제어할 수 있습니다. 
+ 사용자 라이브러리에는 동일한 패키지의 여러 복사본을 설치 하는 대신 여러 데이터베이스 사용자가 패키지를 보다 쉽게 공유할 수 있습니다.
+ 서버 및 해당 작업을 보호 하기 위해 안전 하 고 승인 된 패키지에만 설치할 수 있습니다.

그러나 이러한 제한 사항은 반드시 데이터 과학자와 분석가가 작동 하는 방법의 일부 변경을 의미 합니다.

+ 일반적으로 서버에 대 한 관리 액세스는 필요 합니다. SQL Server 2017 년 1 데이터베이스 관리자가 사용자에 게 특정 개인 사용에 대 한 패키지를 설치 하는 기능 역할을 사용할 수 있지만 관리자는 여전히이 기능을 설정 하는 합니다.
+ 여러 서버에 인터넷 액세스를 않아도 됩니다. 이러한 컴퓨터에 패키지를 설치 하려면 몇 가지 추가 준비 합니다.
+ 패키지는 인스턴스 라이브러리에 설치 됩니다. 패키지는 인스턴스 간에 공유할 수 없습니다.
+ 사용자가 사용자 라이브러리에 설치 된 모든 패키지를 실행할 수 없습니다.

## <a name="package-installation-guides-for-r-or-python"></a>R 또는 Python에 대 한 패키지 설치 가이드

새 Python 또는 R 패키지를 설치 하는 방법에 자세한 내용은 다음 문서를 참조 하십시오. 

### <a name="install-new-r-packages"></a>새 R 패키지 설치

+ [SQL Server에 추가 R 패키지를 설치 합니다.](install-additional-r-packages-on-sql-server.md)

    R 도구를 사용 하 여 관리자 권한으로 SQL Server 2016 또는 2017에서 R 패키지를 설치할 수 있습니다.

    R 원격 클라이언트에서 R 패키지를 설치할 수도 있습니다를 R Server 9.0.2 이상이 설치 되어 있습니다.

    DDL 문을 사용 하 여 SQL Server 2017에서 R 패키지를 설치할 수도 있습니다.

### <a name="install-new-python-packages"></a>새 Python 패키지 설치

+ [SQL Server에 새로운 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)

## <a name="prerequisites"></a>필수 구성 요소

다운로드 하거나 모든 새 패키지를 설치 하려고 하기 전에 요구 사항을 검토 합니다.

+ 패키지의 Windows 버전 인지 확인: [올바른 패키지 버전 및 형식 가져오기](#packageVersion)

+ 모든 패키지 종속 파일을 식별 하 고 SQL Server 환경와의 호환성을 확인 합니다.

+ R 버전 또는 Python 버전 호환성을 확인 합니다. 패키지는 SQL Server에서 실행 되는 Python 또는 R의 버전과 호환 되어야 합니다.

+ 사용 권한입니다. 패키지를 설치 하는 권한이 설정 되어 있는지 확인 합니다. 인스턴스 라이브러리를 설치 하려면 SQL Server를 실행 하는 컴퓨터에 대 한 액세스를 관리 해야 합니다. SQL Server 컴퓨터에 관리자 권한이 없으면 데이터베이스 관리자를를 패키지 설치에 대 한 도움말을 찾습니다.

    SQL Server 2017 년 1 서버에 패키지 관리를 활성화 한 경우 데이터베이스 소유자 또는 패키지 관리 역할의 멤버 있는 R 패키지 원격 클라이언트에서 설치할 수 있습니다.

+ SQL Server 환경에 설치 하는 특정 패키지의 이점과 위험을 고려 합니다. 패키지 (또는 필요한 모든 패키지)을 SQL Server에서 또는 정책에 의해 차단 될 수 있는 기능이 포함 되어 있는지 여부를 확인 합니다. 여러 R 및 Python 패키지는 강화 된 SQL Server 환경에 대 한 매우 불량 적합 합니다. 다음과 같은 문제가 발생할 수 있습니다.

    - 네트워크에 액세스 하는 패키지
    - Java 또는 SQL Server 환경에서 사용 하지 일반적으로 다른 프레임 워크를 필요로 하는 패키지
    - 승격 된 파일 시스템 액세스를 필요로 하는 패키지
    - 패키지 웹 개발 또는 SQL Server 내에서 실행 하 여 장점이 없는 다른 작업에 사용 됩니다.

## <a name="installation-on-servers-with-no-internet-access"></a>인터넷에 연결 된 서버에 설치

일반적으로 프로덕션 데이터베이스를 호스팅하는 서버는 인터넷 연결을 허용 하지 않습니다. 이러한 환경에서는 새 Python 또는 R 패키지를 설치 하려면 모든 패키지 및 패키지의 종속성을 사전에 준비할 설치에서 사용 하기 위해 서버에 있는 폴더에 파일을 복사 하 필요 합니다.

1. 모든 패키지 종속 파일을 식별 합니다. 
2. 필요한 패키지는 서버에 이미 설치 되어 있는지 확인 합니다. 패키지가 설치 되어 있는 경우 버전이 올바른지 확인 합니다.
3. 별도 컴퓨터에 패키지 및 모든 종속성을 다운로드 합니다.
4. 서버에서 액세스할 수 있는 폴더에 파일을 이동 합니다.
5. 인스턴스 라이브러리에 패키지를 설치 하려면 지원 되는 설치 명령이 나 DDL 문을 실행 합니다.

모든 종속성을 식별 하기가 복잡할 수 있습니다. R을 사용 하는 권장 [miniCRAN](create-a-local-package-repository-using-minicran.md) 오프 라인 패키지 리포지토리를 준비 합니다.

Python에 대 한 모든 종속성을 준비 하 고 로컬에 저장할 유사 해야 합니다. Windows 호환 이진 파일을 사용 하 고 WHL 형식을 사용 해야 합니다.
