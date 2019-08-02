---
title: SQLRUserGroup에 대한 로그인 만들기
description: 묵시적 인증을 사용 하는 루프백 연결의 경우 SQLRUserGroup에 대 한 SQL Server 로그인을 만듭니다. 이렇게 하면 작업자 계정이 서버에 로그인 하 여 호출 하는 사용자에 게 다시 id를 변환할 수 있습니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a5194f251b7ea47e0d9485446b8957e96037ded0
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714967"
---
# <a name="create-a-login-for-sqlrusergroup"></a>SQLRUserGroup에 대한 로그인 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

스크립트의 루프백 [연결](../../advanced-analytics/concepts/security.md#implied-authentication) 에서 *트러스트 된 연결*을 지정 하 고 개체를 실행 하는 데 사용 되는 id에 Windows 사용자 계정인 [SQLRUserGroup](../concepts/security.md#sqlrusergroup) 에 대 한 [SQL Server 로그인](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login) 을 만듭니다.

연결 문자열 `Trusted_Connection=True` 에는 트러스트 된 연결이 있습니다. SQL Server에서 트러스트 된 연결을 지정 하는 요청을 수신 하는 경우 현재 Windows 사용자의 id가 로그인을 갖고 있는지 여부를 확인 합니다. 작업자 계정으로 실행 되는 외부 프로세스 (예: **SQLRUserGroup**의 MSSQLSERVER01)의 경우 해당 계정에는 기본적으로 로그인이 없기 때문에 요청이 실패 합니다.

**SQLServerRUserGroup**에 대 한 로그인을 만들어 연결 오류를 해결할 수 있습니다. Id 및 외부 프로세스에 대 한 자세한 내용은 [확장성 프레임 워크의 보안 개요](../concepts/security.md)를 참조 하세요.

> [!Note]
> **SQLRUserGroup** 에 "로컬 로그온 허용" 권한이 있는지 확인 합니다. 기본적으로이 권한은 모든 새 로컬 사용자에 게 제공 되지만 일부 조직에서는 그룹 정책을 보다 엄격 하 게 사용 하지 못할 수도 있습니다.

## <a name="create-a-login"></a>로그인을 만듭니다.

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **보안**을 확장하고 **로그인**을 마우스 오른쪽 단추로 클릭한 다음 **새 로그인**을 선택합니다.

2. **로그인-새로 만들기** 대화 상자에서 **검색**을 선택 합니다. (상자에 아무것도 입력 하지 마세요.)
    
     ![검색을 클릭 하 여 machine learning에 대 한 새 로그인을 추가 합니다] . (media/implied-auth-login1.png "검색을 클릭 하 여 machine learning에 대 한 새 로그인을 추가 합니다") .

3. **사용자 또는 그룹 선택** 상자에서 **개체 유형** 단추를 클릭 합니다.

     ![Machine learning에 대 한 새 로그인을 추가 하는 개체 유형 검색](media/implied-auth-login2.png "Machine learning에 대 한 새 로그인을 추가 하는 개체 유형 검색")

4. **개체 유형** 대화 상자에서 **그룹**을 선택 합니다. 다른 모든 확인란의 선택을 취소 합니다.

     ![개체 유형 대화 상자에서 그룹 선택](media/implied-auth-login3.png "개체 유형 대화 상자에서 그룹 선택")

4. **고급**을 클릭 하 고 검색할 위치가 현재 컴퓨터 인지 확인 한 다음 **지금 찾기**를 클릭 합니다.

     ![지금 찾기를 클릭 하 여 그룹 목록을 가져옵니다] . (media/implied-auth-login4.png "지금 찾기를 클릭 하 여 그룹 목록을 가져옵니다") .

5. 로 `SQLRUserGroup`시작 하는 항목을 찾을 때까지 서버의 그룹 계정 목록을 스크롤합니다.
    
    + _기본 인스턴스에_ 대 한 실행 패드 서비스와 연결 된 그룹의 이름은 R 또는 Python을 설치 했는지 아니면 둘 다에 설치 했는지에 관계 없이 항상 **SQLRUserGroup**입니다. 기본 인스턴스에만이 계정을 선택 합니다.
    + _명명 된 인스턴스_를 사용 하는 경우 인스턴스 이름은 기본 작업자 그룹 이름 `SQLRUserGroup`의 이름에 추가 됩니다. 예를 들어 인스턴스의 이름이 "MLTEST" 인 경우이 인스턴스의 기본 사용자 그룹 이름은 **Sqlrusergroupmltest**입니다.
 
    ![서버에 있는 그룹의 예](media/implied-auth-login5.png "서버에 있는 그룹의 예")
   
5. **확인** 을 클릭 하 여 고급 검색 대화 상자를 닫습니다.

    > [!IMPORTANT]
    > 인스턴스에 대해 올바른 계정을 선택 해야 합니다. 각 인스턴스는 자체 실행 패드 서비스와 해당 서비스에 대해 생성 된 그룹을 사용할 수 있습니다. 인스턴스는 실행 패드 서비스 또는 작업자 계정을 공유할 수 없습니다.

6. **확인** 을 한 번 더 클릭 하 여 **사용자 또는 그룹 선택** 대화 상자를 닫습니다.

7. **로그인-새로 만들기** 대화 상자에서 **확인**을 클릭 합니다. 기본적으로 로그인은 **public** 역할에 할당되며 데이터베이스 엔진에 연결할 수 있는 권한이 있습니다.

## <a name="next-steps"></a>다음 단계

+ [보안 개요](../concepts/security.md)
+ [확장성 프레임 워크](../concepts/extensibility-framework.md)
