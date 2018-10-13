---
title: SQLRUserGroup을 데이터베이스 사용자 (SQL Server Machine Learning)로 추가 | Microsoft Docs
description: SQL Server Machine Learning Services에 대 한 SQLRUserGroup을 데이터베이스 사용자로 추가 하는 방법.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: fc5294453def64d13cc43a74a8a5fb299c3e23e3
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100324"
---
# <a name="add-sqlrusergroup-as-a-database-user"></a>SQLRUserGroup을 데이터베이스 사용자로 추가
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

에 대 한 데이터베이스 로그인을 만들고 합니다 [SQLRUserGroup](../concepts/security.md#sqlrusergroup) 대상이 데이터 또는 SQL Server 인스턴스에 대해 작업 하는 경우 R 및 Python 스크립트에서 발생 하는 신뢰할 수 있는 연결을 허용 하도록 합니다. 

SQL Server 로그인을 사용 하 여 연결 문자열 또는 완전히 지정 된 사용자 이름 및 암호를 포함 하는 스크립트에 대 한 로그인을 만들 필요 하지 않습니다.

## <a name="when-a-login-is-required"></a>로그인이 필요한 경우

R 또는 Python 스크립트에는 트러스트 된 연결을 지정 하는 연결 문자열을 포함 하는 경우 (예를 들어, "Trusted_Connection = True"), 추가 구성은 SQL Server에 올바른 사용자 id 위해 필요 합니다. 외부 프로세스에서 실행 되는 **SQLRUserGroup** MSSQLSERVER01, 신뢰할 수 있는 사용자 같은 작업자 계정이 작업자 id로 표시 됩니다. 이 id에 SQL Server에 로그인 권한이 없음을, 때문에 신뢰할 수 있는 추가 하지 않는 한 연결은 실패 **SQLRUserGroup** 데이터베이스 사용자로 합니다. 자세한 내용은 [ *묵시적된 인증*](../../advanced-analytics/concepts/security.md#implied-authentication)합니다.

실행 패드에서 스크립트 및 프로세스를 실행 하는 작업자 계정 호출 원래 사용자의 매핑을 유지 하는 것을 기억 하십시오. 작업자 계정에 대 한 신뢰할 수 있는 연결에 성공 하면 원래 호출 하는 사용자의 id는 및 데이터를 검색 하는 데 사용 됩니다. Db_datareader 권한을 부여할 필요가 없습니다 **SQLRUserGroup**합니다.

> [!Note]
>  했는지 **SQLRUserGroup** "로컬 로그온 허용" 권한이 있습니다. 기본적으로이 권한은 모든 새 로컬 사용자에 게 제공 됩니다 되지만 일부 조직에서는 더 엄격한 그룹 정책이 적용 될 수 있습니다.

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
    + 사용 중인 경우는 _명명 된 인스턴스로_, 기본 작업자 그룹 이름에 인스턴스 이름이 추가 됩니다 `SQLRUserGroup`합니다. 따라서 인스턴스 이름이 "MLTEST" 인 경우이 인스턴스에 대 한 기본 사용자 그룹 이름을 것 **SQLRUserGroupMLTest**합니다.
 
     ![서버에서 그룹의 예](media/implied-auth-login5.png "서버의 그룹의 예")
   
5. 클릭 **확인** 고급 검색 대화 상자를 닫습니다.

    > [!IMPORTANT]
    > 인스턴스에 대 한 올바른 계정을 선택 해야 합니다. 각 인스턴스는 자체 실행 패드 서비스에만 및 해당 서비스에 대해 만든 그룹에 사용할 수 있습니다. 인스턴스는 실행 패드 서비스 또는 작업자 계정을 공유할 수 없습니다.

6. 클릭 **확인** 한 번 더 클릭 하 여 닫습니다 합니다 **사용자 또는 그룹 선택** 대화 상자.

7. 에 **로그인-신규** 대화 상자, 클릭 **확인**합니다. 기본적으로 로그인은 **public** 역할에 할당되며 데이터베이스 엔진에 연결할 수 있는 권한이 있습니다.