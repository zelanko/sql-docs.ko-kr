---
title: 미사용 암호화
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 빅 데이터 클러스터의 미사용 데이터 암호화에 대한 모든 것을 알아봅니다.
author: dacoelho
ms.author: dacoelho
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 10/19/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: de0bc20d7551e8d42c5dc1463fada6ffcbb6a0fd
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257153"
---
# <a name="encryption-at-rest-concepts-and-configuration-guide"></a>미사용 데이터 암호화 개념 및 구성 가이드

SQL Server 빅 데이터 클러스터 CU8부터 포괄적인 암호화 기능 집합을 사용하여 플랫폼에 저장된 모든 데이터에 대한 애플리케이션 수준 암호화를 제공할 수 있습니다. 이 가이드에서는 SQL Server 빅 데이터 클러스터용 미사용 데이터 암호화 기능 집합에 대한 개념, 아키텍처 및 구성을 설명합니다.

SQL Server 빅 데이터 클러스터는 다음 두 위치에 데이터를 저장합니다.

* __SQL Server__ 마스터 인스턴스와
* 스토리지 풀 및 Spark에서 사용되는 __HDFS__ 입니다.

SQL Server 빅 데이터 클러스터의 데이터를 투명하게 암호화하려면 다음 두 가지 방법을 사용할 수 있습니다.

* __볼륨 암호화__ . 이 방법은 Kubernetes 플랫폼에서 지원되며 빅 데이터 클러스터 배포를 위한 모범 사례로 생각됩니다. 이 가이드에서는 볼륨 암호화에 대해 다루지 않습니다. SQL Server 빅 데이터 클러스터에 사용할 볼륨을 적절히 암호화하는 방법에 대한 가이드는 Kubernetes 플랫폼 또는 어플라이언스 설명서를 참조하세요.
* __애플리케이션 수준 암호화__ . 이 아키텍처는 디스크에 데이터를 쓰기 전에 애플리케이션이 처리하는 데이터 암호화를 나타냅니다. 볼륨이 노출되는 경우 대상 시스템도 동일한 암호화 키로 구성되지 않은 한 공격자는 다른 곳에서 데이터 아티팩트를 복원할 수 없습니다. 

SQL Server 빅 데이터 클러스터의 미사용 데이터 암호화 기능 집합은 SQL Server 및 HDFS 구성 요소에 대한 애플리케이션 수준 암호화의 핵심 시나리오를 지원합니다.

제공되는 기능은 다음과 같습니다.

* __시스템 관리형 미사용 데이터 암호화__ . 이 기능은 CU8에서 사용할 수 있습니다.
* 서비스 관리형 및 외부 키 공급자가 모두 통합된 __사용자 관리형 미사용 데이터 암호화(BYOK)__ . 현재는 서비스 관리형 사용자 생성 키만 지원됩니다.

## <a name="key-definitions"></a>주요 정의

### <a name="sql-server-big-data-clusters-key-management-service-kms"></a>SQL Server 빅 데이터 클러스터 KMS(키 관리 서비스)

SQL Server BDC 클러스터용 미사용 데이터 암호화 기능 집합에 대한 키 및 인증서 관리를 담당하는 컨트롤러 호스팅 서비스입니다. 이 서비스는 다음 기능을 지원합니다.

* 미사용 데이터 암호화에 사용되는 키 및 인증서를 안전하게 관리 및 저장.
* Hadoop KMS 호환성. BDC의 HDFS 구성 요소에 대한 키 관리 서비스 역할을 합니다.
* SQL Server TDE 인증서 관리.

지금은 다음 기능이 지원되지 않습니다.
* 키 버전 관리 지원. 

이 문서의 나머지 부분에서는 이 서비스를 __BDC KMS__ 로 지칭합니다. 또한 용어 __BDC__ 가 __SQL Server 빅 데이터 클러스터__ 컴퓨팅 플랫폼을 지칭하는 데 사용됩니다.

### <a name="system-managed-keys-and-certificates"></a>시스템 관리형 키 및 인증서

BDC KMS 서비스는 SQL Server 및 HDFS에 대한 모든 키 및 인증서를 관리합니다.

### <a name="user-provided-certificates"></a>사용자 제공 인증서

사용자가 BDC KMS에서 관리하는 키 및 인증서를 제공합니다. 이를 일반적으로 BYOK(Bring Your Own Key)라고 합니다.

### <a name="external-providers"></a>외부 공급자

외부 위임을 위한 BDC KMS 호환 외부 키 솔루션입니다. 지금은 이 기능이 지원되지 않습니다.

