---
title: SQLRUserGroup-SQL Server Machine Learning Services에 대 한 로그인 만들기
description: 묵시적된 인증을 사용 하 여 루프백 연결에 대 한 로그인을 만들기 SQL Server에서 SQLRUserGroup에 대 한 작업자 계정 id 변환 다시 호출 사용자에 게는 서버에 로그인 할 수 있도록 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 7dafb4c9edfe830a354da61b72d330d800349781
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962354"
---
# <a name="create-a-login-for-sqlrusergroup"></a>SQLRUserGroup에 대한 로그인 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

만들기를 [SQL Server 로그인](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login) 에 대 한 [SQLRUserGroup](../concepts/security.md#sqlrusergroup) 때를 [루프백 연결 루프](../../advanced-analytics/concepts/security.md#implied-authentication) 스크립트에서 지정을 *트러스트 된 연결*, 코드를 포함 하는 개체를 실행 하는 데 id 및 Windows 사용자 계정입니다.

연결 되는 것을 신뢰할 수 있는 `Trusted_Connection=True` 연결 문자열에 있습니다. SQL Server가 트러스트 된 연결을 지정 하는 요청을 받으면 현재 Windows 사용자의 id를 로그인에 있는지 여부를 확인 합니다. 작업자 계정으로 실행 하는 외부 프로세스에 대 한 (에서 MSSQLSERVER01 등 **SQLRUserGroup**), 이러한 계정을 기본적으로 로그인 하지 않으므로 요청이 실패 합니다.

에 대 한 로그인을 만들어 연결 오류를 해결할 수 있습니다 **SQLServerRUserGroup**합니다. Id 및 외부 프로세스에 대 한 자세한 내용은 참조 하세요. [확장성 프레임 워크에 대 한 보안 개요](../concepts/security.md)합니다.

> [!Note]
> 했는지 **SQLRUserGroup** "로컬 로그온 허용" 권한이 있습니다. 기본적으로이 권한은 모든 새 로컬 사용자에 게 제공 됩니다 되지만 일부 조직에서는 더 엄격한 그룹 정책이이 권한을 사용 하지 않도록 설정할 수 있습니다.

## <a name="create-a-login"></a>로그인을 만듭니다.

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **보안**을 확장하고 **로그인**을 마우스 오른쪽 단추로 클릭한 다음 **새 로그인**을 선택합니다.

2. 에 **로그인-신규** 대화 상자에서 **검색**합니다. (입력 하지 않습니다 모든 상자에 아직.)
    
     ![Machine learning 위한 새 로그인을 추가 하려면 검색을 누릅니다](media/implied-auth-login1.png "검색 machine learning 위한 새 로그인 추가 클릭 합니다.")

3. 에 **사용자 또는 그룹 선택** 상자를 **개체 유형** 단추.

     ![Machine learning 위한 새 로그인을 추가할 개체 유형을 검색](media/implied-auth-login2.png "machine learning 위한 새 로그인을 추가할 개체 형식 검색")

4. 에 **개체 유형** 대화 상자에서 **그룹**합니다. 다른 모든 확인란의 선택을 취소 합니다.

     ![개체 유형 대화 상자에서 그룹을 선택](media/implied-auth-login3.png "개체 유형 대화 상자에서 그룹 선택")

4. 클릭 **Advanced**를 클릭 한 다음 확인 하 고 현재 컴퓨터를 검색할 위치 인지 확인 **지금 찾기**합니다.

     ![그룹의 목록을 가져오려면 지금 찾기를 클릭](media/implied-auth-login4.png "클릭 지금 찾기 그룹 목록을 가져오려면")

5. 그룹 계정 하나부터 찾을 때까지 서버에서 목록 스크롤하여 `SQLRUserGroup`합니다.
    
    + 에 대 한 실행 패드 서비스와 연결 된 그룹의 이름을 합니다 _기본 인스턴스_ 은 항상 **SQLRUserGroup**R 또는 Python 설치 여부에 관계 없이 합니다. 기본 인스턴스를 사용할 경우에이 계정을 선택 합니다.
    + 사용 중인 경우는 _명명 된 인스턴스로_, 기본 작업자 그룹 이름에 인스턴스 이름이 추가 됩니다 `SQLRUserGroup`합니다. 예를 들어 인스턴스 이름이 "MLTEST" 인 경우이 인스턴스에 대 한 기본 사용자 그룹 이름을 것 **SQLRUserGroupMLTest**합니다.
 
    ![서버에서 그룹의 예](media/implied-auth-login5.png "서버의 그룹의 예")
   
5. 클릭 **확인** 고급 검색 대화 상자를 닫습니다.

    > [!IMPORTANT]
    > 인스턴스에 대 한 올바른 계정을 선택 해야 합니다. 각 인스턴스는 자체 실행 패드 서비스에만 및 해당 서비스에 대해 만든 그룹에 사용할 수 있습니다. 인스턴스는 실행 패드 서비스 또는 작업자 계정을 공유할 수 없습니다.

6. 클릭 **확인** 한 번 더 클릭 하 여 닫습니다 합니다 **사용자 또는 그룹 선택** 대화 상자.

7. 에 **로그인-신규** 대화 상자, 클릭 **확인**합니다. 기본적으로 로그인은 **public** 역할에 할당되며 데이터베이스 엔진에 연결할 수 있는 권한이 있습니다.

## <a name="next-steps"></a>다음 단계

+ [보안 개요](../concepts/security.md)
+ [확장성 프레임 워크](../concepts/extensibility-framework.md)
