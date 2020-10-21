---
title: Active Directory 모드로 배포 - 필수 조건
titleSuffix: SQL Server Big Data Cluster
description: SQL Server 빅 데이터 클러스터에 대해 Active Directory 구성
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6c25038680d71257e609d99460841d63b8e87d33
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91898714"
---
# <a name="deploy-big-data-clusters-2019-in-active-directory-mode-prerequisites"></a>Active Directory 모드로 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포: 필수 구성 요소

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 Active Directory 인증 모드로 SQL Server BDC(빅 데이터 클러스터)를 배포하기 위해 준비하는 방법을 설명합니다. 클러스터는 인증을 위해 기존 AD 도메인을 사용합니다.

>[!Note]
>SQL Server 2019 CU5 릴리스 전까지는 빅 데이터 클러스터에 하나의 Active Directory 도메인에 하나의 클러스터만 배포될 수 있도록 하는 제한이 있었습니다. 이 제한은 CU5 릴리스부터 제거되었습니다. 새로운 기능에 대한 자세한 내용은 [개념: Active Directory 모드에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포](active-directory-deployment-background.md)를 참조하세요. 이 문서의 예는 두 가지 배포 사용 사례를 모두 수용하도록 수정되었습니다.

## <a name="background"></a>배경

AD(Active Directory) 인증을 사용하도록 설정하려면 BDC에서 클러스터의 다양한 서비스에 필요한 사용자, 그룹, 머신 계정 및 SPN(서비스 사용자 이름)을 자동으로 만듭니다. 이러한 계정을 일부 포함하고 범위 지정 권한을 허용하려면 클러스터를 배포하기 전에 OU(조직 구성 단위)를 만드는 것이 좋습니다. 모든 BDC 관련 AD 개체는 배포 중에 생성됩니다. 

## <a name="pre-requisites"></a>필수 구성 요소

### <a name="organizational-unit-ou"></a>OU(조직 구성 단위)
OU(조직 구성 단위)는 사용자, 그룹 및 기타 OU를 배치할 수 있는 Active Directory 내 하위 단위입니다. 큰 그림 OU는 조직의 기능 또는 비즈니스 구조를 미러링하는 데 사용할 수 있습니다. 이 문서에서는 예시로 `bdc`라는 OU를 만듭니다. 

>[!NOTE]
>OU(조직 구성 단위)는 관리 경계를 나타내며 고객이 데이터 관리자의 권한 범위를 제어할 수 있도록 합니다. 

[OU 디자인 원칙](/windows-server/identity/ad-ds/plan/reviewing-ou-design-concepts)을 따르면 조직 내에서 OU를 사용하여 작업하는 데 가장 적합한 구조를 결정할 수 있습니다.

### <a name="ad-account-for-bdc-domain-service-account"></a>BDC 도메인 서비스 계정의 AD 계정

Active Directory에 필요한 모든 개체를 자동으로 만들 수 있으려면 BDC에는 제공된 OU(조직 구성 단위) 내에서 사용자, 그룹 및 컴퓨터 계정을 만들 수 있는 특정 권한이 있는 AD 계정이 필요합니다. 이 문서에서 이 AD 계정의 권한을 구성하는 방법을 설명합니다. 이 문서에서는 예시로 `bdcDSA`라는 AD 계정을 사용합니다.

### <a name="auto-generated-active-directory-objects"></a>자동 생성된 Active Directory 개체
BDC 배포에서 자동으로 계정 및 그룹 이름을 생성합니다. 각 계정은 BDC의 서비스를 나타내며 BDC 클러스터가 사용되는 수명 내내 BDC를 통해 관리됩니다. 이때 계정은 각 서비스에 필요한 SPN(서비스 사용자 이름)을 소유합니다.  관리되는 AD 자동 생성 계정, 그룹 및 서비스의 전체 목록은 [자동 생성된 Active Directory 개체](active-directory-objects.md)를 참조하세요.