## <a name="encryption-at-rest-on-sql-server-big-data-clusters-cu8"></a>SQL Server 빅 데이터 클러스터 CU8에서의 미사용 데이터 암호화

SQL Server 빅 데이터 클러스터 CU8는 미사용 데이터 암호화 기능 집합의 초기 릴리스입니다. 시나리오를 완전히 평가하려면 이 문서를 자세히 읽어보세요.

이 기능 집합은 __BDC KMS 컨트롤러 서비스__ 를 도입하여 SQL Server 및 HDFS 모두에서 미사용 데이터 암호화를 위한 시스템 관리형 키 및 인증서를 제공합니다. 이러한 키 및 인증서는 서비스에서 관리하며, 이 설명서에서는 서비스와 상호 작용하는 방법에 대한 작업 지침을 제공합니다.

* __SQL Server__ 인스턴스는 설정된 [TDE(투명한 데이터 암호화)](../relational-databases/security/encryption/transparent-data-encryption.md) 기능을 활용합니다.
* __HDFS__ 는 각 Pod 내에서 네이티브 Hadoop KMS를 사용하여 컨트롤러의 BDC KMS와 상호 작용합니다. 이를 통해 HDFS에서 보안 경로를 제공하는 HDFS 암호화 영역을 사용할 수 있습니다.

### <a name="sql-server-instances"></a>SQL Server 인스턴스

* 시스템 생성 인증서는 TDE 명령과 함께 사용할 SQL Server Pod에 설치됩니다. 시스템 관리형 인증서 명명 표준은 `TDECertificate` + `timestamp`입니다. 예: `TDECertificate2020_09_15_22_46_27`.
* 마스터 인스턴스 BDC 프로비전된 데이터베이스와 사용자 데이터베이스는 자동으로 암호화되지 않습니다. DBA는 설치된 인증서를 사용하여 모든 데이터베이스를 암호화할 수 있습니다.
* 컴퓨팅 풀과 스토리지 풀은 시스템 생성 인증서를 사용하여 자동으로 암호화됩니다.
* 데이터 풀 암호화는 T-SQL `EXECUTE AT` 명령을 사용하여 기술적으로 가능하지만 권장하지 않으며 지금은 지원되지 않습니다. 이 기법을 사용하여 데이터 풀 데이터베이스를 암호화하는 것은 효과적이지 않으며 암호화가 원하는 상태에서 발생하지 않을 수 있습니다. 또한 이후 릴리스에 호환되지 않는 업그레이드 경로를 만듭니다.
* 지금은 인증서 회전이 없습니다. HA 배포를 사용하지 않는 경우 T-SQL 명령을 사용하여 새 인증서로 암호를 해독한 후 암호화하기 위해 지원됩니다.
* 암호화 모니터링은 기존의 TDE용 표준 SQL Server DMV를 통해 수행됩니다.
* TDE 사용 데이터베이스를 클러스터로 백업하고 복원하기 위해 지원됩니다.
* HA가 지원됩니다. SQL Server의 기본 인스턴스에서 데이터베이스가 암호화되면 해당 데이터베이스의 모든 보조 복제본이 암호화됩니다.

### <a name="hdfs-encryption-zones"></a>HDFS 암호화 영역

* HDFS에 암호화 영역 기능을 사용하도록 설정하려면 [Active Directory 통합](active-directory-prerequisites.md)이 필요합니다.
* 시스템 생성 키는 Hadoop KMS에 프로비전됩니다. 키 이름은 `securelakekey`입니다. CU8에서 기본 키는 256비트이며 256비트 AES 암호화를 지원합니다.
* 기본 암호화 영역은 `/securelake`라는 경로에서 위의 시스템 생성 키를 사용하여 프로비전됩니다.
* 사용자는 이 가이드에서 제공하는 지침을 사용하여 추가 키 및 암호화 영역을 만들 수 있습니다. 사용자는 키를 생성할 때 128, 192 또는 256의 키 크기를 선택할 수 있습니다.
* CU8에서는 HDFS에 대한 현재 위치 키 회전이 가능하지 않습니다. 대체 방법으로, distcp를 사용하여 한 암호화 영역에서 다른 암호화 영역으로 데이터를 이동할 수 있습니다.
* 암호화 영역을 기반으로 HDFS 계층화 탑재를 수행하는 것은 지원되지 않습니다.

## <a name="configuration-guide"></a>구성 가이드

