---
title: Active Directory 도메인에 여러 항목 배포
titleSuffix: SQL Server Big Data Cluster
description: 단일 Active Directory 도메인에 여러 SQL Server 빅 데이터 클러스터를 배포하는 방법을 알아봅니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4d5c30e4c3d7c3188920ecd15104b20a5472e306
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892503"
---
# <a name="deploy-multiple-big-data-clusters-2019-in-the-same-active-directory-domain"></a>동일한 Active Directory 도메인에 여러 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 동일한 Active Directory 도메인에서 여러 SQL Server 2019 빅 데이터 클러스터를 배포하고 통합하는 기능을 사용할 수 있는 SQL Server 2019 CU 5로 업데이트하는 방법을 설명합니다.

CU5 이전에는 하나의 AD 도메인에 여러 BDC를 배포하는 것을 방해하는 두 가지 문제가 있었습니다.

- 서비스 사용자 이름과 DNS 도메인 이름의 충돌
- 도메인 계정 보안 주체 이름

## <a name="object-name-collisions"></a>개체 이름 충돌

### <a name="service-principal-names-spn-and-dns-domain-naming-conflict"></a>SPN(서비스 사용자 이름)과 DNS 도메인 이름의 충돌

배포 시 제공된 도메인 이름은 AD DNS 도메인으로 사용됩니다. 즉, Pod는 이 DNS 도메인을 사용하여 내부 네트워크에서 서로 연결할 수 있습니다. 또한 사용자는 이 DNS 도메인을 사용하여 BDC 엔드포인트에 연결합니다. 따라서 BDC 내에서 서비스에 대해 생성된 SPN(서비스 사용자 이름)에는 이 AD DNS 도메인으로 한정된 Kubernetes Pod, 서비스 또는 엔드포인트 이름이 사용됩니다. 사용자가 도메인에 두 번째 클러스터를 배포하는 경우, Pod 이름뿐만 아니라 DNS 도메인 이름이 두 클러스터 간에 다르지 않기 때문에 생성되는 SPN의 FQDN은 동일합니다. 예를 들어 AD DNS 도메인이 `contoso.local`인 경우를 생각해 보겠습니다. Pod `master-0`에서 마스터 풀 SQL Server에 대해 생성된 SPN 중 하나는 `MSSQLSvc/master-0.contoso.local:1433`입니다. 사용자가 배포하려는 두 번째 클러스터에서 `master-0`의 Pod 이름이 동일하며 사용자는 동일한 SPN 문자열을 생성하는 동일한 AD DNS 도메인(``contoso.local``)을 제공합니다. Active Directory는 충돌하는 SPN이 생성되어 두 번째 클러스터에서 배포하지 못하게 되는 일을 방지합니다.

### <a name="domain-account-principal-names"></a>도메인 계정 보안 주체 이름

Active Directory 도메인을 사용하여 BDC를 배포하는 동안 BDC 내부에서 실행되는 서비스에 대해 여러 계정 보안 주체가 생성됩니다. 이 계정은 기본적으로 AD 사용자 계정입니다. CU5 이전에는 이러한 계정의 이름이 클러스터 간에 고유하지 않았습니다. 이런 현상은 두 개의 서로 다른 클러스터에서 BDC의 특정 서비스에 대해 동일한 사용자 계정 이름을 만들려고 할 때 확인됩니다. 두 번째로 배포되는 클러스터는 AD에서 충돌이 발생하고 계정을 만들 수 없습니다.

## <a name="resolution-for-collisions"></a>충돌 해결

### <a name="solution-to-solve-the-problem-with-spns-and-dns-domain---cu5"></a>SPN 및 DNS 도메인의 문제를 해결하는 방법 - CU5

SPN은 두 클러스터에서 서로 달라야 하므로, 배포 시 전달되는 DNS 도메인 이름도 서로 달라야 합니다. 배포 구성 파일 `subdomain`에서 새로 도입된 설정을 사용하여 다른 DNS 이름을 지정할 수 있습니다. 두 클러스터 간에 하위 도메인이 서로 다르고 이 하위 도메인을 통해 내부 통신이 발생할 수 있는 경우 SPN에는 필요한 고유성을 달성하는 하위 도메인이 포함됩니다.

>[!NOTE]
>하위 도메인 설정을 통해 전달된 값은 새 AD 도메인이 아니라 내부적으로 사용되는 DNS 도메인입니다.

