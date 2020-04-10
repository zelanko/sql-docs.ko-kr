---
title: SQLRUserGroup에 대한 로그인 만들기
description: 암시적 인증을 사용하는 루프백 연결의 경우 SQLRUserGroup에 대한 SQL Server 로그인을 만듭니다. 이렇게 하면 작업자 계정은 ID를 호출 사용자로 다시 변환하기 위해 서버에 로그인할 수 있습니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c57a62e954ae8cb0fc52c9a5ead22d418243c0b8
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117126"
---
# <a name="create-a-login-for-sqlrusergroup"></a>SQLRUserGroup에 대한 로그인 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

스크립트의 [루프백 연결](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login)이 [신뢰할 수 있는 연결](../concepts/security.md#sqlrusergroup)을 지정하고 코드를 포함하는 개체를 실행하는 데 사용되는 ID가 Windows 사용자 계정인 경우 [SQLRUserGroup](../../machine-learning/concepts/security.md#implied-authentication)에 대한 *SQL Server 로그인*을 만듭니다.

신뢰할 수 있는 연결은 연결 문자열에 `Trusted_Connection=True`가 있는 연결입니다. SQL Server에서 신뢰할 수 있는 연결을 지정하는 요청을 수신하는 경우 현재 Windows 사용자의 ID에 로그인이 있는지 여부를 확인합니다. 작업자 계정으로 실행되는 외부 프로세스(예: **SQLRUserGroup**의 MSSQLSERVER01)의 경우 해당 계정에는 기본적으로 로그인이 없기 때문에 요청이 실패합니다.

**SQLServerRUserGroup**에 대한 로그인을 만들어 연결 오류를 해결할 수 있습니다. ID 및 외부 프로세스에 대한 자세한 내용은 [확장성 프레임워크에 대한 보안 개요](../concepts/security.md)를 참조하세요.

> [!Note]
> **SQLRUserGroup**에 "로컬 로그온 허용" 권한이 있는지 확인합니다. 기본적으로 이 권한은 모든 새 로컬 사용자에게 제공되지만 일부 조직에서는 그룹 정책이 좀 더 엄격하므로 이 권한을 사용하지 못할 수도 있습니다.

## <a name="create-a-login"></a>로그인을 만듭니다.

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **보안**을 확장하고 **로그인**을 마우스 오른쪽 단추로 클릭한 다음 **새 로그인**을 선택합니다.

2. **로그인 - 새로 만들기** 대화 상자에서 **검색**을 선택합니다. (상자에 아직 아무 것도 입력하지 마세요.)
    
     ![검색을 클릭하여 새로운 기계 학습 로그인 추가](media/implied-auth-login1.png "검색을 클릭하여 새로운 기계 학습 로그인 추가")

3. **사용자 또는 그룹 선택** 상자에서 **개체 유형** 단추를 클릭합니다.

     ![개체 형식을 검색하여 새로운 기계 학습 로그인 추가](media/implied-auth-login2.png "개체 형식을 검색하여 새로운 기계 학습 로그인 추가")

4. **개체 유형** 대화 상자에서 **그룹**을 선택합니다. 다른 모든 확인란의 선택을 취소합니다.

     ![개체 형식 대화 상자에서 그룹 선택](media/implied-auth-login3.png "개체 형식 대화 상자에서 그룹 선택")

4. **고급**을 클릭하고 검색할 위치가 현재 컴퓨터인지 확인한 다음, **지금 찾기**를 클릭합니다.

     ![지금 찾기를 클릭하여 그룹 목록 가져오기](media/implied-auth-login4.png "지금 찾기를 클릭하여 그룹 목록 가져오기")

5. `SQLRUserGroup`으로 시작하는 항목을 찾을 때까지 서버의 그룹 계정 목록을 스크롤합니다.
    
    + _기본 인스턴스_에 대한 실행 패드 서비스와 연결된 그룹의 이름은 R과 Python 중 어떤 언어를 설치했는지에 관계없이 항상 **SQLRUserGroup**입니다. 기본 인스턴스의 경우에만 이 계정을 선택합니다.
    + _명명된 인스턴스_를 사용하는 경우 기본 작업자 그룹 이름 `SQLRUserGroup`에 인스턴스 이름이 추가됩니다. 예를 들어, 인스턴스의 이름이 "MLTEST"인 경우 이 인스턴스의 기본 사용자 그룹 이름은 **SQLRUserGroupMLTest**가 됩니다.
 
    ![서버에 있는 그룹의 예](media/implied-auth-login5.png "서버에 있는 그룹의 예")
   
5. **확인**을 클릭하여 고급 검색 대화 상자를 닫습니다.

    > [!IMPORTANT]
    > 인스턴스에 대해 올바른 계정을 선택했는지 확인합니다. 각 인스턴스는 자체 실행 패드 서비스와 해당 서비스에 대해 생성된 그룹만 사용할 수 있습니다. 인스턴스는 실행 패드 서비스 또는 작업자 계정을 공유할 수 없습니다.

6. **확인**을 한 번 더 클릭하여 **사용자 또는 그룹 선택** 대화 상자를 닫습니다.

7. **로그인 - 새로 만들기** 대화 상자에서 **확인**을 클릭합니다. 기본적으로 로그인은 **public** 역할에 할당되며 데이터베이스 엔진에 연결할 수 있는 권한이 있습니다.

## <a name="next-steps"></a>다음 단계

+ [보안 개요](../concepts/security.md)
+ [확장성 프레임워크](../concepts/extensibility-framework.md)