SQL Server 빅 데이터 클러스터 미사용 데이터 암호화는 서비스 관리형 기능이며 배포 경로에 따라 추가 단계가 필요할 수 있습니다.

CU8부터 __SQL Server 빅 데이터 클러스터를 새로 배포__ 하는 동안 __기본적으로 미사용 데이터 암호화가 활성화되고 구성됩니다.__ 이는 다음을 의미합니다.

* BDC KMS 구성 요소가 컨트롤러에 배포되고 기본 키 및 인증서 집합을 생성합니다.
* SQL Server가 TDE 설정 상태로 배포되고 컨트롤러가 인증서를 설치합니다.
* Hadoop KMS(HDFS용)가 암호화 작업을 위해 BDC KMS와 상호 작용하도록 구성됩니다. HDFS 암호화 영역이 구성되고 사용할 준비가 됩니다.

이전 섹션에서 설명한 요구 사항 및 기본 동작이 적용됩니다.

__클러스터를 CU8로 업그레이드__ 하는 경우 __다음 섹션을 자세히 읽어 보세요__ .

### <a name="upgrading-to-cu8"></a>CU8로 업그레이드

   > [!CAUTION]
   > SQL Server 빅 데이터 클러스터 CU8로 업그레이드하기 전에 데이터 전체 백업을 수행하세요.

기존 클러스터에서는 업그레이드 프로세스가 사용자 데이터에 대한 암호화를 적용하지 않으며 HDFS 암호화 영역을 구성하지 않습니다. 이 동작은 의도적인 것이며 구성 요소별로 다음 사항을 고려해야 합니다.

* __SQL Server__

    1. __SQL Server 마스터 인스턴스__ 업그레이드 프로세스는 마스터 인스턴스 데이터베이스 및 설치된 TDE 인증서에 영향을 주지 않지만 업그레이드 프로세스 전에 데이터베이스 및 수동으로 설치한 TDE 인증서를 백업하는 것이 좋습니다. 또한 이러한 아티팩트를 SQL Server BDC 클러스터 외부에 저장하는 것이 좋습니다.
    1. __컴퓨팅 및 스토리지 풀__ . 이러한 데이터베이스는 시스템에서 관리하고 휘발성이며 클러스터 업그레이드 시 다시 만들어지고 자동으로 암호화됩니다.
    1. __데이터 풀__ . 업그레이드는 데이터 풀의 SQL Server 인스턴스 부분에 있는 데이터베이스에 영향을 주지 않습니다.

* __HDFS__

    1. __HDFS__ . 업그레이드 프로세스가 암호화 영역 외부에서 HDFS 파일 및 폴더에 영향을 주지 않습니다.
    1. __암호화 영역이 구성되지 않음__ . Hadoop KMS 구성 요소가 BDC KMS를 사용하도록 구성되지 않습니다. 업그레이드 후 HDFS 암호화 영역 기능을 구성하고 사용하도록 설정하려면 다음 섹션을 따릅니다.

### <a name="enable-hdfs-encryption-zones-after-upgrade"></a>업그레이드 후 HDFS 암호화 영역 사용

클러스터를 CU8로 업그레이드(`azdata upgrade`)하고 HDFS 암호화 영역을 사용하도록 설정하려면 다음 작업을 실행합니다.

요구 사항:

- [Active Directory](active-directory-prerequisites.md) 통합 클러스터.

- [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)](AD 모드에서 구성되고 클러스터에 로그인).

다음 절차에 따라 암호화 영역을 지원하도록 클러스터를 다시 구성합니다.