예를 들어 마스터 풀 SQL Server SPN의 경우를 다시 생각해 보겠습니다. 하위 도메인이 `bdc`인 경우 앞에서 설명한 SPN은 `MSSQLSvc/master-0.bdc.contoso.local:1433`으로 변경됩니다.  

Active Directory 구성 사양에서 새로 도입된 하위 도메인 매개 변수의 값을 사용자 지정하는 것은 선택 사항입니다. 기본적으로 BDC 클러스터 이름이나 네임스페이스 이름은 하위 도메인 설정의 값을 계산하는 데 사용됩니다. 사용자가 하위 도메인 이름을 재정의하려는 경우 Active Directory 구성 사양에 도입된 새 하위 도메인 매개 변수를 사용하면 됩니다.

### <a name="solution-to-solve-the-problem-regarding-account-names-uniqueness"></a>계정 이름 고유성과 관련된 문제를 해결하는 방법

고유성을 보장하는 체계로 계정 이름을 업데이트하기 위해 Microsoft는 계정 접두사의 개념을 도입했습니다. 계정 접두사는 계정 이름에서 두 클러스터 간에 고유한 부분입니다. 계정 이름의 나머지 부분은 지정 서비스에 적용되는 상수입니다. 계정 이름의 새 형식은 `<prefix>-<name>-<podId>`입니다. 

>[!NOTE]
>Active Directory에서는 계정 이름을 20자로 제한합니다. BDC 클러스터는 Pod 및 StatefulSets를 구별하기 위해 8자를 사용해야 합니다. 따라서 계정 접두사로 사용할 12자가 남습니다.

계정 이름을 사용자 지정하는 것은 선택 사항입니다. Active Directory 구성 사양에서 `accountPrefix` 매개 변수를 사용합니다. SQL Server 2019 CU5에서는 구성 사양에 `accountPrefix`가 도입되었습니다. 기본적으로 하위 도메인 이름이 계정 접두사로 사용됩니다. 하위 도메인 이름이 12자 보다 길면 하위 도메인 이름에서 첫 12자에 해당하는 하위 문자열이 계정 접두사로 사용됩니다.

하위 도메인은 DNS에만 적용됩니다. 따라서 새 LDAP 사용자 계정 이름은 `bdc-ldap@contoso.local`입니다. `bdc-ldap@bdc.contoso.local`이 아닙니다.

## <a name="semantics"></a>의미 체계

요약하면, CU5에서 도메인의 여러 클러스터에 대해 추가된 매개 변수의 의미 체계는 다음과 같습니다.

### `subdomain`

- 선택적 필드
- 데이터 형식: 문자열
- 정의: 이 BDC 클러스터에 사용할 고유한 DNS 하위 도메인입니다. 이 값은 Active Directory 도메인에 배포된 각 클러스터에 대해 달라야 합니다.  
- 기본값: 제공되지 않으면 클러스터 이름이 기본값으로 사용됩니다.
- 최대 길이: 레이블당 63자(각 문자열이 점으로 구분된 레이블).
- 설명: 엔드포인트 DNS 이름은 해당 FQDN의 하위 도메인을 사용해야 합니다.

### `accountPrefix`

- 선택적 필드
- 데이터 형식: 문자열
- 정의: AD 계정 BDC 클러스터의 고유한 접두사가 생성됩니다. 이 값은 Active Directory 도메인에 배포된 각 클러스터에 대해 달라야 합니다.
- 기본값: 제공되지 않으면 하위 도메인 이름이 기본값으로 사용됩니다. 하위 도메인을 제공하지 않으면 클러스터 이름이 하위 도메인 이름으로 사용되므로, 클러스터 이름은 accountPrefix에도 상속됩니다. 하위 도메인이 제공되었으며 여러 부분으로 구성된 이름(하나 이상의 점 포함)인 경우 사용자는 accountPrefix를 제공해야 합니다. 
- 최대 길이: 12자 

## <a name="impact-on-ad-domain-and-dns-server"></a>AD 도메인 및 DNS 서버에 미치는 영향 

동일한 Active Directory 도메인에 대한 여러 BDC 배포를 수용하기 위해 AD 도메인 또는 도메인 컨트롤러에 필요한 변경이 없습니다. DNS 하위 도메인은 외부 엔드포인트 DNS 이름을 등록할 때 DNS 서버에서 자동으로 생성됩니다. 

