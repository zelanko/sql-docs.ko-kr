---
title: 데이터베이스 사용자 (SQL Server 기계 학습)로 SQLRUserGroup 추가 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6f0877f04b35475dd4d1403390447adad0c3936c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203135"
---
# <a name="add-sqlrusergroup-as-a-database-user"></a>SQLRUserGroup 데이터베이스 사용자로 추가
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 여러 작업자 계정 SQL Server의 컴퓨터 학습 서비스에서 사용 하는 데이터베이스에 연결 하 고 사용자 대신 Python 또는 R 작업을 실행 하는 데 필요한 사용 권한을 부여 하는 방법에 설명 합니다.

## <a name="what-is-sqlrusergroup"></a>SQLRUserGroup 란?

설치 동안 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] 또는 [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)], R의 실행을 지원 하기 위해 새로운 Windows 사용자 계정을 만드는 또는 Python 스크립트 작업의 보안 토큰에서는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스입니다.

이러한 계정은 Windows 사용자 그룹에 볼 수 있습니다 **SQLRUserGroup**합니다. 기본적으로 기계 학습을 실행 하기 위한 충분 한 더 많은 작업은 일반적으로 20 작업자 계정이 생성 됩니다.

기계 학습 외부 클라이언트에서 스크립트를 보낼 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 가능한 작업자 계정을 활성화 하 고 호출 하는 사용자의 id로 매핑합니다 사용자를 대신 하 여 스크립트를 실행 합니다. 데이터베이스 엔진의이 새로운 서비스 보안 이라는 외부 스크립트 실행을 지원 *암시 된 인증이*합니다.

그러나 원격 데이터 과학자의 클라이언트에서 Python 또는 R 스크립트를 실행 해야 하는 경우 Windows 인증을 사용 하는 권한을 부여 해야 이러한 작업자 계정에 로그인 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 대신 인스턴스.

## <a name="add-sqlrusergroup-as-a-sql-server-login"></a>SQLRUserGroup를 SQL Server 로그인으로 추가

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **보안**을 확장하고 **로그인**을 마우스 오른쪽 단추로 클릭한 다음 **새 로그인**을 선택합니다.

2. 에 **로그인-신규** 대화 상자에서 **검색**합니다. (입력 하지 않은 아무 것도 상자에서 아직.)
    
     ![기계 학습에 대 한 새 로그인 추가 검색 클릭](media/implied-auth-login1.png "검색 기계 학습에 대 한 새 로그인 추가 클릭 합니다.")

3. **사용자 또는 그룹 선택** 상자는 **개체 유형** 단추입니다.

     ![기계 학습에 대 한 새 로그인을 추가 하려면 개체 유형 검색](media/implied-auth-login2.png "기계 학습에 대 한 새 로그인을 추가 하려면 개체 유형 검색")

4. 에 **개체 유형** 대화 상자에서 **그룹**합니다. 다른 모든 확인란의 선택을 취소 합니다.

     ![개체 유형 대화 상자에서 그룹을 선택](media/implied-auth-login3.png "개체 유형 대화 상자에서 그룹 선택")

4. 클릭 **고급**를 확인 합니다.를 검색할 위치는 현재 컴퓨터를 클릭 한 다음 **지금 찾기**합니다.

     ![그룹의 목록을 가져오려면 지금 찾기를 클릭](media/implied-auth-login4.png "클릭 지금 찾기 그룹 목록 가져오기")

5. 부터는 하나를 찾을 때까지 서버에서 그룹 계정 목록 스크롤하여 `SQLRUserGroup`합니다.
    
    + 에 대 한 실행 패드 서비스와 관련 된 그룹의 이름에서 _기본 인스턴스_ 항상 **SQLRUserGroup**R, Python 또는 둘 다 설치 여부에 관계 없이 합니다. 기본 인스턴스용이 계정을 선택 합니다.
    + 사용 하는 경우는 _명명 된 인스턴스_, 인스턴스 이름이 기본 작업자 그룹 이름의 이름에 추가 됩니다 `SQLRUserGroup`합니다. 따라서 인스턴스 이름이 "MLTEST" 이면이 인스턴스에 대 한 기본 사용자 그룹 이름을 것 **SQLRUserGroupMLTest**합니다.
 
     ![서버의 그룹에 대 한 예제](media/implied-auth-login5.png "서버의 그룹 예제")
   
5. 클릭 **확인** 고급 검색 대화 상자를 닫습니다.

    > [!IMPORTANT]
    > 인스턴스에 대 한 올바른 계정을 선택 해야 합니다. 각 인스턴스는 자체 실행 패드 서비스와 해당 서비스에 대해 생성 된 그룹에 사용할 수 있습니다. 인스턴스는 실행 패드 서비스 또는 작업자 계정을 공유할 수 없습니다.

6. 클릭 **확인** 를 한 번 더 닫습니다는 **사용자 또는 그룹 선택** 대화 상자.

7. 에 **로그인-신규** 대화 상자를 클릭 **확인**합니다. 기본적으로 로그인은 **public** 역할에 할당되며 데이터베이스 엔진에 연결할 수 있는 권한이 있습니다.

## <a name="change-the-number-of-worker-accounts-in-sqlrusergroup"></a>SQLRUserGroup의 작업자 계정 수를 변경 합니다.

기계 학습의 집중적으로 사용 하려는 경우에이 문서에 설명 된 대로 외부 스크립트를 실행 하는 데 사용 되는 계정의 수를 늘릴 수 있습니다. 

+ [기계 학습에 대 한 사용자 계정 풀 수정](modify-the-user-account-pool-for-sql-server-r-services.md)

기본적으로 20 동시 세션을 지 원하는 20 계정은 생성 됩니다. 병렬된 작업 추가 계정을 사용 하지 않습니다. 예를 들어 사용자가 병렬 처리를 사용 하는 점수 매기기 작업을 실행 하는 경우 동일한 작업자 계정은 다시 사용 되 모든 스레드에 대 한 합니다.