1. `azdata`를 사용하여 업그레이드한 후 다음 스크립트를 저장합니다.

    스크립트 실행 요구 사항:
        
    * 두 스크립트가 동일한 디렉터리에 있어야 합니다. 
    * `PATH의 `kubectl`
    * ```$HOME/.kube``` 폴더 내의 Kubernetes용 ```config``` 파일
    
    이 스크립트는 이름이 __```run-key-provider-patch.sh```__ 로 지정되어야 합니다.

    ```console
    #!/bin/bash
    
    if [[ -z "${BDC_DOMAIN}" ]]; then
      echo "BDC_DOMAIN environment variable with the domain name of the cluster is not defined."
      exit 1
    fi
    
    if [[ -z "${BDC_CLUSTER_NS}" ]]; then
      echo "BDC_CLUSTER_NS environment variable with the cluster namespace is not defined."
      exit 1
    fi
    
    kubectl get configmaps -n test
    
    diff <(kubectl get configmaps mssql-hadoop-storage-0-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py) <(kubectl get configmaps mssql-hadoop-storage-0-configmap -n $BDC_CLUSTER_NS -o json | python -m json.tool)
    
    diff <(kubectl get configmaps mssql-hadoop-sparkhead-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py) <(kubectl get configmaps mssql-hadoop-sparkhead-configmap -n $BDC_CLUSTER_NS -o json | python -m json.tool)
    
    # Replace the config maps.
    #
    kubectl replace -n $BDC_CLUSTER_NS -o json -f <(kubectl get configmaps mssql-hadoop-storage-0-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py)
    
    kubectl replace -n $BDC_CLUSTER_NS -o json -f <(kubectl get configmaps mssql-hadoop-sparkhead-configmap -n $BDC_CLUSTER_NS -o json | ./updatekeyprovider.py)
    
    # Restart the pods which need to have the necessary changes with the core-site.xml
    kubectl delete pods -n $BDC_CLUSTER_NS nmnode-0-0
    kubectl delete pods -n $BDC_CLUSTER_NS storage-0-0
    kubectl delete pods -n $BDC_CLUSTER_NS storage-0-1
    
    # Wait for sometime for pods to restart
    #
    sleep 300
    
    # Check for the KMS process status.
    #
    kubectl exec -n $BDC_CLUSTER_NS -c hadoop nmnode-0-0 -- bash -c 'ps aux | grep kms'
    kubectl exec -n $BDC_CLUSTER_NS -c hadoop storage-0-0 -- bash -c 'ps aux | grep kms'
    kubectl exec -n $BDC_CLUSTER_NS -c hadoop storage-0-1 -- bash -c 'ps aux | grep kms'
    ```

    이 스크립트는 이름이 __```updatekeyprovider.py```__ 로 지정되어야 합니다.

    ```python
    #!/usr/bin/env python3
    
    import json
    import re
    import sys
    import xml.etree.ElementTree as ET
    import os
    
    class CommentedTreeBuilder(ET.TreeBuilder):
        def comment(self, data):
            self.start(ET.Comment, {})
            self.data(data)
            self.end(ET.Comment)
    
    domain_name = os.environ['BDC_DOMAIN']
    
    parser = ET.XMLParser(target=CommentedTreeBuilder())
    
    core_site = 'core-site.xml'
    j = json.load(sys.stdin)
    cs = j['data'][core_site]
    csxml = ET.fromstring(cs, parser=parser)
    props = [prop.find('value').text for prop in csxml.findall(
        "./property/name/..[name='hadoop.security.key.provider.path']")]
    
    kms_provider_path=''
    
    for x in range(5):
        if len(kms_provider_path) != 0:
            kms_provider_path = kms_provider_path + ';'
        kms_provider_path = kms_provider_path + 'nmnode-0-0.' + domain_name
    
    if len(props) == 0:
        prop = ET.SubElement(csxml, 'property')
        name = ET.SubElement(prop, 'name')
        name.text = 'hadoop.security.key.provider.path'
        value = ET.SubElement(prop, 'value')
        value.text = 'kms://https@' + kms_provider_path + ':9600/kms'
        cs = ET.tostring(csxml, encoding='utf-8').decode('utf-8')
    
    j['data'][core_site] = cs
    
    kms_site = 'kms-site.xml.tmpl'
    ks = j['data'][kms_site]
    
    kp_uri_regex = re.compile('(<name>hadoop.kms.key.provider.uri</name>\s*<value>\s*)(.*)(\s*</value>)', re.MULTILINE)
    
    def replace_uri(match_obj):
        key_provider_uri = 'bdc://https@hdfsvault-svc.' + domain_name
        if match_obj.group(2) == 'jceks://file@/var/run/secrets/keystores/kms/kms.jceks' or match_obj.group(2) == key_provider_uri:
            return match_obj.group(1) + key_provider_uri + match_obj.group(3)
        return match_obj.group(0)
    
    ks = kp_uri_regex.sub(replace_uri, ks)
    
    j['data'][kms_site] = ks
    print(json.dumps(j, indent=4, sort_keys=True))
    ```

    적절한 매개 변수를 사용하여 __```run-key-provider-patch.sh```__ 를 실행합니다. 

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에서 미사용 데이터 암호화를 효과적으로 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

- [미사용 데이터 암호화 - SQL Server TDE](encryption-at-rest-sql-server-tde.md)
- [미사용 데이터 암호화 - HDFS 암호화 영역](encryption-at-rest-hdfs-encryption-zones.md)

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 다음 개요를 참조하세요.

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요?](big-data-cluster-overview.md)