## <a name="impact-on-setting-up-the-deployment-configuration-file-used-for-the-bdc-deployment"></a>BDC 배포에 사용되는 배포 구성 파일 설정에 미치는 영향 

컨트롤 플레인 구성 *control.json*의 *activeDirectory* 섹션에는 `subdomain`, `accountPrefix` 등 두 가지 옵션 매개 변수가 있습니다. 각 항목에 대해 클러스터 이름을 사용하는 기본 동작을 재정의하려는 경우에만 이러한 설정에 값을 제공하세요. 클러스터 이름은 네임스페이스 이름과 동일합니다.

또한 원하는 엔드포인트 DNS 이름(정규화된 이름인 경우)을 사용할 수 있으며, 동일한 도메인에 배포된 두 개의 빅 데이터 클러스터 간에 이름이 충돌하지 않습니다. 필요에 따라 하위 도메인 매개 변수 값을 사용하여 여러 클러스터에서 DNS 이름이 서로 다른지 확인할 수 있습니다.  예를 들어 게이트웨이 엔드포인트를 생각해 보겠습니다. 엔드포인트에 이름 `gateway`를 사용하고 BDC 배포의 일부로 DNS 서버에 자동으로 등록하려면 DNS 이름으로 `gateway.bdc1.contoso.local`을 사용합니다. `bdc1`은 하위 도메인이고 `contoso.local`은 AD DNS 도메인 이름입니다. 허용되는 다른 값은 `gateway-bdc1.contoso.local` 또는 간단히 `gateway.contoso.local`입니다.

## <a name="examples"></a>예제

다음은 하위 도메인 및 accountPrefix를 재정의하려는 경우 Active Directory 보안 구성의 예입니다. 

```json
    "security": { 
        "activeDirectory": { 
            "ouDistinguishedName":"OU=contosoou,DC=contoso,DC=local", 
            "dnsIpAddresses": [ "10.10.10.10" ], 
            "domainControllerFullyQualifiedDns": [ "contoso-win2016-dc.contoso.local" ], 
            "domainDnsName":"contoso.local", 
            "subdomain": "bdc", 
            "accountPrefix": "myprefix", 
            "clusterAdmins": [ "contosoadmins" ], 
            "clusterUsers": [ "contosousers1", "contosousers2" ] 
        } 
    } 
  
```

다음은 컨트롤 플레인 엔드포인트의 엔드포인트 사양 예입니다. 고유하고 정규화된 모든 값을 DNS 이름에 사용할 수 있습니다.
  
```json
        "endpoints": [ 
            { 
                "serviceType": "NodePort", 
                "port": 30080, 
                "name": "Controller", 
                "dnsName": "control-bdc1.contoso.local" 
            }, 
            { 
                "serviceType": "NodePort", 
                "port": 30777, 
                "name": "ServiceProxy", 
                "dnsName": "monitor-bdc1.contoso.local" 
            } 
        ] 
  
```

## <a name="questions"></a>질문

### <a name="do-you-need-to-create-separate-ous-for-different-clusters"></a>다른 클러스터에 대해 별도의 OU를 만들어야 할까요?

필수 사항은 아니지만 권장 사항입니다. 별개의 클러스터에 대해 별도의 OU를 제공하면 생성된 사용자 계정을 관리할 수 있습니다.

### <a name="how-to-revert-back-to-the-pre-cu5-behavior"></a>CU5 이전 동작으로 되돌리려면 어떻게 해야 하나요?

새로 도입된 `subdomain` 매개 변수를 수용할 수 없는 시나리오가 있을 수도 있습니다. 이미 `azdata` CLI로 업그레이드했으며 CU5 이전 릴리스를 배포해야 하는 경우를 예를 들겠습니다. 이런 경우는 매우 드물지만, CU5 이전 동작으로 되돌려야 하는 경우 `control.json`의 Active Directory 섹션에서 `false` 매개 변수를 `useSubdomain`로 설정하면 됩니다.

다음은 이런 시나리오의 경우 `useSubdomain`을 `false`로 설정하는 예입니다.

```console
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.useSubdomain=false" 
```

## <a name="next-steps"></a>다음 단계

[SQL Server 빅 데이터 클러스터 Active Directory 통합 문제 해결](troubleshoot-active-directory.md)