>[!IMPORTANT]
>도메인 컨트롤러에 설정된 암호 만료 정책에 따라 이러한 계정의 암호는 만료될 수 있습니다. 기본 만료 정책은 42일입니다. BDC의 모든 계정에 대한 자격 증명을 회전하는 메커니즘은 없으므로 만료 기간이 경과하면 클러스터가 작동하지 않게 됩니다. 이 문제를 해결하려면 도메인 컨트롤러에서 BDC 서비스 계정의 만료 정책을 "암호 사용 기간 제한 없음"으로 업데이트합니다. 이 작업은 만료 이전 또는 이후에 수행할 수 있습니다. 후자의 경우 만료된 암호를 Active Directory가 다시 활성화합니다.
>
>다음 이미지에서는 Active Directory 사용자 및 컴퓨터에서 이 속성을 설정하는 위치를 보여 줍니다.
>
>:::image type="content" source="media/deploy-active-directory/image25.png" alt-text="암호 만료 정책 설정":::

아래 단계에서는 Active Directory 도메인 컨트롤러가 이미 있다고 가정합니다. 도메인 컨트롤러가 없는 경우 도움이 될 수 있는 단계는 이 [가이드](https://social.technet.microsoft.com/wiki/contents/articles/37528.create-and-configure-active-directory-domain-controller-in-azure-windows-server.aspx)에 포함되어 있습니다.

## <a name="create-ad-objects"></a>AD 개체 만들기

AD 통합을 사용하여 BDC를 배포하기 전에 다음 작업을 수행합니다.

1. 모든 BDC 관련 AD 개체가 저장되는 OU(조직 구성 단위)를 만듭니다. 또는 배포 시에 기존 OU를 선택할 수도 있습니다.
1. BDC에 대한 AD 계정을 만들거나, 기존 BDC AD 계정을 사용하여 제공된 OU 내에서 올바른 권한을 이 계정에 제공합니다.

### <a name="create-a-user-in-ad-for-bdc-domain-service-account"></a>AD에서 BDC 도메인 서비스 계정에 대한 사용자 만들기

빅 데이터 클러스터에는 특정 권한이 있는 계정이 필요합니다. 계속하기 전에 기존 AD 계정이 있는지 확인하거나 빅 데이터 클러스터에서 필요한 개체를 설정하는 데 사용할 수 있는 새 계정을 만들어야 합니다.

AD에서 새 사용자를 만들려면 마우스 오른쪽 단추로 도메인 또는 OU를 클릭하고, **새로 만들기** > **사용자**를 차례로 선택하면 됩니다.

![Active Directory 사용자 대화 상자](./media/deploy-active-directory/image12.png)

이 문서에서는 이 사용자를 *BDC 도메인 서비스 계정*이라고 합니다.

### <a name="create-an-ou"></a>OU 만들기

도메인 컨트롤러에서 **Active Directory 사용자 및 컴퓨터**를 엽니다. 왼쪽 패널에서 마우스 오른쪽 단추로 OU를 만들려는 디렉터리를 클릭하고, **새로 만들기** \> **조직 구성 단위**를 차례로 선택한 다음, 마법사의 안내에 따라 OU를 만듭니다. 또는 PowerShell을 사용하여 OU를 만들 수 있습니다.

```powershell
New-ADOrganizationalUnit -Name "<name>" -Path "<Distinguished name of the directory you wish to create the OU in>"
```

이 문서의 예에서는 OU 이름으로 `bdc`를 사용합니다.

![Active Directory 조직 구성 단위](./media/deploy-active-directory/image13.png)

![새 개체 - 조직 구성 단위](./media/deploy-active-directory/image14.png)

### <a name="set-permissions-for-an-ad-account"></a>AD 계정에 대한 사용 권한 설정

새 AD 사용자를 만들었는지, 아니면 기존 AD 사용자를 사용하는지에 관계없이 사용자에게 필요한 특정 권한이 있습니다. 이 계정은 BDC 컨트롤러에서 클러스터를 AD에 조인할 때 사용하는 사용자 계정입니다.

BDC DSA(도메인 서비스 계정)는 OU에서 사용자, 그룹 및 컴퓨터 계정을 만들 수 있어야 합니다. 다음 단계에서는 BDC 도메인 서비스 계정의 이름을 `bdcDSA`로 지정했습니다. 이 계정의 이름은 임의로 선택할 수 있습니다.

1. 도메인 컨트롤러에서 **Active Directory 사용자 및 컴퓨터**를 엽니다.

1. 왼쪽 패널에서 도메인, `bdc`에서 사용할 OU로 차례로 이동합니다.

1. 마우스 오른쪽 단추로 OU를 클릭하고 **속성**을 선택합니다.

1. [보안] 탭으로 이동합니다(마우스 오른쪽 단추로 OU를 클릭하고 **보기**를 선택하여 **고급 기능**을 선택했는지 확인).

    ![BDC 개체 속성](./media/deploy-active-directory/image15.png)

1. **추가...** 를 클릭하고 **bdcDSA** 사용자를 추가합니다.

    ![BDC 개체 속성 추가](./media/deploy-active-directory/image16.png)

    ![개체 선택](./media/deploy-active-directory/image17.png)

1. **bdcDSA** 사용자를 선택하고 모든 권한을 지운 다음, **고급**을 클릭합니다.

1. **추가**를 클릭합니다.

    ![추가 클릭](./media/deploy-active-directory/image18.png)

    - **보안 주체 선택**을 클릭하고 **bdcDSA**를 삽입한 다음, 확인을 클릭합니다.

    - **형식**을 **허용**으로 설정합니다.

    - **적용 대상**을 **이 개체 및 모든 하위 개체**로 설정합니다.

        ![속성 허용 설정](./media/deploy-active-directory/image19.png)

    - 아래쪽으로 스크롤하여 **모두 지우기**를 클릭합니다.

    - 위쪽으로 다시 스크롤하여 다음을 선택합니다.
       - **모든 속성 읽기**
       - **모든 속성 쓰기**
       - **컴퓨터 개체 만들기**
       - **컴퓨터 개체 삭제**
       - **그룹 개체 만들기**
       - **그룹 개체 삭제**
       - **사용자 개체 만들기**
       - **사용자 개체 삭제**

    - **확인**을 클릭합니다.

- **추가**를 클릭합니다.

    - **보안 주체 선택**을 클릭하고 **bdcDSA**를 삽입한 다음, 확인을 클릭합니다.

    - **형식**을 **허용**으로 설정합니다.

    - **적용 대상**을 **하위 컴퓨터 개체**로 설정합니다.

    - 아래쪽으로 스크롤하여 **모두 지우기**를 클릭합니다.

    - 위쪽으로 다시 스크롤하여 **암호 재설정**을 선택합니다.

    - **확인**을 클릭합니다.

- **추가**를 클릭합니다.

    - **보안 주체 선택**을 클릭하고 **bdcDSA**를 삽입한 다음, 확인을 클릭합니다.

    - **형식**을 **허용**으로 설정합니다.

    - **적용 대상**을 **하위 사용자 개체**로 설정합니다.

    - 아래쪽으로 스크롤하여 **모두 지우기**를 클릭합니다.

    - 위쪽으로 다시 스크롤하여 **암호 재설정**을 선택합니다.

    - **확인**을 클릭합니다.

- **확인**을 두 번 더 클릭하여 열려 있는 대화 상자를 닫습니다.

## <a name="next-steps"></a>다음 단계

[Active Directory 모드에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포](active-directory-deploy.md)

[SQL Server 빅 데이터 클러스터 Active Directory 통합 문제 해결](troubleshoot-active-directory.md)

[개념: Active Directory 모드에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포](active-directory-deployment-background.md)
